## 성능 최적화 및 GPU 가속화

일반적으로 모델 훈련은 딥러닝 개발 중 특히 의료 영상 애플리케이션에서 시간이 많이 걸리는 단계이다. 체적 의료 영상은 일반적으로 크고(다차원 배열처럼) 모델 훈련 과정이 복잡할 수 있다. 강력한 하드웨어(ex: 대형 RAM이 장착된 CPU/GPU)를 사용하더라도 고성능을 달성하기 위해 완벽하게 활용하기는 쉽지 않습니다. NVIDIA GPU는 딥러닝 훈련 및 평가의 많은 영역에 광범위하게 적용되었으며, CUDA 병렬 연산은 기존 계산 방법과 비교할 때 분명한 가속도를 보여준다. GPU 기능을 최대한 활용하기 위해 자동 혼합 정밀도(AMP), 병렬 분산 데이터 등과 같은 널리 사용되는 많은 메커니즘이 이러한 기능을 지원할 수 있으며, 이 폴더는 최상의 성능과 풍부한 예를 달성하기 위한 빠른 교육 가이드를 제공한다.

#### 노트북 및 예제 목록

[fast_model_training_guide](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/fast_model_training_guide.md)

이 문서에서는 교육 파이프라인을 프로파일링하는 방법, 데이터 세트를 분석하고 적절한 알고리즘을 선택하는 방법, 단일 GPU, 다중 GPU 또는 다중 노드에서 GPU 활용도를 최적화하는 바업에 대한 세부 사항을 소개한다.

[distributed_training](https://github.com/Project-MONAI/tutorials/tree/master/acceleration/distributed_training)

다음은 3가지 다른 프레임워크를 기반으로 분산 교육 및 평가를 실행하는 방법을 보여주는 예입니다.
-	`torch.distributed.launch`의 PyTorch 기반 `DistributedDataParallel` 모듈입니다.
-	`Horovodrun`가 있는 Horovod API
-	PyTorch ignite와 MONAI 워크플로우

각 노드에 여러 GPU 장치가 있는 여러 분산 노드에서 실행할 수 있습니다.

[automatic_mixed_precision](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/automatic_mixed_precision.ipynb)

AMP를 사용하거나 사용하지 않는 훈련 속도와 메모리 사용량을 비교합니다.

[dataset_type_performance](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/dataset_type_performance.ipynb)

이 노트북은 Dataset, CacheDataset 및 PersistentDataset의 성능을 비교합니다. 이러한 클래스는 데이터가 저장되는 방식(메모리 또는 디스크에)과 변환이 적용되는 시점에 따라 다릅니다.

[fast_training_tutorial](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/fast_training_tutorial.ipynb)

이 튜토리얼은 NVIDIA GPU 장치와 최신 CUDA 라이브러리 기반으로 MONAAI에서 순수 PyTorch 프로그램과 최적화된 프로그램의 교육 성능을 비교한다. 최적화 방법에는 주로 AMP, CacheDataset 및 Novograd가 포함된다.

[multi_gpu_test](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/multi_gpu_test.ipynb)

이 노트북은 CPU, GPU 및 여러 GPU에서 Ignite 트레이너 엔진을 구동하는 장치용 빠른 데모입니다.

[threadbuffer_performance](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/threadbuffer_performance.ipynb)

별도의 스레드에서 학습하는 동안 데이터 배치를 생성하는데 사용되는 ThreadBuffer 클래스의 사용을 보여줍니다.

[transform_speed](https://github.com/Project-MONAI/tutorials/blob/master/acceleration/transform_speed.ipynb)

여러 장치에서 NIfTI 파일을 읽고 다양한 변환의 테스트 속도를 보여줍니다.
