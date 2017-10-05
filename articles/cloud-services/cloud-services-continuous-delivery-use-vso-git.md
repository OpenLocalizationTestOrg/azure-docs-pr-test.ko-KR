---
title: "Azure에서 Git 및 Visual Studio Team Services를 사용한 지속적인 업데이트 | Microsoft Docs"
description: "Git을 사용하여 자동으로 빌드되어 Azure 앱 서비스 또는 클라우드 서비스의 웹앱 기능에 배포되도록 Visual Studio Team Services 팀 프로젝트를 구성하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a>Visual Studio Team Services 및 Git을 사용하여 Azure에 지속적으로 전송
Visual Studio Team Services 팀 프로젝트를 사용하여 소스 코드용 Git 리포지토리를 호스트할 수 있으며 리포지토리로 커밋을 푸시할 때마다 Azure 웹앱 또는 클라우드 서비스를 자동으로 빌드 및 배포할 수 있습니다.

Visual Studio 2013 및 Azure SDK가 설치되어 있어야 합니다. Visual Studio 2013을 아직 설치하지 않은 경우 **www.visualstudio.com** 에서 [무료로 시작하기](http://www.visualstudio.com)링크를 선택하여 다운로드하세요. Azure SDK의 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=239540)에서 설치할 수 있습니다.

> [!NOTE]
> 이 자습서를 완료하려면 Visual Studio Team Services 계정이 있어야 합니다. [Visual Studio Team Services 계정은 무료로 개설](http://go.microsoft.com/fwlink/p/?LinkId=512979)할 수 있습니다.
> 
> 

Visual Studio Team Services를 사용하여 Azure에 자동으로 빌드 및 배포하도록 클라우드 서비스를 설정하려면 다음 단계를 따르세요.

## <a name="1-create-a-git-repository"></a>1: Git 리포지토리 만들기
1. Visual Studio Team Services 계정이 없는 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=397665)에서 계정을 확보할 수 있습니다. 팀 프로젝트를 만들 때 소스 제어 시스템으로 Git을 선택합니다. 지침을 따라 Visual Studio를 팀 프로젝트에 연결합니다.
2. **팀 탐색기**에서 **이 리포지토리 복제** 링크를 선택합니다.
   
    ![][3]
3. 로컬 복사본의 위치를 지정한 다음 **복제** 단추를 클릭합니다.

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a>2: 프로젝트를 만들어 리포지토리로 푸시
1. **팀 편집기**의 **솔루션** 섹션에서 로컬 리포지토리에 새 프로젝트를 만들 수 있는 **새** 링크를 선택합니다.
   
    ![][4]
2. 이 연습의 단계에 따라 웹앱 또는 클라우드 서비스(Azure 응용 프로그램)를 배포할 수 있습니다. 새 Azure 클라우드 서비스 프로젝트 또는 새 ASP.NET MVC 프로젝트를 만듭니다. 프로젝트가 .NET Framework 4 또는 그 이상을 대상으로 하는지 확인합니다. Visual Studio 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할과 작업자 역할을 추가합니다.
   웹앱을 만들려는 경우 **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 선택한 후 **MVC**를 선택합니다. 자세한 내용은 [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md) 를 참조하세요.
3. 솔루션의 바로 가기 메뉴를 열고 **커밋**을 선택합니다.
   
    ![][7]
4. Visual Studio Team Services에서 처음으로 Git을 사용하는 경우 Git에서 본인을 식별해 주는 정보를 제공해야 합니다. **팀 탐색기**의 **보류 중인 변경 내용** 영역에서 사용자 이름 및 메일 주소를 입력합니다. 커밋에 대한 설명을 입력한 다음 **커밋** 단추를 선택합니다.
   
    ![][8]
5. 체크 인할 때 특정 변경 내용을 포함하거나 제외하는 옵션을 선택할 수 있습니다. 원하는 변경 내용이 제외된 경우 **모두 포함**링크를 선택합니다.
6. 이제 리포지토리에 있는 로컬 복사본의 변경 내용을 커밋했습니다. 그런 다음 **동기화** 링크를 선택하여 변경 내용을 서버와 동기화합니다.

## <a name="3-connect-the-project-to-azure"></a>3: Azure에 프로젝트 연결
1. Visual Studio Team Services에 일부 소스 코드를 포함한 Git 리포지토리가 있으므로 Azure에 Git 리포지토리를 연결할 준비가 되었습니다.  [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 클라우드 서비스 또는 웹앱을 선택하거나, 왼쪽 아래에 있는 **클라우드 서비스** 또는 **웹앱**을 선택한 후 **빠른 생성**을 선택하여 새로 만듭니다.
   
    ![][9]
2. 클라우드 서비스의 경우 **Visual Studio Team Services로 게시 설정** 링크를 선택합니다. 웹앱의 경우 **소스 코드에서 배포 설정** 링크를 선택합니다.
   
    ![][10]
3. 마법사의 텍스트 상자에 Visual Studio Team Services 계정의 이름을 입력하고 **지금 권한 부여** 링크를 선택합니다. 로그인하라는 메시지가 표시될 수 있습니다.
   
    ![][11]
4. **연결 요청** 팝업 대화 상자에서 **동의함**을 선택하여 Azure에 권한을 부여하고 Visual Studio Team Services에서 팀 프로젝트를 구성합니다.
   
    ![][12]
5. 권한 부여가 완료된 후, Visual Studio Team Services 팀 프로젝트를 포함하는 드롭다운 목록이 표시됩니다.  이전 단계에서 만든 팀 프로젝트 이름을 선택하고 마법사의 확인 표시 단추를 선택합니다.
   
    ![][13]
   
    다음에 리포지토리에 커밋을 푸시할 때 Visual Studio Team Services가 프로젝트를 빌드하여 Azure에 배포합니다.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: 프로젝트 다시 빌드 및 다시 배포 트리거
1. Visual Studio에서 파일을 열어 변경합니다. 예를 들어 MVC 웹 역할의 Views\\ 폴더에서 `_Layout.cshtml` 파일을 변경합니다.
   
    ![][17]
2. 사이트에 대한 바닥글 텍스트를 편집하고 파일을 저장합니다.
   
    ![][18]
3. **솔루션 탐색기**에서 솔루션 노드, 프로젝트 노드 또는 변경한 파일의 바로 가기 메뉴를 연 다음, **커밋**을 선택합니다.
4. 설명을 입력하고 **커밋**을 선택합니다.
   
    ![][20]
5. **동기화** 링크를 선택합니다.
   
    ![][38]
6. **푸시** 링크를 선택하여 Visual Studio Team Services의 리포지토리에 커밋을 푸시합니다. 또한 **동기화** 단추를 사용하여 리포지토리로 커밋을 복사할 수도 있습니다. **동기화** 는 리포지토리의 최신 변경 내용을 끌어온다는 점이 다릅니다.
   
    ![][39]
7. **홈** 단추를 선택하여 **팀 탐색기** 홈 페이지로 돌아갑니다.
   
    ![][21]
8. **빌드** 링크를 선택하여 진행 중인 빌드를 확인합니다.
   
    ![][22]
   
    **팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.
   
    ![][23]
9. 빌드가 진행되는 동안 자세한 로그를 보려면 진행 중인 빌드의 이름을 두 번 클릭합니다.
10. 빌드가 진행되는 동안 마법사를 사용하여 Azure에 연결할 때 생성된 빌드 정의를 살펴봅니다.  빌드 정의의 바로 가기 메뉴를 열고 **빌드 정의 편집**을 선택합니다.
    
    ![][25]
11. **트리거** 탭에서 기본적으로 체크 인할 때마다 빌드 정의가 빌드되도록 설정된 것을 확인합니다. 클라우드 서비스의 경우 Visual Studio Team Services에서 마스터 분기를 자동으로 빌드하여 스테이징 환경에 배포합니다. 라이브 사이트에 배포하려면 여전히 수동 단계를 수행해야 합니다. 스테이징 환경이 없는 웹 사이트의 경우 마스터 분기를 라이브 사이트에 직접 배포합니다.
    
    ![][26]
12. **프로세스** 탭에서 배포 환경이 사용 중인 클라우드 서비스 또는 웹앱의 이름으로 설정된 것을 확인할 수 있습니다.
    
     ![][27]
13. 기본값 이외의 다른 값을 원하는 경우 속성 값을 지정합니다. Azure 게시의 속성은 **배포** 섹션에 있으며 MSBuild 매개 변수를 설정해야 할 수 있습니다. 예를 들어 클라우드 서비스 프로젝트에서 "클라우드" 외의 서비스 구성을 지정하려면 MSbuild 매개 변수를 `/p:TargetProfile=[YourProfile]`로 설정합니다. 여기서 *[YourProfile]*은 ServiceConfiguration.*YourProfile*.cscfg와 같은 이름을 갖는 서비스 구성 파일입니다.
    
     다음 테이블에서는 **배포** 섹션에서 사용할 수 있는 속성을 보여 줍니다.
    
    | 속성 | 기본값 |
    | --- | --- |
    | 신뢰할 수 없는 인증서 허용 |false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다. |
    | 업그레이드 허용 |새로운 배포를 만들지 않고 기존 배포를 업데이트할 수 있습니다. IP 주소를 유지합니다. |
    | 삭제 안 함 |true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨). |
    | 배포 설정의 경로 |보고서의 루트 폴더를 기준으로 웹앱의 .pubxml 파일 경로입니다. 클라우드 서비스의 경우 무시됩니다. |
    | SharePoint 배포 환경 |서비스 이름과 같습니다. |
    | Azure 배포 환경 |웹앱 또는 클라우드 서비스 이름입니다. |
14. 이제 빌드가 완료됩니다.
    
     ![][28]
15. 빌드 이름을 두 번 클릭하면 Visual Studio에서 연결된 단위 테스트 프로젝트의 모든 테스트 결과가 포함된 **빌드 요약**을 표시합니다.
    
     ![][29]
16. [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 스테이징 환경을 선택하면 **배포** 탭에서 연결된 배포를 확인할 수 있습니다.
    
     ![][30]
17. 사용 중인 사이트의 URL로 이동합니다. 웹앱의 경우 포털에서 **찾아보기** 단추를 선택합니다. 클라우드 서비스의 경우 클라우드 서비스에 대한 스테이징 환경을 표시하는 **대시보드** 페이지의 **간략 상태** 섹션에서 URL을 선택합니다.
    
    클라우드 서비스의 연속 통합에서 배포는 기본적으로 스테이징 환경에 게시됩니다. **대체 클라우드 서비스 환경** 속성을 **프로덕션**으로 설정하여 이를 변경할 수 있습니다. 다음 스크린샷은 클라우드 서비스의 대시보드 페이지에서 사이트 URL이 어느 위치에 있는지 보여 줍니다.
    
    ![][31]
    
    새 브라우저 탭이 열리며 실행 중인 사이트를 표시합니다.
    
    ![][32]
18. 프로젝트의 다른 내용을 변경하고 추가 빌드를 트리거하면 여러 배포가 누적됩니다. 최신 배포가 활성으로 표시됩니다.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: 초기 빌드 다시 배포
이 단계는 옵션입니다. Azure 클래식 포털에서 이전 배포를 선택하고 **다시 배포** 를 선택하여 사이트를 이전 체크 인으로 되돌립니다. 그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.

![][34]

## <a name="6-change-the-production-deployment"></a>6: 프로덕션 배포 변경
준비가 되면 Azure 클래식 포털에서 **교환** 을 선택하여 스테이징 환경에서 프로덕션 환경으로 수준을 올릴 수 있습니다. 새로 배포된 스테이징 환경에서 프로덕션으로 수준이 올라가며, 이전 프로덕션 환경이 있는 경우 스테이징 환경으로 변경됩니다. 활성 배포는 프로덕션 환경과 스테이징 환경에서 서로 다를 수 있지만 최근 빌드의 배포 기록은 환경과 관계없이 동일합니다.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: 작업 분기에서 배포
Git을 사용할 경우 보통 작업 분기에서 변경한 다음 개발이 최종 단계에 도달하면 마스터 분기로 통합합니다. 프로젝트의 개발 단계에서는 작업 분기를 구성하여 Azure에 배포합니다.

1. **팀 탐색기**에서 **홈** 단추를 선택한 다음 **분기** 단추를 선택합니다.
   
    ![][40]
2. **새 분기** 링크를 선택합니다.
   
    ![][41]
3. "working"과 같은 분기의 이름을 입력하고 **분기 만들기**를 선택합니다. 그러면 새 로컬 분기가 생성됩니다.
   
    ![][42]
4. 분기를 게시합니다. **게시 취소된 분기**에서 분기 이름을 선택하고 **게시**를 선택합니다.
   
    ![][44]
5. 기본적으로 마스터 분기만 변경하면 연속 빌드가 트리거됩니다. 작업 분기의 연속 빌드를 설정하려면 **팀 탐색기**에서 **빌드** 페이지를 선택하고 **빌드 정의 편집**을 선택합니다.
6. **소스 설정** 탭을 선택합니다. **지속적인 통합 및 빌드의 모니터링된 분기**에서 **새 행을 추가하려면 여기를 클릭하세요.**를 선택합니다.
   
    ![][47]
7. 생성된 분기(예: refs/heads/working)를 지정합니다.
   
    ![][48]
8. 코드를 변경하고, 변경된 파일의 바로 가기 메뉴를 연 다음, **커밋**을 선택합니다.
   
    ![][43]
9. **동기화되지 않은 커밋** 링크를 선택한 다음 **동기화** 단추 또는 **푸시** 링크를 선택하여 Visual Studio Team Services에서 작업 분기의 복사본 변경 내용을 복사합니다.
   
   ![][45]
10. **빌드** 뷰로 이동하여 작업 분기에 대해 트리거된 빌드를 찾습니다.

## <a name="next-steps"></a>다음 단계
Visual Studio Team Services에서 Git 사용에 대해 더 많은 팁을 알아보려면 [Visual Studio를 사용하여 Git에서 코드 개발 및 공유](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)를 참조하고, Visual Studio Team Services에서 관리하지 않는 Git 리포지토리를 사용하여 Azure에 게시하는 방법에 대한 자세한 내용은 [Azure App Service에 지속적인 배포](../app-service-web/app-service-continuous-deployment.md)를 참조하세요. Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
