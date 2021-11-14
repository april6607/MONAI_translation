- [소개](#소개)
- [기여과정](#기여과정)
  * [작업 서명](#작업-서명)

## 소개

MONAILabel 프로젝트에 오신 것을 환영합니다! 당신이 여기 와서 기여하고 싶어한다는 것에 감사를 표합니다. 본 문서는 MONAILabel에 기여하고자 하는 개인 및 기관을 대상으로 합니다. MONAILabel은 오픈 소스 프로젝트이며, 따라서 그 성공은 계속 개선하고자 하는 기여자들의 커뮤니티에 달려 있습니다. 귀하의 기여는 코드 베이스에 가치가 있는 추가가 될 것입니다. 우리는 노련한 오픈 소스 기여자이든 또는 처음 기여자이든 간에 이 페이지를 읽고 우리의 기여 과정을 이해하기를 요청합니다.

### 우리와 소통하세요

MONAILabel에 대한 니즈와 프로젝트에 기여하기 위한 아이디어에 대해 이야기하게 되어 기쁩니다. 이렇게 하는 한 가지 방법은 여러분의 생각을 토론하기 위한 이슈를 만드는 것입니다. 매우 유사한 기능이 개발 중이거나 이미 존재하기 때문에 이슈가 좋은 출발점일 수 있습니다. MONAILabel 프로젝트에 도움이 될 만한 문제를 찾고 있는 경우 [*이슈*](https://github.com/Project-MONAI/MONAILabel/labels/good%20first%20issue) 및 [*기여*](https://github.com/Project-MONAI/MONAILabel/labels/Contribution%20wanted) 라벨들을 참조하십시오.

## 기여과정

>진행 중입니다.  더 많은 지시를 따르기 위해 기다려 주십시오.

  - 풀 요청서를 제출하기 전에 기본 CI 검사가 통과되었는지 확인합니다.
    ```
    ./runtests.sh --codeformat
    ./runtests.sh --unittests
    ```

### 작업 서명
MONAILabel은 모든 풀 요청에 대해 [개발자 원천 증명](https://developercertificate.org/)(DCO)을 적용합니다.
모든 커밋 메시지에는 이메일 주소가 있는 ‘Signed-off-by’줄이 포함되어야 합니다. [GitHub DCO APPS](https://github.com/apps/dco)은 MONAILabel에 구축되어 있습니다. 커밋에 유효한 ‘Signed-off-by’ 줄이 없을 경우 풀 요청의 상태는 'Failed' 상태가 됩니다.

Git에는 커밋 메시지에 자동으로 추가할 수 있는 '-s'(또는 '-signoff') 명령줄 옵션이 있습니다.
```bash
git commit -s -m 'a new commit'
```
커밋 메시지는 다음과 같습니다: 
```
    a new commit

    Signed-off-by: Your Name <yourname@example.org>
```
DCO 전체 텍스트:
```
개발자 원천 증명
Version 1.1

Copyright (C) 2004, 2006 The Linux Foundation and its contributors.
1 Letterman Drive
Suite D4700
San Francisco, CA, 94129

모든 사용자는 이 라이센스 문서의 실제 사본을 복사하여 배포할 수 있지만 변경할 수는 없습니다.


개발자 원천 증명 1.1

본인은 이 프로젝트에 기여함으로써 다음을 보증합니다.

(a) 기여의 전부 또는 일부를 본인에 의해 작성되었으며, 파일에 표시된 오픈 소스 라이센스에 따라 제출할 권리가 있습니다. 또는

(b) 기여는 제가 아는 한, 적절한 오픈 소스 라이센스에 의거한 이전 작업에 근거하며, 해당 라이센스에 의거해(다른 라이센스로 제출할 수
    없는 경우), 파일에 표시된 것과 같이, 본인에 의해 전체 또는 일부가 작성되었든 상관없이, 해당 라이센스에 의거해 해당 작업을
    수정할 수 있는 권한이 있습니다. 또는

(c) 기여는 (a), (b) 또는 (c)를 인증한 다른 사람에 의해 직접 제공되었으며 나는 이를 수정하지 않았습니다.

(d) 본 프로젝트와 기여는 공개되며 기여에 대한 기록(승인서를 포함하여 제출하는 모든 개인 정보 포함)이 무기한 유지되며 본 프로젝트
    또는 관련 오픈 소스 라이센스와 일치하도록 재배포될 수 있다는 것을 이해하고 동의합니다.
```
