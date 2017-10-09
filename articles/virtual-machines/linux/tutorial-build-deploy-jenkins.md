---
title: "Jenkins tooAzure Team Services를 통해 Vm에서에서 aaaCI/CD | Microsoft Docs"
description: "CI (연속 통합) 및 VSTS Visual Studio Team Services () 또는 Microsoft Team Foundation Server (TFS)에 Release Management에서 Jenkins tooAzure Vm을 사용 하 여 Node.js 응용 프로그램의 연속 배포 (CD) 설정"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>사용자 응용 프로그램 tooLinux Vm 배포 Jenkins 및 Team Services를 사용 하 여

CI(지속적인 통합) 및 CD(지속적인 배포)는 코드를 작성, 릴리스 및 배포하는 데 사용할 수 있는 파이프라인입니다. Team Services 배포 tooAzure에 대 한 완전 하 고 모든 기능을 갖춘 CI/CD 자동화 도구 집합이 제공 합니다. Jenkins는 널리 사용되고 있는 타사 CI/CD 서버 기반 도구이며, 마찬가지로 CI/CD 자동화 기능을 제공합니다. 모두 함께 toocustomize를 사용할 수 있습니다 어떻게 클라우드 앱 이나 서비스 발휘 합니다.

이 자습서를 사용 하 여 Jenkins toobuild는 **Node.js 웹 응용 프로그램**, 및 Visual Studio Team Services toodeploy 것 tooa [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux 가상 컴퓨터를 포함 하 합니다.

다음을 수행합니다.

> [!div class="checklist"]
> * Jenkins에서 앱 빌드
> * Team Services와 통합되도록 Jenkins 구성
> * Azure 가상 컴퓨터 hello에 대 한 배포 그룹 만들기
> * Hello Vm을 구성 하 고 hello 앱을 배포 하는 릴리스 정의 만들기

## <a name="before-you-begin"></a>시작하기 전에

* 액세스 tooa Jenkins 계정이 필요합니다. Jenkins 서버를 아직 만들지 않은 경우 [Jenkins 설명서](https://jenkins.io/doc/)를 참조하세요. 

* Tooyour Team Services 계정에에서 로그인 (`https://{youraccount}.visualstudio.com`). 
  [Team Services 계정은 무료](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)로 제공됩니다.

  > [!NOTE]
  > 자세한 내용은 참조 [tooTeam 서비스 연결](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)합니다.

* Team Services 계정에 PAT(개인용 액세스 토큰)가 아직 없으면 만듭니다. Jenkins는이 정보 tooaccess Team Services 계정이 필요합니다.
  읽기 [어떻게 만드나요 개인용 액세스 토큰을 Team Services 및 TFS 용](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn 어떻게 toogenerate 하나입니다.

## <a name="get-hello-sample-app"></a>Hello 샘플 응용 프로그램 가져오기

Git 리포지토리에 저장 하는 응용 프로그램 toodeploy가 필요 합니다.
이 자습서에서는 [GitHub에서 제공되는 이 샘플 앱](https://github.com/azooinmyluggage/fabrikam-node)을 사용하는 것이 좋습니다.

1. 이 앱의 분기를 만들고이 자습서의 이후 단계에서 사용 하기 위해 hello 위치 (URL)을 숙지 합니다.

1. Hello 포크 확인 **공용** toosimplify tooGitHub 나중에 다시 연결 합니다.

> [!NOTE]
> 자세한 내용은 [Fork a repo](https://help.github.com/articles/fork-a-repo/)(리포지토리 포크) 및 [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/)(비공개 리포지토리를 공개로 설정)을 참조하세요.

> [!NOTE]
> hello 앱을 사용 하 여 빌드된 [Yeoman](http://yeoman.io/learning/index.html); 사용 하 여 **Express**, **bower**, 및 **grunt**; 일부 있으며 **npm**종속성으로 패키지 합니다.
> hello 샘플 응용 프로그램 집합이 포함 되어 [Azure 리소스 관리자 템플릿을](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) 는 사용 되는 toodynamically 배포에 대 한 hello 가상 컴퓨터에서 만들 Azure입니다. 이러한 템플릿은 hello에 작업에 사용 되 [Team Services 릴리스 정의가](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)합니다.
> hello 주 템플릿은 네트워크 보안 그룹, 가상 컴퓨터 및 가상 네트워크를 만듭니다. 또한 공용 IP 주소를 할당하고 인바운드 포트 80을 엽니다. 또한 hello 배포 그룹 너무 선택 hello 컴퓨터 tooreceive hello 배포에서 사용 되는 태그를 추가 합니다.
>
> 또한 hello 샘플 Nginx를 설정 하 고 hello 앱을 배포 하는 스크립트를 포함 합니다. 각각의 hello 가상 컴퓨터에서 실행 됩니다. Hello 스크립트 노드, Nginx, 및; 오후 2를 설치 하는 구체적으로, Nginx 및 오후 2; 구성합니다. hello 노드 앱을 시작합니다.

## <a name="configure-jenkins-plugins"></a>Jenkins 플러그 인 구성

먼저 **NodeJS**용과 **Team Services와의 통합**용 Jenkins 플러그 인을 두 개 구성해야 합니다.

1. Jenkins 계정을 열고 **Manage Jenkins**(Jenkins 관리)를 선택합니다.

1. Hello에 **관리 Jenkins** 페이지에서 선택 **플러그 인 관리**합니다.

1. 필터 hello 목록 toolocate hello **NodeJS** 플러그 인 및 다시 시작 하지 않아도 설치 합니다.

   ![Hello NodeJS 플러그 인 tooJenkins 추가](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. 필터 hello 목록 toofind hello **Team Foundation Server** 플러그 인 하 고 설치 합니다. 이 플러그 인은 Team Foundation Server와 Team Services 둘 다에서 작동합니다. Jenkins를 다시 시작할 필요는 없습니다.

## <a name="configure-jenkins-build-for-nodejs"></a>Node.js용으로 Jenkins 빌드 구성

Jenkins에서 새 빌드 프로젝트를 만들고 다음과 같이 구성합니다.

1. Hello에 **일반** 탭에서 빌드 프로젝트에 대 한 이름을 입력 합니다.

1. Hello에 **소스 코드 관리** 탭에서 **Git** hello 저장소 및 응용 프로그램 코드를 포함 하는 hello 분기의 hello 세부 정보를 입력 합니다.

   ![리포지토리 tooyour 빌드 추가](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > 리포지토리에 public 인 경우 선택 **추가** tooconnect tooit 자격 증명을 제공 합니다.

1. Hello에 **빌드 트리거** 탭에서 **폴링 SCM** hello 일정을 입력 하 고 `H/03 * * * *` toopoll hello Git 리포지토리 3 분 마다 변경에 대 한 합니다. 

1. Hello에 **빌드 환경** 탭에서 **제공 노드 &amp; npm bin / 폴더 경로** 입력 `NodeJS` hello 노드 JS 설치 값에 대 한 합니다. **npmrc file**(npmrc 파일)은 "use system default"(시스템 기본값 사용) 상태로 유지합니다.

1. Hello에 **빌드** 탭을 hello 명령 입력 `npm install` tooensure 모든 종속 업데이트 됩니다.

## <a name="configure-jenkins-for-team-services-integration"></a>Team Services와 통합되도록 Jenkins 구성

1. Hello에 **빌드 후 작업** 탭에 대 한 **파일 tooarchive**, 입력 `**/*` tooinclude 모든 파일.

1. 에 대 한 **TFS/Team Services에서 릴리스 트리거**, 사용자의 계정 hello 전체 URL을 입력 (같은 `https://your-account-name.visualstudio.com`), 프로젝트 이름, (나중에 만들어진) hello 릴리스 정의 대 한 이름 hello 및 자격 증명 tooconnect tooyour 계정 hello 합니다.
   사용자 이름 및 hello 앞에서 만든 PAT 필요. 

   ![Jenkins 빌드 후 작업 구성](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Hello 빌드 프로젝트를 저장 합니다.

## <a name="create-a-jenkins-service-endpoint"></a>Jenkins 서비스 끝점 만들기

서비스 끝점에는 Team Services tooconnect tooJenkins 수 있습니다.

1. 열기 hello **서비스** 열기 hello Team Services의 페이지 **새 서비스 끝점** , 목록을 열고 **Jenkins**합니다.

   ![Jenkins 끝점 추가](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Toorefer toothis 연결을 사용할 이름을 입력 합니다.

1. Jenkins 서버 hello URL을 입력 하 고 hello 눈금 **신뢰할 수 없는 SSL 인증서를 수락** 옵션입니다.

1. Jenkins 계정에 대 한 hello 사용자 이름 및 암호를 입력 합니다.

1. 선택 **연결을 확인** 정보 hello toocheck 올바릅니다.

1. 선택 **확인** toocreate hello 서비스 끝점입니다.

## <a name="create-a-deployment-group"></a>배포 그룹 만들기

필요한는 [배포 그룹](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) 너무 hello 가상 컴퓨터를 포함 합니다.

1. 열기 hello **릴리스** hello 탭 **빌드 &amp; 릴리스** 허브 다음 열기 hello **배포 그룹** 탭을 선택한 **+ 새로 만들기**.

1. Hello 배포 그룹 및 선택적 설명을 대 한 이름을 입력 합니다.
   그런 다음 **만들기**를 선택합니다.

hello Azure 리소스 그룹 배포 작업이 만들고 hello Azure 리소스 관리자 템플릿을 사용 하 여 실행 될 때 hello Vm을 등록 합니다.
Toocreate 필요 하 고 직접 hello 가상 컴퓨터를 등록 하지 않습니다.

## <a name="create-a-release-definition"></a>릴리스 정의 만들기

릴리스 정의 hello 프로세스 Team Services는 toodeploy hello 앱 실행을 지정 합니다.
Team Services에서 toocreate hello 릴리스 정의:

1. 열기 hello **릴리스** hello 탭 **빌드 &amp; 릴리스** 허브, 열기 hello  **+**  드롭 다운 릴리스 정의의 hello 목록에서 선택 하 고 hello **만들기 릴리스 정의**합니다. 

1. 선택 hello **빈** 템플릿을 선택 하 고 **다음**합니다.

1. Hello에 **아티팩트** 섹션에서 클릭 **아티팩트 링크** 선택 **Jenkins**합니다. Jenkins 서비스 끝점 연결을 선택합니다. 그런 다음 hello Jenkins 소스 작업을 선택 하 고 선택 **만들기**합니다. 

1. Hello 새 릴리스 정의 선택 **작업 추가 +** 추가 **Azure 리소스 그룹 배포** 작업 toohello 기본 환경입니다.

1. 화살표 다음 toohello hello 드롭다운 선택 **작업 추가 +** 에 연결 하 고 배포 그룹 단계 toohello 정의 추가 합니다.

   ![배포 그룹 단계 추가](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Hello 작업 카탈로그에서 엽니다 hello **유틸리티** hello의 인스턴스를 추가 하 고 섹션 **셸 스크립트** 작업 합니다.

1. hello 매개 변수 템플릿 hello Azure 리소스 그룹 배포 작업에 사용 된 hello 관리자 사용 되는 암호 tooconnect toohello Vm을 설정 합니다.
   Hello 변수와 함께이 암호를 제공 **$(adminpassword)**:
   
   - 열기 hello **변수** 탭 및 hello **변수** 섹션을 hello 이름 입력 `adminpassword`합니다.

   - Hello 관리자 암호를 입력 합니다.

   - Hello "자물쇠" 아이콘 다음 toohello 값 텍스트 상자에 붙여넣습니다 tooprotect hello 암호를 선택 합니다. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Hello Azure 리소스 그룹 배포 태스크 구성

hello **Azure 리소스 그룹 배포** 작업은 사용 되는 toocreate hello 배포 그룹입니다. 다음과 같이 구성합니다.

* **Azure 구독:** hello 목록 아래에서 연결을 선택 **사용할 수 있는 Azure 서비스 연결**합니다. 
  연결이 없는 나타나지 **관리**선택, **새 서비스 끝점** 다음 **Azure 리소스 관리자**, hello 프롬프트를 따릅니다.
  새로 고침 hello tooyour 릴리스 정의 반환 **AzureRM 구독** 목록과 만든 선택 hello 연결 합니다.

* **리소스 그룹**: 이전에 만든 hello 리소스 그룹의 이름을 입력 합니다.

* **위치**: hello 배포에 대 한 영역을 선택 합니다.

  ![새 리소스 그룹 만들기](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **템플릿 위치**: `URL of hello file`

* **템플릿 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **템플릿 매개 변수 링크**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **템플릿 매개 변수 재정의**: hello 목록이 재정의 값, 예: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`합니다.<br />{자리 표시자} hello에 대 한 고유한 특정 값을 삽입 합니다. 

* **필수 구성 요소 사용**: `Configure with Deployment Group agent`

* **TFS/VSTS 끝점**: 선택 **추가** hello "새 Team Foundation Server 팀/서비스 연결 추가" 대화 상자에서 선택 및 **토큰 기반 인증**합니다. Hello 연결의 이름 및 팀 프로젝트의 hello URL을 입력 합니다. 그런 다음 생성 하 고 입력 한 [개인 액세스 토큰 (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello 연결 tooyour 팀 프로젝트입니다.

  ![개인용 액세스 토큰 만들기](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **팀 프로젝트**: 현재 프로젝트를 선택합니다.

* **배포 그룹**: 입력 hello에 사용한 것과 동일한 배포 그룹 이름을 hello **리소스 그룹** 매개 변수입니다.

hello Azure 리소스 그룹 배포 작업에 대 한 기본 설정을 hello toocreate 또는 리소스 및 toodo 하므로 증분 업데이트 합니다. hello 작업 hello Vm hello 처음으로 실행 하 고 이후에 업데이트를 만듭니다.

## <a name="configure-hello-shell-script-task"></a>Hello 셸 스크립트 태스크 구성

hello **셸 스크립트** 작업 항목은 각 서버 tooinstall Node.js 및 시작 hello 앱에 스크립트 toorun에 사용 되는 tooprovide hello 구성 합니다. 다음과 같이 구성합니다.

* **스크립트 경로**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **작업 디렉터리 지정**: `Checked`

* **작업 디렉터리**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>이름을 바꾸고 hello 릴리스 정의 저장 합니다.

1. Hello hello 릴리스 정의 toohello 이름에 지정 된 이름을 편집 하는 **빌드 후 작업** hello Jenkins 빌드를 탭 합니다. Jenkins는 hello 소스 아티팩트를 업데이트할 때이 이름을 toobe 수 tootrigger 새 릴리스가 필요 합니다.

1. 필요에 따라 hello 이름을 클릭 하 여 hello 환경의 hello 이름을 변경 합니다. 

1. **저장**과 **확인**을 차례로 선택합니다.

## <a name="start-a-manual-deployment"></a>수동 배포 시작

1. **+ 릴리스**와 **릴리스 만들기**를 차례로 선택합니다.

1. Hello 빌드를 완료 하셨습니까 hello 강조 표시 된 드롭 다운 목록에서 선택 하 고 선택 **만들기**합니다.

1. Hello 팝업 메시지의 hello 릴리스 링크를 선택 합니다. 예를 들어 "**Release-1** 릴리스를 만들었습니다."를 선택합니다.

1. 열기 hello **로그** toowatch hello 릴리스 콘솔 출력을 탭 합니다.

1. 브라우저를 열고 hello URL tooyour 배포 그룹을 추가한 hello 서버 중 하나입니다. 예를 들어 `http://{your-server-ip-address}`를 입력합니다.

## <a name="start-a-cicd-deployment"></a>CI/CD 배포 시작

1. Hello에 정의 해제, hello의 선택을 취소 **Enabled** hello 확인란을 선택 **제어 옵션** hello Azure 리소스 그룹 배포 작업에 대 한 hello 설정의 섹션입니다.
   이후 배포 toohello 기존 배포 그룹에 대 한 불필요 toore-이 작업을 실행 합니다.

1. Toohello 소스 Git 리포지토리를 이동 하 고 hello의 hello 내용을 수정 **h1** hello 파일의 제목 [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade)합니다.

1. 변경 내용을 커밋합니다.

1. 몇 분 후 hello에서 만든 새 릴리스 나타납니다 **릴리스** Team Services 또는 TFS의 페이지입니다. Hello 릴리스 toosee hello 배포 수행을 엽니다. 축하합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Jenkins 빌드 및 릴리스에 대 한 Team Services를 사용 하는 응용 프로그램 tooAzure의 hello 배포를 자동화 합니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Jenkins에서 앱 빌드
> * Team Services와 통합되도록 Jenkins 구성
> * Azure 가상 컴퓨터 hello에 대 한 배포 그룹 만들기
> * Hello Vm을 구성 하 고 hello 앱을 배포 하는 릴리스 정의 만들기

다음 자습서 toolearn toohello toodeploy (Linux, Apache, MySQL 및 PHP) LAMP 스택 하는 방법에 대 한 자세한 진행 합니다.

> [!div class="nextstepaction"]
> [LAMP 스택 배포](tutorial-lamp-stack.md)