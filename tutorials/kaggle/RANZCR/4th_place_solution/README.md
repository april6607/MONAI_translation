## 개요
이 파이프라인은 캐글의 RANZCR CLiP - 카테터 및 라인 위치 챌린지의 4위 솔루션에서 수정되었다. https://www.kaggle.com/c/ranzcr-clip-catheter-line-classification

최초 솔루션은 수냉식 팀이 제작했으며, 저자는 Dieter(https://www.kaggle.com/christofhenkel)와 Psi(https://www.kaggle.com/philippsinger))이다.

## 준비물
MONAI docker를 사용하는 것이 좋습니다.

```
docker pull projectmonai/monai:latest
```

그렇지 않으면 모나이가 필요한 라이브러리를 제외하고 opencv-python 및 Scipy가 설치되어 있는지 확인하십시오. 명령은 다음과 같습니다:

```
pip install opencv-python
pip install scipy
```

경쟁 사이트에서 데이터 세트를 다운로드하고 config/default_config.py에서 데이터 세트 경로를 수정하십시오.

이 파이프라인에서 데이터 분할 파일 train_train.csv는 원래 솔루션과는 다른 다음과 같은 공용 커널에서 달성됩니다: https://www.kaggle.com/underwearfitting/how-to-properly-split-folds을 다운로드하여 데이터 세트의 경로에 넣으십시오.

## 사용 GPU :
단일 NVIDIA Tesla V100 32G

## 추론
로컬에서 추론을 수행하는 명령은 다음과 같습니다 :

```
python train.py -c cfg_seg_40_1024d_full -i True -p your_actual_local_weight_folder_path
```

Kaggle에서, 제출을 위한 커널이 인터넷 접속을 지원하지 않기 때문에, 당신은 `MONAI/monai`의 코드를 복사하고 (MONAI 도커를 사용하는 경우, 경로는 `/opt/monai/monai/`) 사용할 전체 폴더를 Kaggle 데이터 세트로 업로드해야 할 필요가 있다. 참조할 수 있도록 `train.py`의 `run_infer` function 함수를 선택하고 스크립트를 작성하십시오.

## Places uncovered
원래 솔루션은 6가지 다른 모델/훈련 전략으로 구성됩니다.

1.	Backbone: EfficientNet-b8, with imagenet pretrained weights
2.	Backbone: EfficientNet-b8, with AdvProp (https://rwightman.github.io/pytorch-image-models/models/advprop/) pretrained weights
3.	Backbone: EfficientNet-b7, with imagenet pretrained weights
4.	Backbone: EfficientNet-b7, with AdvProp pretrained weights
5.	Backbone: EfficientNet-b7, with noisy student(https://rwightman.github.io/pytorch-image-models/models/noisy-student/) pretrained weights
6.	Backbone: EfficientNet-b7, with noisy student pretrained weights (different training strategies)

그러나, 두 번째, 세 번째, 네 번째 방법만이 재현에 적용된다. 그 이유는 MONAI에서 구현된 EfficientNet이 EfficientNet-PyTorch(https://github.com/lukemelas/EfficientNet-PyTorch) Team Watercooled는 이 저장소를 참조함)를 참조했기 때문이다. EfficientNet-PyTorch는 드러나지 않은 사전 검증된 가중치를 제공하지 않으며, 효율적인 넷 구조의 일부 차이 때문에 대신 파이토치 이미지 모델의 가중치를 사용할 수 없다.

## 성능
위에서 언급한 이유에 따르면 이 파이프라인은 원래 솔루션을 완전히 재현하지 못합니다. 적절한 사전 훈련 가중치를 가진 모델의 경우, 유사한 성능에 도달할 수 있다.

AdvProp 사전 검증된 가중치를 가진 단일 효율적인 net-b8 모델을 사용하여 교육하면 다음을 달성할 수 있습니다.

1. one seed can reach to around `0.97013` for private LB and `0.97092` for public LB.
2. four seeds can reach to around `0.97429` for private LB and `0.97460` for public LB.

명령은 다음과 같습니다:

```
python train.py -cfg_cfg_40_full -s 657028
python train.py -cfg_cfg_40_full -s 770799
python train.py -cfg_cfg_40_full -s 825460
python train.py -cfg_cfg_40_full_s 962001
```

또한 모델이 더 많은 앙상블은 더 높은 점수를 얻을 수 있습니다:

```
python train.py -cfg_cfg_fille_16_ch_fille -s 868472s 868472
python train.py -cfg_cfg_fille_16_ch_fille_s 183105

python train.py -cfg_cfg_filen_16_ch_filen_full -s 701922
python train.py -cfg_cfg_fille_16_ch_full_s 7259
```
