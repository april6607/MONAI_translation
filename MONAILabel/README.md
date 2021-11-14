# MONAI Label

[![License](https://img.shields.io/badge/license-Apache%202.0-green.svg)](https://opensource.org/licenses/Apache-2.0)
[![CI Build](https://github.com/Project-MONAI/MONAILabel/workflows/build/badge.svg?branch=main)](https://github.com/Project-MONAI/MONAILabel/commits/main)
[![Documentation Status](https://readthedocs.org/projects/monailabel/badge/?version=latest)](https://docs.monai.io/projects/label/en/latest/?badge=latest)
[![codecov](https://codecov.io/gh/Project-MONAI/MONAILabel/branch/main/graph/badge.svg)](https://codecov.io/gh/Project-MONAI/MONAILabel)
[![PyPI version](https://badge.fury.io/py/monailabel.svg)](https://badge.fury.io/py/monailabel)

MONAI Label은 AI를 사용하여 양방향 의료 이미지 주석을 용이하게 하는 서버-클라이언트 시스템입니다. 오픈소스이며, 단일 GPU 또는 여러 GPU가 있는 시스템에서 로컬로 실행할 수 있는 간편한 에코 시스템입니다. 서버와 클라이언트는 모두 동일한/다른 컴퓨터에서 작동합니다. MONAI Label은 [MONAI](https://github.com/Project-MONAI))와 같은 원칙을 공유합니다.

[MONAI Label Demo](https://youtu.be/o8HipCgSZIw?t=1319)

![DEMO](https://raw.githubusercontent.com/Project-MONAI/MONAILabel/main/docs/images/demo.png)

## 특징

> _코드베이스는 현재 개발 중입니다._

- AI 모델을 교육하고 유추하기 위해 MONAI 라벨 앱을 개발하고 배포하는 프레임워크
- 기존 워크플로우에서의 간편한 통합을 위한 구성 및 휴대용 API
- 다양한 사용자 전문성을 위한 맞춤형 라벨링 앱 설계
- 3DSLicer 및 OHIF를 통한 주석 지원 
- DICOMWeb을 통한 PACS 연결

## 설치

MONAI Label은 **GPU/CUDA**가 가능한 다음 OS에서 지원합니다.

- Ubuntu
- [Windows](https://docs.monai.io/projects/label/en/latest/installation.html#windows)

[현재 릴리스](https://pypi.org/project/monailabel/)를 설치하려면 다음을 실행하면 됩니다.

```bash
  pip install monailabel
  
  # 샘플 앱/데이터셋 다운로드
  monailabel apps --download --name deepedit --output apps
  monailabel datasets --download --name Task09_Spleen --output datasets
  
  # 서버 실행
  monailabel start_server --app apps/deepedit --studies datasets/Task09_Spleen/imagesTr
```

> monailabel 설치 경로가 자동으로 결정되지 않으면 다음과 같이 명시적 설치 경로를 제공할 수 있습니다. 
> 
> `monailabel apps --prefix ~/.local`

**_전제조건_**, 기타 설치 방법(기본 GitHub branch 사용, Docker 사용 등)은 [설치 가이드](https://docs.monai.io/projects/label/en/latest/installation.html)을 참조하십시오.

> 일단 MONAI Label Server를 시작하면, 기본적으로 서버는 http://127.0.0.1:8000/. 에서 작동됩니다. 브라우저에서 서비스 URL을 열면 사용 가능한 Rest API 목록이 제공됩니다.

### 3D 슬라이서

https://download.slicer.org/ 에서 Preview Release를 다운로드하고 Slicer Extension Manager에서 MONAI Label 플러그인을 설치합니다.

3D Slicer에서 MONAI Label 플러그인을 설치 및 실행하기 위한 다른 옵션은 [3D Slicer 플러그인](플러그인/슬라이서)을 참조하십시오.
> 이전 버전의 Slicer를 실수로 사용하지 않으려면 이전에 설치한 3D Slicer 패키지를 _제거_ 하는 것이 좋습니다.

### OHIF

MONAI 레이블에는 [OHIF Viewer](https://github.com/OHIF/Viewers)용 [사전 빌드 플러그인](plugins/ohif)이 함께 제공됩니다.  OHIF Viewer를 사용하려면 서버를 시작할 때 FileSystem 대신 DICOMWeb을 _studies_로 제공해야 합니다.
> OHIF Viewer를 사용하기 전에 [Orthanc](https://www.orthanc-server.com/download.php)을 설치하십시오. Ubuntu 20.x의 경우 Orthanc을 `apt-get install orthanc orthanc-dicomweb`으로 설치할 수 있습니다. 그러나 [여기](https://book.orthanc-server.com/users/debian-packages.html#replacing-the-package-from-the-service-by-the-lsb-binaries)에서 언급한 단계를 수행하여 **최신 버전으로 업그레이드**해야 합니다.
>
> [PlastiMatch](https://plastimatch.org/plastimatch.html#plastimatch-convert)를 사용하여 NIFTI를 DICOM으로 변환할 수 있습니다.

```bash
  # DICOMWeb을 사용하여 서버 시작
  monailabel start_server --app apps\deepedit --studies http://127.0.0.1:8042/dicom-web
```
> OHIF 뷰어는 http://127.0.0.1:8000/ohif 에서 액세스할 수 있습니다.

![OHIF](https://raw.githubusercontent.com/Project-MONAI/MONAILabel/main/docs/images/ohif.png)

> **_참고:_** OHIF는 DeepEdit에 대한 스크리블 기반 주석 및 다중 라벨 상호 작용을 아직 지원하지 않습니다.

## 기여

MONAI 라벨에 대한 기여 지침은 [기여 지침](CONTRIBUTING.md)을 참조하십시오.

## 커뮤니티
트위터[@ProjectMONAI](https://twitter.com/ProjectMONAI)에서 대화에 참여하거나 [Slack 채널](https://forms.gle/QTxJq3hFictp31UM9)에 참여하십시오.

질문하고 질문에 답합니다.
[MONAI Label's GitHub Discussions tab](https://github.com/Project-MONAI/MONAILabel/discussions)에서 질문하고 답변하세요.

## 링크

- 웹사이트: https://monai.io/
- API 설명서: https://docs.monai.io/projects/label
- 코드: https://github.com/Project-MONAI/MONAILabel
- 프로젝트 트래커: https://github.com/Project-MONAI/MONAILabel/projects
- 이슈 트래커: https://github.com/Project-MONAI/MONAILabel/issues
- 위키: https://github.com/Project-MONAI/MONAILabel/wiki
- 테스트 현황: https://github.com/Project-MONAI/MONAILabel/actions
- PyPI 패키지: https://pypi.org/project/monailabel/
- 주간 예고: https://pypi.org/project/monailabel-weekly/
- Docker 허브: https://hub.docker.com/r/projectmonai/monailabel
