# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Hands-on teaching materials (Korean-language) for hydrology + deep learning. It is a set of Jupyter notebooks, not a package: there is no build, lint, or test suite. "Running" something means executing notebook cells. Markdown cells are written in Korean for students, and code comments are mostly English. Keep that split when editing.

- `1_neural_net_실습자료/`: intro to neural nets in PyTorch. These are adapted from Josh Starmer's (StatQuest) examples and edited by YoungDon Choi (K-water Research Institute). Keep the copyright line.
  - Example-1: a hand-built `nn.Module` with fixed pre-trained weights, plotted with seaborn.
  - Example-2: backpropagation, training one parameter with `lightning` (`L.LightningModule`) and `SGD`.
  - Example-3: an LSTM built from scratch, then `nn.LSTM`, trained with Lightning + Adam and logged to TensorBoard (`lightning_logs/`).
  - `images/`: figures referenced by `<img src="images/...">` in markdown cells.
- `2_neuralhydrology_실습자료/`: training a `cudalstm` with the [NeuralHydrology](https://github.com/neuralhydrology/neuralhydrology) library. It predicts hourly water level at one gauge downstream of Yongdam Dam (Geum River, Korea).

## Dependencies

Two environment files exist, one per hosted launcher (both linked from README badges, both open the repo root in JupyterLab):
- `binder/environment.yml` (mybinder.org): the real runtime. conda-forge stack plus pip installs of CPU-only `torch` (via `--extra-index-url https://download.pytorch.org/whl/cpu`), `lightning`, and `neuralhydrology==1.13.0`. Binder has no GPU.
- `.nblink/environment.yml` (notebook.link): runs in the browser via WebAssembly, using the emscripten-forge channel. PyTorch, Lightning, and NeuralHydrology have no WASM builds, so they are deliberately left out; adding them would break the environment solve. notebook.link is for viewing only.

Device handling: the neuralhydrology notebook sets `device = "cuda:0" if torch.cuda.is_available() else "cpu"` and writes it into the config. The Lightning `Trainer`s in Examples 2 and 3 use the default `accelerator="auto"`, so they fall back to CPU on their own.

To execute a notebook headlessly:
```bash
jupyter nbconvert --to notebook --execute --inplace "2_neuralhydrology_실습자료/neuralhydrology_실습.ipynb"
```
Run it from the notebook's own directory. The neuralhydrology notebook uses relative paths like `./data/...`.

## NeuralHydrology pipeline (folder 2)

The notebook runs this flow in order:

1. **Source data**: `data/training_data/time_series/Train_YD_Dam_Downstream_hourly.csv` is one wide hourly CSV for 2014-10 onward. Columns are station codes with a suffix: `_hwl` = water level, `_hrf` = rainfall, `_hoflw`/`_hiflw` = dam outflow/inflow (`yd` = Yongdam, `mj` = Muju, `dc` = Daecheong).
2. **Per-target split**: the notebook picks `input` and `target` column lists. It writes `input/hourly/<target>/...csv` and `target/hourly/<target>/...csv` under `training_data/time_series/`. This layout is what the `dataset: hourlycsv` loader expects. `hourlycsv` is not one of upstream NeuralHydrology's built-in datasets, so it probably comes from a custom or forked build.
3. **Basin file**: `data/Train_YD_Dam_Downstream.txt` holds a single "basin" ID, `Train_YD_Dam_Downstream`. The results are keyed by that name: `results["Train_YD_Dam_Downstream"]["1h"]`.
4. **Config**: the notebook loads `data/Train_Overwrite.yml`, updates the experiment, path, and variable keys, and then **writes the file back in place**. That file is therefore both the template and the last-run config. Train/val/test periods, `seq_length: 720`, and the LR schedule live there.
5. **Train**: `start_run(config_file=...)` creates `data/runs/<target>/<model>/<experiment>_<ddmm_HHMMSS>/`. That directory holds `config.yml`, `model_epochNNN.pt`, `train_data/train_data_scaler.yml`, and `img_log/`. The notebook picks the newest run directory by mtime.
6. **Evaluate**: `get_tester(..., period="train"|"validation"|"test")` produces obs/sim xarrays and NSE, which the notebook plots.

`data/Train_YD_Dam_Downstream_hwl_targets_lists.yml` maps each downstream gauge to the dam outflow, rain gauges, and upstream water-level gauges to use as inputs. It reflects the river network topology. The notebook currently uses only the first entry (`3004630_hwl` ← `yd_hoflw`, `3003430_hrf`). Use this file when switching to another target station.

## Gotchas

- The notebooks build paths relative to their own directory (`Path.cwd()`). The committed `config.yml` files under `data/runs/` and the `Train_Overwrite.yml` template still contain absolute paths from the original machine (`/home/neuralriverops/...`). The notebook overwrites the path keys before each run.
- `dataset: hourlycsv` is not registered in upstream `neuralhydrology` 1.13.0 (built-ins: `camels_*`, `hourly_camels_us`, `generic`, `lamah_*`, `caravan`). `start_run` fails unless a custom dataset class is registered with `neuralhydrology.datasetzoo.register_dataset("hourlycsv", ...)`.
- `data/runs/` contains committed example run outputs, including `.pt` weights. New training runs add more timestamped directories there.
