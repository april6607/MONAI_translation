#### NVFlare를 통한 Federated learning

여기의 예는 [NVFlare](https://pypi.org/project/nvflare/) 및 MONAI 기반 트레이너와 연합 학습 모델을 훈련하는 방법을 보여준다.

1. Nvflare_example는 로컬 컴퓨터에서 MONAI와 함께 NVFlare를 실행하여 FL 설정을 시뮬레이션하는 방법을 보여준다(서버와 클라이언트는 로컬 호스트를 통해 통신한다). 또한 관리 API를 사용하여 시뮬레이션한 FL 실험을 완전히 자동화하는 방법을 보여줍니다. 실험을 간소화하기 위해 본 튜토리얼에서 최대 8개의 클라이언트를 위한 시작 키트가 준비되어 있습니다.
2. [nflare_example_docker](https://github.com/Project-MONAI/tutorials/blob/master/federated_learning/nvflare/nvflare_example_docker/README.md)는 MONAI와 함께 FL을 실행하는 것과 NVFlare를 사용하여 서버와 각 클라이언트를 위한 도커 컨테이너를 사용하여 실제 환경을 보다 쉽게 배치하는 방법에 대한 자세한 정보를 제공합니다.
