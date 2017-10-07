---
title: "Azure에서 Jenkins 서버 aaaCreate"
description: "Jenkins hello Jenkins 솔루션 템플릿에서 Azure Linux 가상 컴퓨터에 설치 하 고 샘플 Java 응용 프로그램을 빌드하십시오."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Jenkins 서버 hello Azure 포털에서에서 Azure Linux VM에서 만들기

이 퀵 스타트의 표시 방법을 tooinstall [Jenkins](https://jenkins.io) azure hello 도구와 구성 된 플러그 인 toowork Ubuntu Linux VM에서 합니다. 작업을 완료하면 Azure에서 실행되는 Jenkins 서버가 [GitHub](https://github.com)에서 샘플 Java 앱을 작성합니다.

## <a name="prerequisites"></a>필수 조건

* Azure 구독
* 컴퓨터의 명령줄에 대 한 액세스 tooSSH (hello 예: Bash 셸은 또는 [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Hello 솔루션 템플릿에서 hello Jenkins VM 만들기

열기 hello [마켓플레이스 이미지를 Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) 에서 웹 브라우저를 선택 **GET IT 이제** hello hello 페이지의 왼쪽에서 합니다. 가격 책정 세부 정보 및 선택 검토 hello **계속**을 선택한 후 **만들기** tooconfigure hello Jenkins 서버 hello Azure 포털에에서 있습니다. 
   
![Azure Portal 대화 상자](./media/install-jenkins-solution-template/ap-create.png)

Hello에 **기본 설정을 구성** 탭 hello 필드 뒤에 입력 합니다.

![기본 설정 구성](./media/install-jenkins-solution-template/ap-basic.png)

* **이름**에 **Jenkins**를 사용합니다.
* **사용자 이름**을 입력합니다. 사용자 이름은 hello 만족 해야 합니다 [특정 요구 사항](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm)합니다.
* 선택 **암호** hello로 **인증 유형을** 고 암호를 입력 합니다. hello 암호는 대문자, 숫자 및 특수 문자를 하나 포함 해야 합니다.
* 사용 하 여 **myJenkinsResourceGroup** hello에 대 한 **리소스 그룹**합니다.
* Hello 선택 **미국 동부** [Azure 지역](https://azure.microsoft.com/regions/) hello에서 **위치** 드롭 다운 합니다.

선택 **확인** tooproceed toohello **추가 옵션을 구성** 탭 합니다. 고유한 도메인 이름을 tooidentify hello Jenkins 서버를 입력 하 고 선택 **확인**합니다.

![추가 옵션 설정](./media/install-jenkins-solution-template/ap-addtional.png)  

 유효성 검사에 통과 되 면 선택 **확인** hello에서 다시 **요약** 탭 합니다. 마지막으로 선택 **구매** toocreate hello Jenkins VM입니다. 서버에 준비 되 면 알림을 받게 hello Azure 포털에서:   

![Jenkins는 준비 알림임](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>TooJenkins 연결

웹 브라우저에서 tooyour 가상 컴퓨터 (예를 들어 http://jenkins2517454.eastus.cloudapp.azure.com/)를 이동 합니다. SSH 터널을 사용 하 여 컴퓨터에서 안전 하 게 hello 페이지 tooaccess hello Jenkins 콘솔에 설명 되어 있으므로 hello Jenkins 콘솔을 보안 되지 않은 HTTP를 통해 액세스할 수 없습니다.

![Jenkins 잠금 해제](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Hello를 사용 하 여 hello 터널 설정 `ssh` hello 페이지 hello 명령줄에서 명령을 교체 `username` hello 솔루션 템플릿에서 hello 가상 컴퓨터를 설정 하는 경우 이전에 선택한 hello 가상 컴퓨터 관리자 사용자의 hello 이름의 합니다.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Hello 터널 시작 된 후 이동 toohttp://localhost:8080 / 로컬 컴퓨터에 있습니다. 

Hello 다음 SSH toohello Jenkins VM을 통해 연결 되어 있는 동안 hello 명령줄에서 명령을 실행 하 여 hello 초기 암호를 가져옵니다.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

이 초기 암호를 사용 하 여 처음 hello에 대 한 hello Jenkins 대시보드를 잠금 해제 합니다.

![Jenkins 잠금 해제](./media/install-jenkins-solution-template/jenkins-unlock.png)

선택 **제안 된 플러그 인 설치** hello에서 다음 페이지 하 고 다음 Jenkins 관리자 사용 되는 사용자 tooaccess hello Jenkins 대시보드를 만듭니다.

![Jenkins가 준비되었습니다.](./media/install-jenkins-solution-template/jenkins-welcome.png)

Jenkins 서버 hello 준비 toobuild 코드 되었습니다.

## <a name="create-your-first-job"></a>첫 번째 작업 만들기

선택 **새 작업을 만들** hello Jenkins 콘솔에서 다음 이름을 **mySampleApp** 선택 **Freestyle 프로젝트**을 선택한 후 **확인**합니다.

![새 작업 만들기](./media/install-jenkins-solution-template/jenkins-new-job.png) 

선택 hello **소스 코드 관리** 탭을 사용 하도록 설정 **Git**, hello에 대 한 url을 입력 하 고 **리포지토리 URL** 필드:`https://github.com/spring-guides/gs-spring-boot.git`

![Hello Git 리포지토리를 정의 합니다.](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

선택 hello **빌드** 탭 한 다음 선택 **추가 빌드 단계**, **호출 Gradle 스크립트**합니다. **Gradle 래퍼 사용**을 선택한 후 **래퍼 위치**에 `complete`를 입력하고 **작업**에 `build`를 입력합니다.

![Gradle 래퍼 toobuild hello를 사용 하 여](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

**고급..**을 선택하고 다음을 입력 하 고 `complete` hello에 **루트 빌드 스크립트** 필드입니다. **저장**을 선택합니다.

![Hello Gradle 래퍼 빌드 단계에서 설정을 고급 설정](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Hello 코드 작성

선택 **이제 빌드** toocompile hello 코드와 패키지 hello 샘플 응용 프로그램입니다. 빌드가 완료 되 면 선택 hello **작업 영역** hello 프로젝트에 대 한 링크입니다.

![Hello 빌드에서 toohello 작업 영역 tooget hello JAR 파일 찾아보기](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

너무 이동`complete/build/libs` hello를 확인 하 고 `gs-spring-boot-0.1.0.jar` 거기 tooverify 프로그램 빌드에 성공 합니다. 서버는 이제 프로그램 Jenkins toobuild Azure에서 사용자의 프로젝트를 준비 합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Jenkins 에이전트로 Azure VM 추가](jenkins-azure-vm-agents.md)
