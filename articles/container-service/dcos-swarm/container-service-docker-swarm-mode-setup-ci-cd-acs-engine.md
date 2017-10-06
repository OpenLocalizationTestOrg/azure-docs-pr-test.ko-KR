---
title: "Azure 컨테이너 서비스 엔진 및 Swarm 모드로 aaaCI/CD | Microsoft Docs"
description: "Azure 컨테이너 서비스 엔진을 사용 하 여 Docker Swarm 모드, Azure 컨테이너 레지스트리 및 Visual Studio Team Services toodeliver 지속적으로 다중 컨테이너.NET Core 응용 프로그램 사용"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, 컨테이너, 마이크로서비스, Swarm, Azure, Visual Studio Team Services, DevOps, ACS Engine"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>전체 CI/CD 파이프라인 toodeploy ACS 엔진 및 Docker Swarm 모드로 Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램

*이 문서는 기준 [전체 CI/CD 파이프라인 toodeploy docker는 Docker Swarm Visual Studio Team Services를 사용 하 여 Azure 컨테이너 서비스에서 여러 컨테이너 응용 프로그램](container-service-docker-swarm-setup-ci-cd.md) 설명서*

오늘날에 중 하나 hello 난제 수 toodeliver hello 클라우드에 대 한 최신 응용 프로그램을 개발 중인 경우 이러한 응용 프로그램 지속적으로 합니다. 이 문서에서는 어떻게 tooimplement 전체 연속 통합 및 배포 (CI/CD) 파이프라인 사용 하는 방법을 배웁니다. 
* Docker Swarm Mode의 Azure Container Service Engine
* Azure Container Registry
* Visual Studio Team Services

이 문서는 간단한 응용 프로그램을 기반으로 [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)에서 사용할 수 있으며 ASP.NET Core를 사용하여 전개됩니다. 네 개의 서로 다른 서비스로 구성 되어 있고 hello 응용 프로그램: 3 개 웹 Api 및 하나의 웹 프런트 엔드:

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

hello 목표는 toodeliver Visual Studio Team Services를 사용 하 여 Docker Swarm 모드 클러스터에서 지속적으로이 응용 프로그램입니다. hello 다음이 지속적인 업데이트 파이프라인 세부 정보를 그림:

