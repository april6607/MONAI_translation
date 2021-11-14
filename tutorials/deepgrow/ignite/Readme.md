## Deepgrow 예제

이 폴더에는 Deepgrow 2D/3D 모델을 실행하고 검증하는 예가 포함되어 있습니다. 또한 훈련된 모델에 대해 추론을 실행할 수 있는 노트북도 있다.
 
다음을 기반으로 구성:

Sakinis 등, 완전 컨볼루션 신경망을 통한 의료 영상의 대화형 분할.
(2019) https://arxiv.org/abs/1903.08205

#### 1. 데이터
Deepgrow 모델을 훈련하려면 데이터가 필요하다. 예에 사용되는 일부 공개 데이터 세트는 Medical Segmentation Decathlon 또는 Synapse에서 다운로드할 수 있다.

#### 2. 질문과 버그
- MONAI 사용과 관련된 질문은 MONAI의 주 저장소에 있는 토론 탭을 참조하십시오.
- MONAI 기능과 관련된 버그는 주 저장소에서 이슈를 만드십시오.
- 튜토리얼 실행과 관련된 버그의 경우 이 저장소에서 문제를 만드십시오.

#### 3. 노트북 목록 및 예제
[Prepare Your Data](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/prepare_dataset.py)

이 예는 표준 PyTorch 프로그램이며 사용자가 2D 또는 3D에 대한 교육 입력을 준비할 수 있도록 도와줍니다.

```
# Run to know all possible options
python ./prepare_dataset.py -h

# Prepare dataset to train a 2D Deepgrow model
python ./prepare_dataset.py
    --dimensions   2 \
    --dataset_root MSD_Task09_Spleen \
    --dataset_json MSD_Task09_Spleen/dataset.json \
    --output       deepgrow/2D/MSD_Task09_Spleen
    
# Prepare dataset to train a 3D Deepgrow model
python ./prepare_dataset.py
    --dimensions   3 \
    --dataset_root MSD_Task09_Spleen \
    --dataset_json MSD_Task09_Spleen/dataset.json \
    --output       deepgrow/3D/MSD_Task09_Spleen
```

[Deepgrow 2D Training](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/train.py)

이 예는 표준 PyTorch 프로그램이며 사용자가 2D를 위해 사전 처리된 데이터 세트에 대한 교육을 실행할 수 있도록 도와줍니다.

```
# Run to know all possible options
python ./train.py -h
# Train a 2D Deepgrow model on single-gpu
python ./train.py
    --input       deepgrow/2D/MSD_Task09_Spleen/dataset.json \
    --output      models/2D \
    --epochs      50
# Train a 2D Deepgrow model on multi-gpu (NVIDIA)
python -m torch.distributed.launch \
    --nproc_per_node=`nvidia-smi -L | wc -l` \
    --nnodes=1 \
    --node_rank=0 \
    --master_addr="localhost" \
    --master_port=1234 \
    -m train \
    --multi_gpu true \
    --input       deepgrow/2D/MSD_Task09_Spleen/dataset.json \
    --output      models/2D \
    --epochs      50
# After training to export/save as torch script model
python ./train.py
    --input       models/2D/model.pt \
    --output      models/2D/model.ts \
    --export      true
```

[Deepgrow 2D Validation](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/validate.py)

이 예는 표준 PyTorch 프로그램이며 사용자가 훈련된 2D 모델에 대한 평가를 실행할 수 있도록 도와줍니다.

```
# Run to know all possible options
python ./validate.py -h
# Evaluate a 2D Deepgrow model
python ./validate.py
    --input       deepgrow/2D/MSD_Task09_Spleen/dataset.json \
    --output      eval/2D \
    --model_path  models/2D/model.pt
```
    
[Deepgrow 2D Inference](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/inference.ipynb)

이 노트북은 Deepgrow 2D 모델에 대한 추론을 실행하기 전에 사전 변환을 실행하는 데 도움이 됩니다. 또한 변환 후 실행을 통해 최종 레이블 마스크를 얻을 수 있습니다.

[Deepgrow 3D Training](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/train_3d.py)

이것은 3D 훈련을 실행하기 위한 기본 인수를 재정의한 train.py의 연장선입니다.

```
# Run to know all possible options
python ./train_3d.py -h
# Train a 3D Deepgrow model on single-gpu
python ./train_3d.py
    --input       deepgrow/3D/MSD_Task09_Spleen/dataset.json \
    --output      models/3D \
    --epochs      100
# Train a 3D Deepgrow model on multi-gpu (NVIDIA)
python -m torch.distributed.launch \
    --nproc_per_node=`nvidia-smi -L | wc -l` \
    --nnodes=1 \
    --node_rank=0 \
    --master_addr="localhost" \
    --master_port=1234 \
    -m train_3d \
    --multi_gpu true \
    --input       deepgrow/3D/MSD_Task09_Spleen/dataset.json \
    --output      models/3D \
    --epochs      100
# After training to export/save as torch script model
python ./train_3d.py
    --input       models/3D/model.pt \
    --output      models/3D/model.ts \
    --export      true
```
    
[Deepgrow 3D Validation](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/validate_3d.py)

3D 유효성 검사를 실행하기 위한 기본 인수를 재정의하는 Validate.py의 확장입니다

```
# Run to know all possible options
python ./validate_3d.py -h
# Evaluate a 3D Deepgrow model
python ./validate_3d.py
    --input       deepgrow/3D/MSD_Task09_Spleen/dataset.json \
    --output      eval/3D \
    --model_path  models/3D/model.pt
```
    
[Deepgrow 3D Inference](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/inference_3d.ipynb)

이 노트북은 Deepgrow 3D 모델에 대한 추론을 실행하기 전에 사전 변환을 실행하는 데 도움이 됩니다. 또한 변환 후 실행을 통해 최종 레이블 마스크를 얻을 수 있습니다.

[Deepgrow Stats](https://github.com/Project-MONAI/tutorials/blob/master/deepgrow/ignite/handler.py)

다중 레이블 마스크가 있는 데이터 집합에 대해 트레인/유효성 검사를 실행하는 동안 지역/기관별 통계를 캡처하고, 스냅샷을 저장하고, 출력을 저장할 수 있는 기본 Ignite 핸들러를 포함합니다. 기본적으로 처리기는 교육/유효성 검사 단계의 일부로 추가됩니다.
 
