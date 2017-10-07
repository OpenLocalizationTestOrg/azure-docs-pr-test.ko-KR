---
title: "Azure 컨테이너 서비스 및 웜 aaaCI/CD | Microsoft Docs"
description: "Azure 컨테이너 서비스를 사용 하 여 docker는 Docker Swarm, Azure 컨테이너 레지스트리 및 Visual Studio Team Services toodeliver 지속적으로 다중 컨테이너.NET Core 응용 프로그램 사용"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로서비스, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>전체 CI/CD 파이프라인 toodeploy docker는 Docker Swarm Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램

중 하나 hello 난제 수 toodeliver hello 클라우드에 대 한 최신 응용 프로그램을 개발 중인 경우 이러한 응용 프로그램 지속적으로 합니다. 이 문서에서는 tooimplement 전체 연속 통합 및 배포 (CI/CD) 파이프라인 Azure 컨테이너 서비스를 사용 하 여 docker는 Docker Swarm, Azure 컨테이너 레지스트리 및 Visual Studio Team Services를 구축 하는 방법에 대해 알아봅니다 및 릴리스 관리 합니다.

이 문서는 간단한 응용 프로그램을 기반으로 [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs)에서 사용할 수 있으며 ASP.NET Core를 사용하여 전개됩니다. 네 개의 서로 다른 서비스로 구성 되어 있고 hello 응용 프로그램: 3 개 웹 Api 및 하나의 웹 프런트 엔드:

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

hello 목표는 toodeliver Visual Studio Team Services를 사용 하는 docker는 Docker Swarm 클러스터에서 지속적으로이 응용 프로그램입니다. hello 다음이 지속적인 업데이트 파이프라인 세부 정보를 그림:

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Hello 단계에 대 한 간략 한 설명은 다음과 같습니다.

1. 코드 변경 내용이 커밋된 toohello 소스 코드 리포지토리 (여기서 GitHub) 
2. GitHub은 Visual Studio Team Services에서 빌드를 트리거합니다. 
3. Visual Studio Team Services hello hello 소스의 최신 버전을 가져오고 hello 응용 프로그램을 구성 하는 모든 hello 이미지 작성 
4. Visual Studio Team Services 푸시 hello Azure 컨테이너 레지스트리 서비스를 사용 하 여 만든 각 이미지 tooa Docker 레지스트리 
5. Visual Studio Team Services는 새 릴리스를 트리거합니다. 
6. hello 릴리스 hello Azure 컨테이너 서비스 클러스터 노드에서 마스터 SSH를 사용 하 여 몇 가지 명령 실행 
7. Docker 웜 hello 클러스터 끌어오는 소스 hello 최신 버전의 hello 이미지 
8. Docker Compose를 사용 하 여 hello hello 응용 프로그램의 새 버전 배포 

## <a name="prerequisites"></a>필수 조건

이 자습서를 시작 하기 전에 다음 작업 toocomplete hello가 필요 합니다.