![MyShop 샘플 응용 프로그램](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Hello 단계에 대 한 간략 한 설명은 다음과 같습니다.

1. 코드 변경 내용이 커밋된 toohello 소스 코드 리포지토리 (여기서 GitHub) 
2. GitHub은 Visual Studio Team Services에서 빌드를 트리거합니다. 
3. Visual Studio Team Services hello hello 소스의 최신 버전을 가져오고 hello 응용 프로그램을 구성 하는 모든 hello 이미지 작성 
4. Visual Studio Team Services 푸시 hello Azure 컨테이너 레지스트리 서비스를 사용 하 여 만든 각 이미지 tooa Docker 레지스트리 
5. Visual Studio Team Services는 새 릴리스를 트리거합니다. 
6. hello 릴리스 hello Azure 컨테이너 서비스 클러스터 노드에서 마스터 SSH를 사용 하 여 몇 가지 명령 실행 
7. Hello 클러스터에서 docker Swarm 모드 hello hello 이미지의 최신 버전을 가져오고 
8. Docker 스택을 사용 하 여 hello hello 응용 프로그램의 새 버전 배포 

## <a name="prerequisites"></a>필수 조건

이 자습서를 시작 하기 전에 다음 작업 toocomplete hello가 필요 합니다.

- [ACS Engine을 사용하여 Azure Container Service에서 Swarm Mode 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결](../container-service-connect.md)
- [Azure 컨테이너 레지스트리 만들기](../../container-registry/container-registry-get-started-portal.md)
- [Visual Studio Team Services 계정 및 팀 프로젝트 만들기](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [포크 hello GitHub 리포지토리 tooyour GitHub 계정](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> 컨테이너 서비스를 Azure의 hello docker는 Docker Swarm orchestrator 웜 레거시 독립 실행형을 사용합니다. 현재 hello 통합 [웜 모드](https://docs.docker.com/engine/swarm/) (Docker 1.12 및 더 높은) Azure 컨테이너 서비스에서 지원 되는 조정 자가 아닙니다. 이러한 이유로 사용 하 여 [ACS 엔진](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), 커뮤니티 제공 [퀵 스타트 템플릿](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), 또는 hello에 Docker 솔루션 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com)합니다.
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>1단계: Visual Studio Team Services 계정 구성 

이 섹션에서는 사용자의 Visual Studio Team Services 계정을 구성합니다. Visual Studio Team Services 프로젝트에서 tooconfigure VSTS 서비스 끝점을 클릭 하 여 hello **설정** hello 도구 모음 및 선택 아이콘 **서비스**합니다.

![서비스 끝점 열기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Visual Studio Team Services 및 Azure 계정 연결

VSTS 프로젝트와 Azure 계정 간에 연결을 설정합니다.

1. Hello 왼쪽에서 클릭 **새 서비스 끝점** > **Azure 리소스 관리자**합니다.
2. Azure 계정과 tooauthorize VSTS toowork 선택 프로그램 **구독** 클릭 **확인**합니다.

    ![Visual Studio Team Services - Azure 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Visual Studio Team Services 및 GitHub 연결

VSTS 프로젝트와 GitHub 계정 간에 연결을 설정합니다.

1. Hello 왼쪽에서 클릭 **새 서비스 끝점** > **GitHub**합니다.
2. 클릭 하 여 GitHub 계정과 tooauthorize VSTS toowork **Authorize** hello 창이 열리면 hello 절차를 수행 합니다.

    ![Visual Studio Team Services - GitHub 인증](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>VSTS tooyour Azure 컨테이너 서비스 클러스터에 연결

hello CI/CD 파이프라인에 도달 하기 전에 hello 마지막 단계 tooconfigure 외부 연결 tooyour docker는 Docker Swarm Azure 클러스터에에서 적용 됩니다. 

1. Docker는 Docker Swarm 클러스터 hello에 대 한 형식의 끝점을 추가 **SSH**합니다. 웜 클러스터 (마스터 노드)의 hello SSH 연결 정보를 입력 합니다.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

모든 hello 구성은 이제 수행 됩니다. Hello 다음 단계를 빌드 및 hello 응용 프로그램 toohello docker는 Docker Swarm 클러스터를 배포 하는 hello CI/CD 파이프라인을 만듭니다. 

## <a name="step-2-create-hello-build-definition"></a>2 단계: hello 빌드 정의 만들기

이 단계에서는 VSTS 프로젝트에 대 한 빌드 정의를 설정 하 고이 컨테이너 이미지에 대 한 hello 빌드 워크플로 정의 합니다.

### <a name="initial-definition-setup"></a>초기 정의 설정

1. 빌드 정의 toocreate 연결 tooyour Visual Studio Team Services 프로젝트 마우스 클릭 **빌드 및 릴리스**합니다. Hello에 **빌드 정의** 섹션에서 클릭 **+ 새로 만들기**합니다. 

    ![Visual Studio Team Services - 새 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. 선택 hello **빈 프로세스**합니다.

    ![Visual Studio Team Services - 새 빈 빌드 정의](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. 클릭 hello **변수** 탭 및 두 개의 새로운 변수를 만듭니다: **RegistryURL** 및 **AgentURL**합니다. 레지스트리 및 클러스터 에이전트 DNS hello 값을 붙여 넣습니다.

    ![Visual Studio Team Services - 빌드 변수 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Hello에 **빌드 정의** 페이지, 열기 hello **트리거** 탭 및 hello 필수 구성 요소에서 만든 hello MyShop 프로젝트의 분기 hello와 hello 빌드 toouse 연속 통합을 구성 합니다. 그런 다음 **일괄 처리 변경 사항**을 선택합니다. 선택 해야 *docker linux* hello로 **사양 분기**합니다.

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. 마지막 hello를 클릭 하 여 **옵션** 탭 하 고 hello 기본 에이전트 큐를 너무 구성**Linux 미리 보기 호스트**합니다.

    ![Visual Studio Team Services - 호스트 에이전트 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Hello 빌드 워크플로 정의 합니다.
다음 단계 hello hello 빌드 워크플로 정의 합니다. 먼저 hello 코드의 tooconfigure hello 소스입니다. toodo 선택 **GitHub** 하였고 **리포지토리** 및 **분기** (linux docker).

![Visual Studio Team Services - 코드 소스 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Hello에 대 한 컨테이너 이미지 toobuild 다섯 가지 *MyShop* 응용 프로그램입니다. 각 이미지 Dockerfile hello 프로젝트 폴더에 있는 hello를 사용 하 여 만들어집니다.

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

각 이미지에 대 한 두 Docker 단계, 한 toobuild hello 이미지 및 hello Azure 컨테이너 레지스트리에 toopush hello 이미지 하나 필요 합니다. 

1. hello 빌드 워크플로에서 단계 tooadd 클릭 **+ 추가 빌드 단계** 선택 **Docker**합니다.

    ![Visual Studio Team Services - 빌드 단계 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. 각 이미지에 대 한 hello를 사용 하 여 한 번 구성 `docker build` 명령입니다.

    ![Visual Studio Team Services - Docker 빌드](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Hello에 대 한 빌드 작업을 선택 하면 Azure 컨테이너 레지스트리 hello **이미지 빌드** 작업과 각 이미지를 정의 하는 Dockerfile hello 합니다. 집합 hello **작업 디렉터리** hello Dockerfile 루트 디렉터리로 hello 정의 **이미지 이름**을 선택 하 고 **최신 태그 포함**합니다.
    
    이미지 이름 hello이이 형식에 대 한 toobe: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```합니다. 대체 **[NAME]** hello 이미지 이름의:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. 각 이미지에 대 한 hello를 사용 하는 두 번째 단계를 구성 `docker push` 명령입니다.

    ![Visual Studio Team Services - Docker 푸시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Hello 푸시 작업에 대 한 선택 사용자 Azure 컨테이너 레지스트리에 hello **이미지 푸시** 동작을 hello 입력 **이미지 이름** hello 이전 단계를 선택에 기본 제공 되는 **최신 태그 포함** .

4. Hello 빌드를 구성한 후 및 각 hello 5 이미지에 대 한 단계 push, hello에 3 개 더 많은 단계가 빌드 워크플로 추가 합니다.

   ![Visual Studio Team Services - 명령줄 작업 추가](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *RegistryURL* hello RegistryURL 변수로 hello docker compose.yml 파일에서 발생 합니다. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - 레지스트리 URL로 작성 파일 업데이트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Bash 스크립트 tooreplace hello를 사용 하는 명령줄 작업 *AgentURL* hello AgentURL 변수로 hello docker compose.yml 파일에서 발생 합니다.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Hello를 삭제 하는 작업 hello 릴리스에서 사용할 수 있도록 작성 파일 빌드 아티팩트 업데이트. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

         ![Visual Studio Team Services - 아티팩트 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - 작성 파일 게시](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. 클릭 **저장 후 큐** tootest 빌드 정의 합니다.

   ![Visual Studio Team Services - 저장 및 큐에 넣기](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - 새 큐](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. 경우 hello **빌드** 올바른지, toosee이이 화면이 있어야 합니다.

  ![Visual Studio Team Services - 빌드 성공](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>3 단계: hello 릴리스 정의 만들기

Visual Studio Team Services 사용 하면 너무[릴리스를 관리 하는 환경에 걸쳐](https://www.visualstudio.com/team-services/release-management/)합니다. 연속 배포 toomake 부드러운 방식으로 하거나 다른 환경 (예: 개발, 테스트, 사전 프로덕션 및 프로덕션)에서 응용 프로그램은 배포를 사용할 수 있습니다. Azure Container Service Docker Swarm Mode 클러스터를 나타내는 환경을 만들 수 있습니다.

![Visual Studio Team Services-릴리스 tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>최초 릴리스 설정

1. 릴리스 정의 toocreate 클릭 **릴리스** > **릴리스 +**

2. tooconfigure hello 아티팩트 소스 클릭 **아티팩트** > **아티팩트 소스 연결**합니다. 여기에서 hello 이전 단계에서 정의 된이 새 릴리스 정의 toohello 빌드에 연결 합니다. 그 후 hello docker compose.yml 파일을 hello 릴리스 프로세스에서 사용할 수 있습니다.

    ![Visual Studio Team Services - 릴리스 아티팩트](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. tooconfigure hello 릴리스 트리거를 클릭 하 여 **트리거** 선택 **연속 배포**합니다. Hello에 hello 트리거 설정 같은 아티팩트 소스입니다. 이 설정은 새 릴리스 hello 빌드가 성공적으로 완료 될 때 시작 됨을 보장 합니다.

    ![Visual Studio Team Services - 릴리스 트리거](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. tooconfigure hello 릴리스 변수 클릭 **변수** 선택 **변수 +** toocreate hello 레지스트리 hello 정보 인 세 개의 새로운 변수: **docker.username**, **docker.password**, 및 **docker.registry**합니다. 레지스트리 및 클러스터 에이전트 DNS hello 값을 붙여 넣습니다.

    ![Visual Studio Team Services - 빌드 리포지토리 구성](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > 이전 hello 화면에 표시 된 것과 같이 hello 클릭 **잠금** docker.password 확인란을 선택 합니다. 이 설정은 중요 toorestrict hello 암호입니다.
    >

### <a name="define-hello-release-workflow"></a>Hello 릴리스 워크플로 정의 합니다.

hello 릴리스 워크플로 추가 하는 두 가지 작업으로 구성 됩니다.

1. 작업 toosecurely 복사 hello 구성 파일 tooa 작성 *배포* hello docker는 Docker Swarm 마스터 노드를 이전에 구성한 hello SSH 연결을 사용 하는 폴더입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.
    
    소스 폴더: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - 릴리스 SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. 두 번째 작업 tooexecute bash 명령 toorun 구성 `docker` 및 `docker stack deploy` hello 마스터 노드에서 명령입니다. Hello 화면 대 한 자세한 내용은 다음을 참조 하십시오.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - 릴리스 Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    hello 마스터에서 실행 하는 hello 명령은 Docker CLI hello 및 작업을 수행 하는 hello Docker Compose CLI toodo hello를 사용 합니다.

    - Azure 컨테이너 레지스트리 toohello 로그인 (hello에 정의 된 세 개의 빌드 변수를 사용 하 여 **변수** 탭)
    - Hello 정의 **DOCKER_HOST** hello 웜 끝점과 변수 toowork (: 2375)
    - Toohello 이동 *배포* hello docker compose.yml 파일을 포함 하 고 hello 안전한 복사 작업을 앞에서 만든 폴더 
    - 실행 `docker stack deploy` hello 컨테이너를 만들고 hello 새 이미지를 끌어오도록 하는 명령입니다.

    >[!IMPORTANT]
    > 이전 hello 화면에 표시 된 대로 둡니다 hello **STDERR에서 실패** 확인란을 선택된 합니다. 이 설정을 통해 인해 toocomplete hello 릴리스 프로세스 너무`docker-compose` 컨테이너 중지 또는 삭제 하는 hello 표준 오류 출력에는 같은 여러 가지 진단 메시지를 인쇄 합니다. Hello 확인란을 선택 하면 Visual Studio Team Services를 보고 hello 릴리스 하는 동안 오류가 발생 했다는 코드가 정상적으로 작동 하는 경우에 합니다.
    >
3. 새 릴리스 정의를 저장합니다.

## <a name="step-4-test-hello-cicd-pipeline"></a>4 단계: 테스트 hello CI/CD 파이프라인

이제 hello 구성 했으면입니다이 새로운 시간 tootest CI/CD 파이프라인. hello 가장 쉬운 방법은 tootest tooupdate hello 소스 코드 및 커밋 hello는 GitHub 리포지토리에으로 변경 합니다. 몇 초 후 hello 코드 푸시 Visual Studio Team Services에서 실행 되는 새 빌드를 볼 수 있습니다. 성공적으로 완료 되 면 새 릴리스 트리거되고 hello hello Azure 컨테이너 서비스 클러스터에서 hello 응용 프로그램의 새 버전을 배포 합니다.

## <a name="next-steps"></a>다음 단계

* Visual Studio Team Services를 통해 CI/CD에 대 한 자세한 내용은 참조 hello [VSTS 빌드 개요](https://www.visualstudio.com/docs/build/overview)합니다.
* ACS 엔진에 대 한 자세한 내용은 참조 hello [ACS 엔진 GitHub 리포지토리](https://github.com/Azure/acs-engine)합니다.
* Docker는 Docker Swarm 모드에 대 한 자세한 내용은 참조 hello [모드 개요 docker는 Docker Swarm](https://docs.docker.com/engine/swarm/)합니다.
