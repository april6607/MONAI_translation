# CT 영상에서 폐 환부(병변) 분할을 위한 U-Net 모델

[챌린지 웹사이트](https://covid-segmentation.grand-challenge.org/COVID-19-20/) | [리더보드](https://covid-segmentation.grand-challenge.org/evaluation/challenge/leaderboard/)
이 디렉토리에는 [COVID-19 LUNG CT LESION SEGMENTATION CHALLENGE – 2020](https://covid-segmentation.grand-challenge.org/COVID-19-20/) (MICCAI 승인 이벤트)에 대한 교육, 검증 및 추론을 위해 MONAI를 사용하는 간단한 기준 방법이 포함되어 있습니다. 구현은 추가 알고리즘 개선을 위한 출발점이 될 수 있는 기본 딥 러닝 파이프라인이다.
 
## 목차
1. 요구사항들
2. 종속성 및 설치
3. 사용법

   i.	훈련
   
   ii.	추론
   
   iii.	결과
   
   iv.	추가 판독값

5. 리더보드에 제출
6. 라이선스

## 요구사항들

스크립트는 다음과 같이 테스트됩니다:
-	Ubuntu 18.04 | Python 3.6 | CUDA 10.2

자동 혼합 정밀도 기능을 갖춘 GPU:

-	기존 교육 파이프라인에는 약 5.5GB 메모리가 필요합니다.
-	기본 추론 파이프라인에는 약 2.3GB 메모리가 필요합니다.

## 종속성 및 추론
#### Pytorch
Pytorch 설치 지침을 따르십시오. 사용 가능한 설치가 있는지 확인하려면 다음을 실행하십시오.

`python -c 'import torch; print(torch.rand(4, 2, device="cuda"))'`

#### MONAI
`pip install "git+https://github.com/Project-MONAI/MONAI#egg=monai[nibabel,ignite,tqdm]"`

자세한 내용은 설치 안내서를 참조하십시오.

## 사용법
run_net.py를 로컬 폴더에 다운로드합니다. 이러한 지침은 챌린지 데이터도 다운로드되어 동일한 폴더에 압축을 푼 상태에서 가정합니다.
교육 (및 모든 epoch마다 검증)
python run_net.py train --data_folder "COVID-19-20_v2/Train" --model_folder "runs"
교육 중에 상위 3개 모델은 각 epoch 검증을 기반으로 선택되고 –model_folders에 저장됩니다.
훈련은 편리한 파일 로딩 모듈과 MONAI를 사용한 몇 가지 강도 및 공간 무작위 증강 기능을 사용합니다.
-	LoadImaged, AddChannelld, Orientationd, Spacingd, ScaleIntensityRanged
1.25mm x 1.25mm x 5.00mm 해상도와 [-1000.0, 500.0] 사이의 강도를 [0.0, 1.0]으로 조정하여 영상 데이터를 LPS 방향(왼쪽에서 오른쪽으로, 뒤쪽에서 앞쪽, 상위에서 하위)으로 로드합니다.
-  SpatialPadd
볼륨의 처음 두 공간 치수에 192x192 voxels 이상이 되도록 패딩합니다.
-	RandAffined, RandGaussianNoised, RandFlipd
모든 훈현 반복 시 데이터 증강이 무작위화됩니다.
-	RandCropByPosNegLabeld
전경(열) 및 배경(volume의 다른 위치)에서 균형 잡힌 검체를 사용하여 무작위로 이미지/라벨 쌍(192, 192, 16)을 샘플링합니다.
-	U-Net model
UNet 모델은 monai.networks.nets.BasicUNet의 것입니다.
-	Sliding window inference
분할은 (192, 192, 16)로 창크기의 monai.inferers.SlidingWindowInferer에 의해 생성됩니다. 이 추론 파이프라인의 평가 점수는 원래 데이터 해상도에 계산되지 않으며, 모델 선택 목적으로만 여기에 제시됩니다.
추론
python run_net.py infer --data_folder "COVID-19-20_v2/Validation" --model_folder "runs"
이 명령어는 최상의 검증 모델을 로드하고 추론을 실행하고 예측값을 ./output에 저장합니다.




결과
 
이 기준 방법은 유효성 검사 세트에서 0.6904 ± 0.1801 Dice 점수를 획득합니다.
추가 판독값
-	MONAI 기술 문서를 보려면 docs.monai.io를 방문하십시오.
-	다음을 포함한 자세한 예를 보려면 Project-MONAI/tutorials을 방문하십시오.
-	3D segmentation pipelines,
-	Dynamic UNet,
-	Training acceleration.
리더보드에 제출
기본적으로 ./output/to_submit에서 생성된 예측은 제출할 준비가 되어 있습니다. 폴더를 압축하고 업로드 지시에 따라 제출하세요.
문의 사항은 챌린지 주최측에 문의하십시오.
라이선스
이 코드는 Apache License 2.0에 따라 라이선스가 부여된다.
