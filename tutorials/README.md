이 저장소에는 MONAI에 대한 사용 지침서가 있습니다.

### 1. 요구 사항들

대부분의 예제와 사용 지침서에는 [matplotlib](https://matplotlib.org/)와 [Jupyter Notebook](https://jupyter.org/).

이것들은 다음을 통해 설치할 수 있습니다:

```
python -m pip install -U pip
python -m pip install -U matplotlib
python -m pip install -U notebook
```


일부 예제에서는 종속성을 선택적으로 사용해야 할 수 있습니다. Optional import 에러가 발생할 경우 MONAI의 [설치 가이드](https://docs.monai.io/en/latest/installation.html)에 따라 관련 패키지를 설치해 주세요, 또는 다음을 사용하여 모든 optional requirements(요구사항)을 설치합니다:

```
pip install -r https://raw.githubusercontent.com/Project-MONAI/MONAI/dev/requirements-dev.txt
```

#### Colab으로부터 노트북을 실행시키기

대부분의 Jupyter 노트북에는 “Colab에서 열기” 버튼이 있습니다. 해당 노트북 콘텐츠로 Colab 페이지를 시작하려면 버튼을 마우스 오른쪽 버튼으로 클릭하고 “새 탭에서 링크 열기”를 선택하십시오.

Colab을 통해 GPU 리소스를 사용하려면 런타임 유형을 `GPU`로 변경해야 합니다.
1. `Runtime` 메뉴에서 `Change runtime type`을 선택합니다.
2. drop-down 메뉴에서 `GPU`를 선택합니다.
3. `SAVE`를 클릭합니다. 그러면 노트북이 재설정되고 로봇인지 여부를 물을 수 있습니다(이 지침은 사용자가 아닌 것을 가정).

실행중:

```
!nvidia-smi
```

셀에서 이것이 작동하는지 확인하고 어떤 종류의 하드웨어에 접근할 수 있는지 보여줄 것입니다.

#### 데이터

일부 노트북은 추가 데이터가 필요합니다. [runexamples.sh](https://github.com/Project-MONAI/tutorials/blob/master/runexamples.sh) 스크립트를 실행하여 다운로드 할 수 있습니다. 

### 2. 질문과 버그
- MONAI 사용과 관련된 질문은 MONAI의 주 저장소에 있는 Discussions tab을 참조하십시오.
- MONAI 기능과 관련된 버그는 main repository에서 이슈를 만드십시오.
- 튜토리얼 실행과 관련된 버그의 경우 이 저장소에서 문제를 만드십시오.

### 3. 개발자 참고사항
시간을 절약하기 위해 변수를 수정하여 불필요한 for 루프 반복을 방지합니다. 따라서 교육 중에 각각 max_epochs 및 val_interval 변수를 training epochs 횟수와 검증 간격에 사용하십시오.

만약 당신의 노트북인 Epoch라는 개념을 사용하지 않는다면, 그것을 runner.sh의 doesnt_contain_max_epochs 변수에 추가해 주세요. 이를 통해 max_epochs를 찾지 못해도 문제가 되지 않는다는 것을 알 수 있습니다.

테스트하는 동안 변수를 1로 설정하여 도움이 되는 다른 변수가 있으면 runner.sh에서 strings_to_place에 추가합니다.

### 4. 노트북 목록 및 예제
#### 2D 분류
Mednist_tutorial

이 노트북은 MONAI 기능을 기존 PyTorch 프로그램에 쉽게 통합하는 방법을 보여줍니다. 이것은 MedNIST 데이터 세트를 기반으로 하여 초보자에게 튜토리얼로 매우 적합합니다. 또한 이 튜토리얼은 MONAI의 내장 폐색 민감도 기능을 사용합니다.

#### 2D 분할
torch examples

UNet 및 합성 데이터 세트를 기반으로 한 2D 세분화의 교육 및 평가 예제이다. 예제는 표준 PyTorch 프로그램이며 사전 기반과 배열 기반 버전을 모두 가지고 있다.

#### 3D 분류
ignite examples

DenseNet3D 및 IXI 데이터 세트를 기반으로 한 3D 분류의 교육 및 평가 예제이다. 예제는 PyTorch Ignite 프로그램이며 사전 기반 및 배열 기반 변환 버전을 모두 가지고 있다.

torch examples.

DenseNet3D 및 IXI 데이터 세트를 기반으로 한 3D 분류의 교육 및 평가 예제이다. 예제는 표준 PyTorch 프로그램이며 사전 기반 및 배열 기반 변환 버전을 모두 가지고 있다.

#### 3D 분할
ignite examples

UNet3D 및 합성 데이터 세트를 기반으로 한 3D 세분화의 교육 및 평가 예제이다. 예제는 PyTorch Ignite 프로그램이며 사전 기반 및 배열 기반 변환을 모두 가지고 있다.

torch examples.

UNet3D 및 합성 데이터 세트를 기반으로 한 3D 세분화의 교육, 평가 및 추론 예제이다. 예제는 표준 PyTorch 프로그램이며 사전 기반 및 배열 기반 변환 버전을 모두 가지고 있다.

brats_segmentation_3d

이 튜토리얼은 MSD Brain Tumor dataset을 기반으로 다중 라벨 분할 작업의 교육 워크플로우를 구성하는 방법을 보여줍니다.

spleen_segmentation_3d_lightning

이 노트북은 MONAI가 PyTorch Lightning 프레임워크와 함께 어떻게 사용될 수 있는지를 보여줍니다.

spleen_segmentation_3d

이 노트북은 MSD Spleen dataset을 기반으로 한 3D 세분화의 end-to-end 교육 및 평가 예제입니다. 예제는 PyTorch 기반 프로그램에서 MONAI 모듈의 유연성을 보여줍니다.
-	사전 기반 교육 데이터 구조를 위한 변환입니다.
-	메타데이터와 함께 NlfTl 이미지를 로드합니다.
-	의료 영상 강도를 예상 범위로 조정합니다.
-	양수/음수 레이블 비율을 기준으로 균형 잡힌 이미지 샘플들을 잘라냅니다.
-	입출력 및 변환을 캐시에 저장하여 교육 및 검증 시간을 단축합니다.
-	3D 문할 작업을 위한 3D UNet, Dice loss function, Mean Dice metric.
-	슬라이딩 윈도우 추론
-	재현 가능성을 위한 결정론적 훈련

unet_segmentation_3d_catakyst

이 노트북에서는 MONAI를 Catalyst 프레임워크와 함께 사용하는 방법을 보여줍니다.

unet_segmentation_3d_ignite

이 노트북은 합성 데이터 세트를 기반으로 한 3D 세분화의 end-to-end 교육 및 평가 예제입니다. 예제는 PyTorch Ignite 프로그램이며, 특히 의료 영역별 변환 및 프로파일링을 위한 이벤트 핸들러(logging, TensorBoard, MLFlow 등)와 함께 MONAI의 몇 가지 주요 특징을 보여준다.

COVID 19-20 challenge baseline

이 폴더는 COVID-19 폐 CT 병변 분할 챌린지 – 2020(MICCAI 승인 이벤트)에 대한 훈련, 검증 및 추론을 위한 간단한 기본 방법을 제공한다.

unetr_btcv_segmentation_3d

이 노트북은 BTCV 챌린지 데이터 세트를 사용하여 다중 기관 분할 작업에 대한 UNETR의 교육 워크플로우를 구성하는 방법을 보여준다.

unetr_btcv_segmentation_3d_lightning

이 튜토리얼은 MONAI를 PyTorch Lightening 프레임워크와 함께 사용하여 BTCV 챌린지 데이터 세트를 사용하는 다중 기관 분할 작업에 대한 UNETR의 훈련 워크플로우를 구성하는 방법을 보여준다.

#### 2D 등록
registration using mednist

이 노트북은 64 x 64 X-Ray hands의 학습 기반 아핀(affine) 등록을 위한 빠른 데모를 보여줍니다.

#### 3D 등록
3D registration using paired lung CT

이 튜토리얼에서는 MONAI를 사용하여 단일 환자에 대한 서로 다른 시점에서 획득한 폐 CT 볼륨을 등록하는 방법을 보여줍니다.

#### Deepgrow
Deepgrow

이 예제에서는 2D/3D Deepgrow 모델을 교육/검증하는 방법을 보여줍니다. 또한 훈련된 Deepgrow 모델에 대한 추론을 실행하는 것을 보여줍니다.

#### 배치
BentoML

이것은 웹 서버로 BentoML을 사용하는 MONAI 네트워크를 훈련하고 배치하는 간단한 예로서, 로컬로 BentoML 저장소를 사용하거나 컨테이너형 서비스로 사용합니다.

Ray

이전 노트북의 훈련된 네트워크를 사용하여 Ray를 사용한 웹 서버 배포를 시연합니다.

#### 연합학습
NVFlare

이 예는 NVFlare 및 MONAI 기반 트레이너와 연합 학습 모델을 훈련하는 방법을 보여준다.

Substra

이 예에서는 연합 학습 플랫폼인 Subsra에서 3D 분할 토치 튜토리얼을 실행하는 방법을 보여준다.

#### 디지털 병리학
Whole Slide Tumor Detection

이 예에서는 전체 슬라이드 조직병리학 영상에 대한 종양 감지 모델(패치 분류 기준)을 교육하고 평가하는 방법을 보여줍니다.

Profiling Whole Slide Tumor Detection

이 예에서는 MONAI NVTX변환을 사용하여 디지털 병리학 전체 슬라이드 종양 감지 파이프라인에서 사전 및 사후 처리 변환을 태그하고 프로파일링하는 방법을 보여준다.

#### 가속
fast_model_training_guide

이 문서에서는 교육 파이프라인을 프로파일링하는 방법, 데이터 세트를 분석하고 적합한 알고리즘을 선택하는 방법, 단일 GPU, 다중 GPU, 또는 멀티노드에서 GPU 활용도를 최적화하는 방법에 대한 세부 정보를 소개한다.

distributed_training

이 예에서는 세 가지 다른 프레임워크를 기반으로 분산 교육 및 평가를 실행하는 방법을 보여줍니다.
-	Torch.distributed.launch를 사용하는 PyTorch native DistributedDataParallel 모듈.
-	Horovodrun이 포함된 Horovod API입니다.
-	PyTorch Ignite 및 MONAI 워크플로우.
각 노드의 여러 GPU 디바이스가 있는 여러 분산 노드에서 실행할 수 있습니다.

automatic_mixed_precision

또한 AMP를 사용한 경우와 사용하지 않은 경우의 교육 속도와 메모리 사용량을 비교합니다.

dataset_type_performance

이 메모는 Dataset, CacheDataset and PersistentDataset의 성능을 비교합니다. 이러한 클래스는 데이터가 메모리 또는 디스크에 저장되는 방법과 변환이 적용되는 순간에 따라 다릅니다.

fast_training_tutorial

이 튜토리얼은 NVIDIA GPU 장치와 최신 CUDA 라이브러리를 기반으로 MONAI에서 순수 PyTorch 프로그램과 최적화된 프로그램의 훈련 성능을 비교한다. 최적화 방법에는 주로 AMP, CacheDataset 및 Novograd가 포함됩니다.

multi_gpu_test

이 메모는 장치에 대한 간단한 데모로 CPU, GPU 및 여러 GPU에서 Ignite 트레이너 엔진을 실행합니다.

threadbuffer_performance

별도의 스레드에서 교육 중에 데이터 배치를 생성하는 데 사용되는 ThreadBuffer 클래스의 사용을 시연합니다.

transform_speed

서로 다른 장치에서 서로 다른 변환의 NIFTI 파일 읽기 및 테스트 속도를 설명합니다.

#### modules
engines

엔진, 이벤트 핸들러 및 사후 변환이 포함된 MONAI 워크플로우가 있는 UNet3D 및 합성 데이터 세트를 기반으로 한 3D 분할의 교육 및 평가 예제. 그리고 의료 이미지 생성의 적대 네트워크에 대한 GAN 훈련 및 평가 예제. 간편 실행 교육 스크립트는 GanTrainer를 사용하여 2D CT 스캔 재구성 네트워크를 교육합니다. 평가 스크립트는 훈련된 네트워크에서 랜덤 샘플을 생성합니다.
예제는 주로 훈련자/평가자, 핸들러, post_transforms 등을 포함하는 MOANI 워크플로우로 작성됩니다.

3d_image_transforms

이 노트북은 체적 이미지에 대한 변환을 보여줍니다.

autoencoder_mednist

이 튜토리얼에서는 MedNIST hand CT 스캔 데이터 세트를 사용하여 MONAI의 자동 인코더 클래스를 시연한다. 자동 인코더는 ID encode/decode(즉, 다시 사용해야 하는 항목)와 함께 사용되며, 흐릿함 제거 및 노이즈 제거에 대한 사용법을 보여줍니다.

batch_output_transform

MONAI 엔진에서 작동하도록 핸들러의 batch_transform 및 output_transform을 설정하는 방법을 설명하고 보여준다.

compute_metric

예에서는 PyTorch 다중 처리 지원을 통해 저장된 예측 및 레이블에서 메트릭스를 계산하는 방법을 보여줍니다.

csv_datasets

튜토리얼에서는 CSVDataset 및 CSVIterableDataset의 사용을 보여주고, 여러 CSV 파일을 로드하고, 후 처리 로직을 실행합니다.

decollate_batch

튜토리얼에서는 batch 데이터를 분류 해제하여 사후 처리 변환을 단순화하고 다음 작업을 보다 유연하게 실행하는 방법을 보여줍니다.

image_dataset

이 메모에는 monai.data.ImageDataset 모듈의 기본 용도가 소개되어 있습니다.

dynunet_tutorial

이 튜토리얼은 MONAI에서 dynUNet을 다시 구현하여 10종 경기 데이터 세트에 대한 3D 분할 작업을 교육하는 방법을 보여줍니다.

integrate_3rd_party_transforms

이 튜토리얼은 타사 변환을 MONAI 프로그램에 통합하는 방법을 보여줍니다. 주로 BatchGenerator, TorchIO, Rising 및 ITK의 변환을 보여줍니다.

inverse transformations and test-time augmentations

이 메모는 역변환의 사용을 설명한 다음 역변환을 활용하여 테스트 시간 증대를 수행하는 방법을 보여줍니다.

layer wise learning rate

이 메모는 예상되는 네트워크 계층을 선택하거나 필터링하고 사용자 정의된 학습 속도 값을 설정하는 방법을 보여줍니다.

learning rate finder

이 메모는 LearningRateFinder API를 사용하여 네트워크의 학습 속도 값을 조정하는 방법을 보여줍니다.

load_medical_imagesl

이 메모는 MONAI에서 다양한 형식의 의료 이미지를 쉽게 로드하고 많은 추가 작업을 실행하는 방법을 소개합니다.

mednist_GAN_tutorial

이 메모는 랜덤 입력 텐서에서 이미지를 생성하기 위해 네트워크를 훈련하기 위해 MONAI의 사용을 설명한다. 별도의 생성기 및 판별기 네트워크와 함께 하기위해 간단한 GAN이 사용된다.

mednist_GAN_workflow_dict

이 메모는 모듈화된 적대적 학습을 위한 MOANI 워크플로우 엔진인 GanTrainer를 보여준다. MedNIST hand CT 스캔 데이터 세트를 사용하여 의료 영상 재구성 네트워크를 교육합니다. 사전 버전입니다.

mednist_GAN_workflow_array

이 메모는 모듈화된 적대적 학습을 위한 MOANI 워크플로우 엔진인 GanTrainer를 보여준다. MedNIST hand CT 스캔 데이터 세트를 사용하여 의료 영상 재구성 네트워크를 교육합니다. 배열 버전입니다.

cross_validation_models_ensemble

이 튜토리얼은 MONAI의 CrossValidation, Ensemble, MeanEnsemble 및 VoteEnsemble 모듈을 활용하여 교차 검증 및 앙상블 프로그램을 설정하는 방법을 보여준다.

nifti_read_example

NIFTI 파일을 읽고 해당 파일에서 로드 된 볼륨의 이미지 패치를 통해 반복하는 것을 보여줍니다.

network_api

이 튜토리얼에서는 유연한 네트워크 API 및 유틸리티를 설명합니다.

postprocessing_transforms

이 메모는 spleen 분할 작업의 모델 출력을 기반으로 한 몇 가지 후 처리 변환의 사용법을 보여줍니다.

public_datasets

이 메모는 MedNistDataset 및 DecathlonDataset을 기반으로 교육 워크플로우를 신속하게 설정하는 방법과 새 데이터 세트를 만드는 방법을 보여줍니다.

tcia_csv_processing

이 메모는 CSV 파일에서 CSVDataset을 사용하여 TCIA 데이터를 로드하고 TCIA 데이터에 대한 정보를 추출하여 REST API를 기반으로 DICOM 이미지를 가져오는 방법을 보여줍니다.

transforms_demo_2d

이 노트북은 GlaS 콘테스트 데이터 세트를 사용한 조직학 이미지의 이미지 변환을 보여줍니다.

UNet_input_size_constrains

이 튜토리얼은 MONAI UNet에 대한 입력 데이터의 합리적인 공간 크기를 결정하는 방법을 보여준다. 이 튜토리얼은 잔류 단위를 지원할 뿐만 아니라 기본 UNet 구현보다 더 많은 하이퍼 파라미터(예: stroads, kernel_size 및 up_kernel_size)를 사용할 수 있다.

TorchIO, MONAI, PyTorch Lightning

이 메모는 공식 PyTorch 생태계의 세 도서관이 어떻게 의학 분할 10종 경기의 뇌 MRI에 해마를 분할하는 데 함께 사용될 수 있는지 보여줍니다.

varautoencoder_mednist

이 튜토리얼에서는 MedNIST 스캔(또는 MNIST) 데이터 세트를 사용하여 MOANI의 가변 자동 인코더 클래스를 시연합니다.

interpretability

이 폴더의 자습서는 MONAI의 모델 시각화 및 해석 기능을 보여줍니다. 현재는 3D 분류 모델 시각화 및 분석을 위한 등급 활성화 매핑과 폐색 민감도로 구성되어 있습니다.

Transfer learning with MMAR

이 튜토리얼은 Clara Train의 의료 모델 아카이브 형식의 사전 교육된 모델로부터의 전송 학습 파이프라인을 보여준다. 노트북에는 LMDB 기반 데이터 세트의 사용도 나와 있습니다.

