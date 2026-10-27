# hydro_practices

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Hands-On-HydroAI-Education-Materials/hydro_practices/main?urlpath=lab) [![Open in notebook.link](https://img.shields.io/badge/launch-notebook.link-F37626?logo=jupyter&logoColor=white)](https://notebook.link/github/Hands-On-HydroAI-Education-Materials/hydro_practices/tree/main/lab/)

두 링크 모두 hydro_practices 폴더 전체를 JupyterLab으로 엽니다.

| 실행 환경 | 설정 파일 | torch | 용도 |
|---|---|---|---|
| Binder | `binder/environment.yml` | 설치됨 (CPU 전용) | 실습 코드 실행 |
| notebook.link | `.nblink/environment.yml` | 설치 불가 | 노트북 열람, pandas/matplotlib 셀 실행 |

- 두 서비스 모두 링크를 열면 설정 파일을 읽어 환경을 자동으로 설치합니다. Binder는 처음 실행할 때 이미지를 빌드하므로 몇 분 걸릴 수 있습니다.
- Binder에는 GPU가 없습니다. 노트북은 GPU가 있으면 GPU를, 없으면 CPU를 사용합니다.
- notebook.link는 브라우저(WebAssembly)에서 실행되며, PyTorch·Lightning·NeuralHydrology는 브라우저용 빌드가 없어 `import torch` 셀이 실행되지 않습니다.

## 실습 노트북

| 노트북 | 내용 | Binder | notebook.link |
|---|---|---|---|
| [Example-1](1_neural_net_실습자료/Example-1_basic_nn_in_pytorch.ipynb) | 간단한 신경망 만들기와 결과 그래프 | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Hands-On-HydroAI-Education-Materials/hydro_practices/main?urlpath=lab/tree/1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-1_basic_nn_in_pytorch.ipynb) | [![Open in notebook.link](https://img.shields.io/badge/launch-notebook.link-F37626?logo=jupyter&logoColor=white)](https://notebook.link/github/Hands-On-HydroAI-Education-Materials/hydro_practices/tree/main/lab/?path=1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-1_basic_nn_in_pytorch.ipynb) |
| [Example-2](1_neural_net_실습자료/Example-2_intro_do_backpropagation.ipynb) | 역전파(Backpropagation) 소개 | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Hands-On-HydroAI-Education-Materials/hydro_practices/main?urlpath=lab/tree/1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-2_intro_do_backpropagation.ipynb) | [![Open in notebook.link](https://img.shields.io/badge/launch-notebook.link-F37626?logo=jupyter&logoColor=white)](https://notebook.link/github/Hands-On-HydroAI-Education-Materials/hydro_practices/tree/main/lab/?path=1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-2_intro_do_backpropagation.ipynb) |
| [Example-3](1_neural_net_실습자료/Example-3_lstms.ipynb) | LSTM | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Hands-On-HydroAI-Education-Materials/hydro_practices/main?urlpath=lab/tree/1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-3_lstms.ipynb) | [![Open in notebook.link](https://img.shields.io/badge/launch-notebook.link-F37626?logo=jupyter&logoColor=white)](https://notebook.link/github/Hands-On-HydroAI-Education-Materials/hydro_practices/tree/main/lab/?path=1_neural_net_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/Example-3_lstms.ipynb) |
| [NeuralHydrology 실습](2_neuralhydrology_실습자료/neuralhydrology_실습.ipynb) | 용담댐 하류 수위 예측 (CudaLSTM) | [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Hands-On-HydroAI-Education-Materials/hydro_practices/main?urlpath=lab/tree/2_neuralhydrology_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/neuralhydrology_%EC%8B%A4%EC%8A%B5.ipynb) | [![Open in notebook.link](https://img.shields.io/badge/launch-notebook.link-F37626?logo=jupyter&logoColor=white)](https://notebook.link/github/Hands-On-HydroAI-Education-Materials/hydro_practices/tree/main/lab/?path=2_neuralhydrology_%EC%8B%A4%EC%8A%B5%EC%9E%90%EB%A3%8C/neuralhydrology_%EC%8B%A4%EC%8A%B5.ipynb) |
