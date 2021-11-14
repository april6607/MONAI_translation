# 사용 가능한 MONAI 라벨 앱

### 개요

이 폴더에는 **3가지 사용 가능한 패러다임** - 두 가지 대화형(DeepGrow, DeepEdit)과 한 가지 자동 분할 - 의 예제가 있습니다.


#### DeepGrow

DeepGrow 패러다임의 경우 [좌심방 분할을 위한 DeepGrow](./deepgrow_left_atrium)와 [deepGrow App](./deepgrow)의 두 가지 경우가 있습니다. 후자는 DeepGrow 기반 앱을 구축하려는 사용자를 위한 것입니다.

#### DeepEdit

Deepgrow Apps와 유사하게, 연구원들이 DeepEdit 기반 앱을 만드는 데 사용할 수 있는 일반적인 [deepedit](.deepedit)를 찾을 수 있습니다.


### 자동 분할

DeepGrow 및 DeepEdit 앱으로서, 연구자들은 UNet을 사용하여 [./segmentation_splen](. segmentation_splen) 및 [left atrium](./segmentation_left_atrium)에 대한 비대화형 앱을 시도할 수 있습니다. 또한 연구원들이 복제하여 자신만의 앱을 만들 수 있는 일반적인 세분화 앱도 있습니다. 


이러한 앱의 더 많은 예는 [MONAI 라벨 앱스 동물원](https://github.com/diazandr3s/MONAILabel-Apps)에서 확인할 수 있습니다.
