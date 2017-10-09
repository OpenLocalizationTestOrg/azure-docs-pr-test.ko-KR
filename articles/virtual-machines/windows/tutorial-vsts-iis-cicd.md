---
title: "Team Services를 사용 하 여 Azure에서 CI/CD 파이프라인 aaaCreate | Microsoft Docs"
description: "연속 통합 및 Windows VM에서 웹 앱 tooIIS를 배포 하는 배달에 대 한 Visual Studio Team Services toocreate 파이프라인 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Visual Studio Team Services 및 IIS를 사용하여 연속 통합 파이프라인 만들기
tooautomate hello 빌드, 테스트 및 배포 응용 프로그램 개발 단계를 연속 통합 및 배포 (CI/CD) 파이프라인을 사용할 수 있습니다. 이 자습서에서는 Visual Studio Team Services 및 IIS를 실행하는 Azure의 Windows VM(가상 컴퓨터)를 사용하여 CI/CD 파이프라인을 만듭니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * ASP.NET 웹 응용 프로그램 tooa Team Services 프로젝트를 게시 합니다.
> * 코드 커밋으로 트리거되는 빌드 정의 만들기
> * Azure의 가상 컴퓨터에 IIS 설치 및 구성
> * Team Services에서 hello IIS 인스턴스 tooa 배포 그룹을 추가 합니다.
> * 릴리스 정의 toopublish 새로운 웹 배포 패키지 tooIIS
> * 테스트 hello CI/CD 파이프라인

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 `Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.


## <a name="create-project-in-team-services"></a>Team Services에서 프로젝트 만들기
Visual Studio Team Services를 사용하면 온-프레미스 코드 관리 솔루션을 유지 관리하지 않고도 손쉽게 공동 작업하고 개발할 수 있습니다. Team Services는 클라우드 코드 테스트, 빌드 및 응용 프로그램 정보를 제공합니다. 코드 개발에 가장 적합한 버전 제어 리포지토리 및 IDE를 선택할 수 있습니다. 이 자습서에 대 한 무료 계정 toocreate 기본 ASP.NET 웹 응용 프로그램 및 CI/CD 파이프라인을 사용할 수 있습니다. Team Services 계정이 없는 경우 [해당 계정을 만듭니다](http://go.microsoft.com/fwlink/?LinkId=307137).

toomanage hello 코드 커밋 프로세스를 빌드 정의 및 정의 해제, Team Services에서 다음과 같이 프로젝트를 만듭니다.

1. 웹 브라우저에서 Team Services 대시보드를 열고 **새 프로젝트**를 선택합니다.
2. 입력 *myWebApp* hello에 대 한 **프로젝트 이름**합니다. 다른 모든 기본 값 toouse 둡니다 *Git* 버전 제어 및 *Agile* 프로세스 작업 항목.
3. 너무 hello 옵션을 선택**공유할** *팀원*을 선택한 후 **만들기**합니다.
5. 프로젝트를 만든 후 hello 옵션을 너무 선택**추가 정보 또는 gitignore 초기화**, 다음 **초기화**합니다.
6. 새 프로젝트를 내부 선택 **대시보드** hello 위쪽 선택 **Visual Studio에서 열기**합니다.


## <a name="create-aspnet-web-application"></a>ASP.NET 웹 응용 프로그램 만들기
Hello 이전 단계에서 Team Services에서 프로젝트를 만들었습니다. hello 최종 단계는 Visual Studio에서 새 프로젝트를 엽니다. 사용자 코드 커밋 hello에 관리 **팀 탐색기** 창. 새 프로젝트의 로컬 복사본을 만든 다음 템플릿에서 다음과 같이 ASP.NET 웹 응용 프로그램을 만듭니다.

1. 선택 **복제** toocreate Team Services 프로젝트의 로컬 git 리포지토리 합니다.
    
    ![Team Services 프로젝트에서 리포지토리 복제](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. **솔루션**에서 **새로 만들기**를 선택합니다.

    ![웹 응용 프로그램 솔루션 만들기](media/tutorial-vsts-iis-cicd/new_solution.png)

3. 선택 **웹** 템플릿 hello 선택 **ASP.NET 웹 응용 프로그램** 템플릿.
    1. 같은 응용 프로그램에 대 한 이름을 입력 *myWebApp*에 대 한 hello 확인란의 선택을 취소 하 고 **솔루션용 디렉터리 만들기**합니다.
    2. Hello 옵션을 사용할 수 있는 경우 확인란의 선택을 취소 hello 너무**Application Insights 추가 tooproject**합니다. Application Insights 있습니다 tooauthorize Azure Application Insights를 사용한 웹 응용 프로그램 필요 합니다. tookeep이이 자습서에서는 간단한 것이 프로세스를 건너뜁니다.
    3. **확인**을 선택합니다.
4. 선택 **MVC** hello 템플릿 목록에서 합니다.
    1. **인증 변경**을 선택하고 **인증 없음**을 선택한 다음 **확인**을 선택합니다.
    2. 선택 **확인** toocreate 솔루션입니다.
5. Hello에 **팀 탐색기** 창 선택 **변경**합니다.

    ![TooTeam 서비스 git 리포지토리에 있는 로컬 변경 내용 커밋](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Hello 커밋 텍스트 상자에를 입력 메시지와 같은 *초기 커밋*합니다. 선택 **모든 커밋 및 동기화** hello 드롭 다운 메뉴에서 합니다.


## <a name="create-build-definition"></a>빌드 정의 만들기
Team Services 응용 프로그램을 작성 해야 하는 방법을 빌드 정의 toooutline를 사용 합니다. 이 자습서에서는 코드 hello 솔루션을 빌드합니다 다음 웹을 만듭니다는 toorun hello 웹 응용 프로그램 IIS 서버에서 사용할 수 패키지를 배포 하는 기본 정의 만듭니다.

1. Team Services 프로젝트에서 선택 **빌드 및 릴리스** hello 위쪽 선택 **빌드**합니다.
3. **+ 새 정의**를 선택합니다.
4. Hello 선택 **ASP.NET (미리 보기)** 템플릿과 선택 **적용**합니다.
5. 작업의 값 모두 hello 기본값을 유지 합니다. 아래 **원본을 가져올**, 해당 hello 확인 *myWebApp* 리포지토리 및 *마스터* 분기를 선택 합니다.

    ![Team Services 프로젝트에서 빌드 정의 만들기](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Hello에 **트리거** 탭에 대 한 hello 슬라이더를 이동, **이 트리거를 사용 하도록 설정** 너무*Enabled*합니다.
7. Hello 빌드 정 및 큐를 선택 하 여 새 빌드 저장 **저장 후 큐** , 다음 **저장 후 큐** 다시 합니다. 선택한 hello 기본값 그대로 두고 **큐**합니다.

조사식은 hello 빌드 호스트 된 에이전트에서 예약 된 다음 toobuild을 시작 합니다. hello 비슷한 toohello 다음은 예제 출력:

![성공적인 Team Services 프로젝트 빌드](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
플랫폼 toorun tooprovide ASP.NET 웹 응용 프로그램 IIS를 실행 하는 Windows 가상 컴퓨터 필요 합니다. Team Services 코드를 커밋합니다 및 빌드 트리거되는으로 hello IIS 인스턴스와 에이전트 toointeract를 사용 합니다.

[이 스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json)을 사용하여 Windows Server 2016 VM을 만듭니다. Hello 스크립트 toorun 몇 분 정도 걸리며 hello VM을 만듭니다. Hello VM을 만든 후에 웹 트래픽에 대해 포트 80을 열고 [추가 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) 다음과 같습니다.

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM을 hello와 공용 IP 주소를 가져올 [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 다음과 같습니다.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

원격 데스크톱 세션 tooyour VM을 만듭니다.

```cmd
mstsc /v:<publicIpAddress>
```

Hello VM에서 열고는 **관리자 PowerShell** 명령 프롬프트입니다. 다음과 같이 IIS 및 필요한 .NET 기능을 설치합니다.

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>배포 그룹 만들기
hello 웹 아웃 toopush 패키지 toohello IIS 서버를 배포 하 고 Team Services에서 배포 그룹을 정의 합니다. 이 그룹을 커밋하 코드 tooTeam 서비스 및 빌드 완료 된 서버를 새 빌드 hello 대상 toospecify가 있습니다.

1. Team Services에서 **빌드 및 릴리스**를 선택한 다음 **배포 그룹**을 선택합니다.
2. **배포 그룹 추가**를 선택합니다.
3. 같은 hello 그룹에 대 한 이름을 입력 *myIIS*을 선택한 후 **만들기**합니다.
4. Hello에 **컴퓨터 등록** 섹션에서 확인 *Windows* 을 선택 하면 hello 확인란 너무**hello 스크립트의 개인용 액세스 토큰을 사용 하 여 인증에 대 한**합니다.
5. 선택 **스크립트 tooclipboard 복사**합니다.


### <a name="add-iis-vm-toohello-deployment-group"></a>IIS VM toohello 배포 그룹 추가
Hello 배포 그룹을 만든에 각 IIS 인스턴스 toohello 그룹을 추가 합니다. 다운로드 하 고 새 웹을 수신 하는 VM을 배포 하는 hello에 에이전트를 구성 하는 스크립트를 생성 하는 team Services를 패키지 한 다음 tooIIS 적용 됩니다.

1. Hello에 다시 **관리자 PowerShell** 세션 VM에 붙여 넣고 Team Services에서 복사 하는 hello 스크립트를 실행 합니다.
2. Hello 에이전트에 대 한 증명된 tooconfigure 태그 선택 하는 경우 *Y* 입력 *웹*합니다.
3. Hello 사용자 계정에 대 한 메시지가 표시 되 면 키를 눌러 *반환* tooaccept hello 기본값입니다.
4. 메시지와 함께 hello 스크립트 toofinish 대기 *서비스 vstsagent.account.computername 성공적으로 시작*합니다.
5. Hello에 **배포 그룹** hello 페이지 **빌드 및 릴리스** 메뉴를 열고 hello *myIIS* 배포 그룹입니다. Hello에 **컴퓨터** 탭 VM이 나열 되어 있는지 확인 합니다.

    ![VM은 tooTeam 서비스 배포 그룹을 성공적으로 추가](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>릴리스 정의 만들기
toopublish Team Services에서 릴리스 정의 만든 빌드에 있습니다. 응용 프로그램을 성공적으로 빌드하면 이 정의가 자동으로 트리거됩니다. Hello 배포 그룹 toopush 웹 배포 패키지를, 선택한 hello 적절 한 IIS 설정을 정의 합니다.

1. **빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다. 이전 단계에서 만든 hello 빌드 정의 선택 합니다.
2. 아래 **최근에 완료 된**를 hello 최신 빌드를 선택한 다음 선택 **릴리스**합니다.
3. 선택 **예** toocreate 릴리스 정의 합니다.
4. Hello 선택 **빈** 서식 파일을 다음 선택 **다음**합니다.
5. 프로젝트를 프로젝트 및 소스 빌드 정의 hello 채워져 확인 합니다.
6. 선택 hello **연속 배포** 확인란을 선택한 다음 선택 **만들기**합니다.
7. 다음 너무 hello 드롭다운 상자를 선택**작업 추가 +** 선택 *배포 그룹 단계 추가*합니다.
    
    ![Team Services에서 작업 toorelease 정의 추가 합니다.](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. 선택 **추가** 다음 너무**IIS 웹 응용 프로그램 Deploy(Preview)**을 선택한 후 **닫기**합니다.
9. 선택 hello **배포 그룹에서 실행** 부모 작업 합니다.
    1. 에 대 한 **배포 그룹**선택, hello 배포 그룹 등 이전에 만든 *myIIS*합니다.
    2. Hello에 **태그 컴퓨터** 상자 선택 **추가** hello 선택 *웹* 태그입니다.
    
    ![IIS용 정의 배포 그룹 작업 릴리스](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. 선택 hello **배포: IIS 웹 응용 프로그램 배포** 작업 tooconfigure IIS 설정을 다음과 같이 인스턴스:
    1. **웹 사이트 이름**에서 *기본 웹 사이트*를 입력합니다.
    2. 모든 hello 다른 기본 설정을 그대로 둡니다.
12. **저장**을 선택한 다음 **확인**을 두 번 선택합니다.


## <a name="create-a-release-and-publish"></a>릴리스 만들기 및 게시
이제 웹 배포 패키지를 새 릴리스로 푸시할 수 있습니다. 이 단계는 hello 배포 그룹의 일부인, hello 웹 푸시 각 인스턴스에서 hello 에이전트와 통신 패키지를 배포한 다음 IIS toorun 업데이트 hello 웹 응용 프로그램을 구성 합니다.

1. 릴리스 정의에서 **+ 릴리스**를 선택한 다음 **릴리스 만들기**를 선택합니다.
2. 와 함께 hello 최신 빌드 hello 드롭 다운 목록에서 선택 되어 있는지 확인 **자동 배포: 릴리스 생성 이후**합니다. **만들기**를 선택합니다.
3. 작은 배너를 표시 하려면 릴리스 정의의 hello 위쪽와 같은 *' 릴리스 1' 릴리스를 만든*합니다. 선택 hello 릴리스 링크입니다.
4. 열기 hello **로그** toowatch hello 릴리스 진행률을 탭 합니다.
    
    ![성공적인 Team Services 릴리스 및 웹 배포 패키지 푸시](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Hello 릴리스 완료 되 면 웹 브라우저를 열고 하 고 VM의 hello 공용 IIP 주소를 입력 합니다. ASP.NET 웹 응용 프로그램이 실행되고 있습니다.

    ![IIS VM에서 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>테스트 hello 전체 CI/CD 파이프라인
IIS에서 실행 중인 웹 응용 프로그램을 지금 hello 전체 CI/CD 파이프라인을 시도 하십시오. Visual Studio와 다음 업데이트 된 웹 릴리스를 트리거하는 코드를 빌드 트리거되는 커밋 변경한 후 배포 패키지 tooIIS:

1. Visual Studio에서 열고 hello **솔루션 탐색기** 창.
2. Tooand 열기 이동 *myWebApp | 뷰 | 홈 | Index.cshtml*
3. 6 행 tooread를 편집 합니다.

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Hello 파일을 저장 합니다.
5. 열기 hello **팀 탐색기** 창, 선택 hello *myWebApp* 프로젝트를 선택한 다음 선택 **변경**합니다.
6. 커밋 메시지를 같은 입력 *테스트 CI/CD 파이프라인*를 눌러 **커밋 모든 및 동기화** hello 드롭 다운 메뉴에서 합니다.
7. Team Services 작업 영역에서 새 빌드 hello 코드 커밋이 트리거됩니다. 
    - **빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다. 
    - 차례로 hello를 선택한 다음 빌드 정의 선택 **실행 및 큐 대기** hello로 빌드 toowatch 빌드 진행 합니다.
9. Hello 빌드에 성공 후 새 릴리스가 트리거됩니다.
    - 선택 **빌드 및 릴리스**, 다음 **릴리스** toosee hello 웹 배포 패키지 tooyour IIS VM 푸시됩니다. 
    - 선택 hello **새로 고침** 아이콘 tooupdate hello 상태입니다. Hello 때 *환경* 열에 녹색 확인 표시가 표시, hello 릴리스가 tooIIS 성공적으로 배포 합니다.
11. toosee 변경 내용을 적용 되며, 브라우저에서 IIS 웹 사이트를 새로 고칩니다.

    ![CI/CD 파이프라인을 통해 IIS VM을 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>다음 단계

이 자습서에서는 Team Services에서 ASP.NET 웹 응용 프로그램을 생성 하 고 구성 된 빌드 및 릴리스 정의 toodeploy 새 웹 배포 패키지 tooIIS 각 코드 커밋에 합니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * ASP.NET 웹 응용 프로그램 tooa Team Services 프로젝트를 게시 합니다.
> * 코드 커밋으로 트리거되는 빌드 정의 만들기
> * Azure의 가상 컴퓨터에 IIS 설치 및 구성
> * Team Services에서 hello IIS 인스턴스 tooa 배포 그룹을 추가 합니다.
> * 릴리스 정의 toopublish 새로운 웹 배포 패키지 tooIIS
> * 테스트 hello CI/CD 파이프라인

다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.

> [!div class="nextstepaction"]
> [SSL로 웹 서버 보안](tutorial-secure-web-server.md)