- [Azure 컨테이너 서비스에서 Swarm 클러스터 만들기](container-service-deployment.md)
- [컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결](../container-service-connect.md)
- [Azure 컨테이너 레지스트리 만들기](../../container-registry/container-registry-get-started-portal.md)
- [Visual Studio Team Services 계정 및 팀 프로젝트 만들기](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [포크 hello GitHub 리포지토리 tooyour GitHub 계정](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

또한 Docker를 설치한 Ubuntu 14.04 또는 16.04 컴퓨터가 필요합니다. 이 컴퓨터를 사용 하는 hello 하는 동안 Visual Studio Team Services에서 빌드 및 릴리스 프로세스입니다. 한 가지 방법은 toocreate이이 컴퓨터는 hello에서 사용할 수 있는 toouse hello 이미지 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/)합니다. 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>1단계: Visual Studio Team Services 계정 구성 

이 섹션에서는 사용자의 Visual Studio Team Services 계정을 구성합니다.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Visual Studio Team Services Linux 빌드 에이전트 구성

toocreate Docker 이미지와 Visual Studio Team Services에서 Azure 컨테이너 레지스트리에 이러한 이미지 빌드 푸시 tooregister Linux 에이전트를 해야 합니다. 다음과 같은 설치 옵션이 있습니다.

* [Linux에서 에이전트 배포](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Docker toorun hello VSTS 에이전트 사용](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Hello Docker 통합 VSTS 확장 설치

Microsoft는 빌드에 Docker가 있는 VSTS 확장 toowork를 제공 하 고 프로세스를 해제 합니다. 이 확장은 hello에서 사용할 수 있는 [VSTS 마켓플레이스](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)합니다. 클릭 **설치** tooadd이 확장 tooyour VSTS 계정:

![Hello Docker 통합 설치](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Tooconnect tooyour VSTS 계정 자격 증명을 사용 하는 단계가 있습니다. 

### <a name="connect-visual-studio-team-services-and-github"></a>Visual Studio Team Services 및 GitHub 연결

VSTS 프로젝트와 GitHub 계정 간에 연결을 설정합니다.

1. Visual Studio Team Services 프로젝트를 클릭 hello **설정** hello 도구 모음 및 선택 아이콘 **서비스**합니다.

    ![Visual Studio Team Services - 외부 연결](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Hello 왼쪽에서 클릭 **새 서비스 끝점** > **GitHub**합니다.

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. 클릭 하 여 GitHub 계정과 tooauthorize VSTS toowork **Authorize** hello 창이 열리면 hello 절차를 수행 합니다.

    ![Visual Studio Team Services - GitHub 인증](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>VSTS tooyour Azure 컨테이너 레지스트리 및 Azure 컨테이너 서비스 클러스터를 연결 합니다.

hello CI/CD 파이프라인에 도달 하기 전에 hello 마지막 단계는 tooconfigure 외부 연결 tooyour 컨테이너 레지스트리 및 Azure에서 docker는 Docker Swarm 클러스터입니다. 

1. Hello에 **서비스** 유형의 서비스 끝점을 추가 하는 Visual Studio Team Services 프로젝트의 설정을 **Docker 레지스트리**합니다. 

2. 열리면 hello 팝업에서 hello URL과 Azure 컨테이너 레지스트리 hello 자격 증명을 입력 합니다.

    ![Visual Studio Team Services - Docker 레지스트리](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Docker는 Docker Swarm 클러스터 hello에 대 한 형식의 끝점을 추가 **SSH**합니다. 웜 클러스터의 hello SSH 연결 정보를 입력 합니다.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

모든 hello 구성은 이제 수행 됩니다. Hello 다음 단계를 빌드 및 hello 응용 프로그램 toohello docker는 Docker Swarm 클러스터를 배포 하는 hello CI/CD 파이프라인을 만듭니다. 

## <a name="step-2-create-hello-build-definition"></a>2 단계: hello 빌드 정의 만들기

이 단계에서는 VSTS 프로젝트 빌드 definitionfor를 설정 하 고이 컨테이너 이미지에 대 한 hello 빌드 워크플로 정의 합니다.

### <a name="initial-definition-setup"></a>초기 정의 설정

1. 빌드 정의 toocreate 연결 tooyour Visual Studio Team Services 프로젝트 마우스 클릭 **빌드 및 릴리스**합니다. 

2. Hello에 **빌드 정의** 섹션에서 클릭 **+ 새로 만들기**합니다. 선택 hello **빈** 서식 파일입니다.

    ![Visual Studio Team Services - 새 빌드 정의](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. GitHub 리포지토리 소스, 확인을 사용 하 여 hello 새 빌드를 구성 **연속 통합**, 및 select hello 에이전트 큐 Linux 에이전트를 등록 합니다. 클릭 **만들기** toocreate hello 빌드 정의 합니다.

    ![Visual Studio Team Services - 빌드 정의 만들기](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Hello에 **빌드 정의** 페이지를 열면 hello **저장소** 탭 하 고 hello 필수 구성 요소에서 만든 hello MyShop 프로젝트의 빌드 toouse hello 포크 hello를 구성 합니다. 선택 해야 *acs docs* hello로 **기본 분기가**합니다.

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Hello에 **트리거** 탭 hello 빌드 toobe 각 커밋 후 트리거를 구성 합니다. **연속 통합** 및 **Batch 변경 내용**을 선택합니다.

    ![Visual Studio Team Services - 빌드 트리거 구성](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Hello 빌드 워크플로 정의 합니다.
다음 단계 hello hello 빌드 워크플로 정의 합니다. Hello에 대 한 컨테이너 이미지 toobuild 다섯 가지 *MyShop* 응용 프로그램입니다. 각 이미지 Dockerfile hello 프로젝트 폴더에 있는 hello를 사용 하 여 만들어집니다.

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

각 이미지에 대 한 두 Docker 단계 tooadd, 한 toobuild hello 이미지 및 hello Azure 컨테이너 레지스트리에 단일 toopush hello 이미지 필요 합니다. 

1. hello 빌드 워크플로에서 단계 tooadd 클릭 **+ 추가 빌드 단계** 선택 **Docker**합니다.

    ![Visual Studio Team Services - 빌드 단계 추가](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. 각 이미지에 대 한 hello를 사용 하 여 한 번 구성 `docker build` 명령입니다.

    ![Visual Studio Team Services - Docker 빌드](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Hello에 대 한 빌드 작업을 선택 하면 Azure 컨테이너 레지스트리 hello **이미지 빌드** 작업과 각 이미지를 정의 하는 Dockerfile hello 합니다. 집합 hello **빌드 컨텍스트에서** Dockerfile hello로 루트 디렉터리를 하 고 hello 정의 **이미지 이름**합니다. 
    
    Hello 화면을 앞에 표시 된 것과 같이 hello 이미지 이름 hello Azure 컨테이너 레지스트리의 URI로 시작 합니다. (사용할 수 있습니다도이 예에서 hello 빌드 식별자와 같은 hello 이미지의 빌드 변수 tooparameterize hello 태그.)

3. 각 이미지에 대 한 hello를 사용 하는 두 번째 단계를 구성 `docker push` 명령입니다.

    ![Visual Studio Team Services - Docker 푸시](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Hello 푸시 작업에 대 한 선택 사용자 Azure 컨테이너 레지스트리에 hello **이미지 푸시** 동작을 hello 입력 **이미지 이름** hello 이전 단계에서 만들어집니다.

4. Hello 빌드를 구성한 후 및 각 hello 5 이미지에 대 한 단계 push, hello에 두 개 이상의 단계 빌드 워크플로 추가 합니다.

    a. Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *BuildNumber* 현재 hello로 hello docker compose.yml 파일에 나타나는 빌드 id입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

    ![Visual Studio Team Services - 작성 파일 업데이트](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Hello를 삭제 하는 작업 hello 릴리스에서 사용할 수 있도록 작성 파일 빌드 아티팩트 업데이트. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

    ![Visual Studio Team Services - 작성 파일 게시](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. **저장**을 클릭하여 빌드 정의의 이름을 지정합니다.

## <a name="step-3-create-hello-release-definition"></a>3 단계: hello 릴리스 정의 만들기

Visual Studio Team Services 사용 하면 너무[릴리스를 관리 하는 환경에 걸쳐](https://www.visualstudio.com/team-services/release-management/)합니다. 연속 배포 toomake 부드러운 방식으로 하거나 다른 환경 (예: 개발, 테스트, 사전 프로덕션 및 프로덕션)에서 응용 프로그램은 배포를 사용할 수 있습니다. Azure Container Service Docker Swarm 클러스터를 나타내는 새 환경을 만들 수 있습니다.

![Visual Studio Team Services-릴리스 tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>최초 릴리스 설정

1. 릴리스 정의 toocreate 클릭 **릴리스** > **릴리스 +**

2. tooconfigure hello 아티팩트 소스 클릭 **아티팩트** > **아티팩트 소스 연결**합니다. 여기에서 hello 이전 단계에서 정의 된이 새 릴리스 정의 toohello 빌드에 연결 합니다. 이 작업을 수행 하 여 hello docker compose.yml 파일은 hello 릴리스 프로세스에서 사용할 수 있습니다.

    ![Visual Studio Team Services - 릴리스 아티팩트](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. tooconfigure hello 릴리스 트리거를 클릭 하 여 **트리거** 선택 **연속 배포**합니다. Hello에 hello 트리거 설정 같은 아티팩트 소스입니다. 이 설정은 새 릴리스 hello 빌드가 완료 되는 즉시 시작 되도록 보장 합니다.

    ![Visual Studio Team Services - 릴리스 트리거](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Hello 릴리스 워크플로 정의 합니다.

hello 릴리스 워크플로 추가 하는 두 가지 작업으로 구성 됩니다.

1. 작업 toosecurely 복사 hello 구성 파일 tooa 작성 *배포* hello docker는 Docker Swarm 마스터 노드를 이전에 구성한 hello SSH 연결을 사용 하는 폴더입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

    ![Visual Studio Team Services - 릴리스 SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. 두 번째 작업 tooexecute bash 명령 toorun 구성 `docker` 및 `docker-compose` hello 마스터 노드에서 명령입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

    ![Visual Studio Team Services - 릴리스 Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    hello 마스터 사용 하 여 hello Docker CLI 및 hello Docker Compose CLI toodo hello 작업 다음에 실행 된 hello 명령:

    - 로그인 toohello Azure 컨테이너 레지스트리 (사용 하 여 hello에 정의 된 세 개의 빌드 variab'les **변수** 탭)
    - Hello 정의 **DOCKER_HOST** hello 웜 끝점과 변수 toowork (: 2375)
    - Toohello 이동 *배포* hello docker compose.yml 파일을 포함 하 고 hello 안전한 복사 작업을 앞에서 만든 폴더 
    - 실행 `docker-compose` hello 새로운 이미지를 끌어오는 명령 hello 서비스를 중지, hello 서비스 제거 및 hello 컨테이너를 만듭니다.

    >[!IMPORTANT]
    > Hello 화면을 앞에 표시 된 대로 둡니다 hello **STDERR에서 실패** 확인란을 선택된 합니다. 중요 한 설정 때문에 이것이 `docker-compose` 컨테이너 중지 또는 삭제 하는 hello 표준 오류 출력에는 같은 여러 가지 진단 메시지를 인쇄 합니다. Hello 확인란을 선택 하면 Visual Studio Team Services를 보고 hello 릴리스 하는 동안 오류가 발생 했다는 코드가 정상적으로 작동 하는 경우에 합니다.
    >
3. 새 릴리스 정의를 저장합니다.


>[!NOTE]
>이 배포에는 hello 이전 서비스를 중지 하 고 새 hello를 실행 하기 때문에 일부 가동 중지 시간이 포함 됩니다. 것 입니까 가능한 tooavoid 청록색 배포를 수행 하 여 합니다.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>4단계. 테스트 hello CI/CD 파이프라인

이제 hello 구성 했으면입니다이 새로운 시간 tootest CI/CD 파이프라인. hello 가장 쉬운 방법은 tootest tooupdate hello 소스 코드 및 커밋 hello는 GitHub 리포지토리에으로 변경 합니다. 몇 초 후 hello 코드 푸시 Visual Studio Team Services에서 실행 되는 새 빌드를 볼 수 있습니다. 성공적으로 완료 되 면 새 릴리스 트리거됩니다 및 hello hello Azure 컨테이너 서비스 클러스터에서 hello 응용 프로그램의 새 버전을 배포 합니다.

## <a name="next-steps"></a>다음 단계

* Visual Studio Team Services를 통해 CI/CD에 대 한 자세한 내용은 참조 hello [VSTS 빌드 개요](https://www.visualstudio.com/docs/build/overview)합니다.
