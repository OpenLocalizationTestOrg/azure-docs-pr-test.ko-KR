---
title: "Git 및 Azure에서 Visual Studio Team Services를 사용한 aaaContinuous 배달 | Microsoft Docs"
description: "어떻게 tooconfigure Visual Studio Team Services 팀 프로젝트 toouse Git tooautomatically 빌드 및 Azure 앱 서비스 또는 클라우드 서비스의 toohello 웹 응용 프로그램 기능을 배포에 대해 알아봅니다."
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
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>Visual Studio Team Services 및 Git를 사용 하 여 지속적인 업데이트 tooAzure
있습니다 수 소스 코드를 Visual Studio Team Services 팀 프로젝트 toohost Git 리포지토리를 사용 하 고 자동으로 빌드 및 tooAzure 웹 앱을 배포 또는 클라우드 서비스 커밋 toohello 리포지토리에 푸시 될 때마다 합니다.

Visual Studio 2013 및 Azure SDK가 설치 되어 hello 필요 합니다. Visual Studio 2013, 아직 없는 경우 hello를 선택 하 여 다운로드 **무료로 시작** 동시 연결할 [www.visualstudio.com](http://www.visualstudio.com)합니다. 설치에서 Azure SDK hello [여기](http://go.microsoft.com/fwlink/?LinkId=239540)합니다.

> [!NOTE]
> 이 자습서는 Visual Studio Team Services 계정 toocomplete 필요한: 할 수 있습니다 [무료 Visual Studio Team Services 계정 열고](http://go.microsoft.com/fwlink/p/?LinkId=512979)합니다.
> 
> 

클라우드 서비스 tooautomatically tooset 빌드 및 Visual Studio Team Services를 사용 하 여 tooAzure 배포, 다음이 단계를 수행 합니다.

## <a name="1-create-a-git-repository"></a>1: Git 리포지토리 만들기
1. Visual Studio Team Services 계정이 없는 경우 [여기](http://go.microsoft.com/fwlink/?LinkId=397665)에서 계정을 확보할 수 있습니다. 팀 프로젝트를 만들 때 소스 제어 시스템으로 Git을 선택합니다. Hello 지침 tooconnect Visual Studio tooyour 팀 프로젝트를 수행 합니다.
2. **팀 탐색기**, hello 선택 **이 리포지토리를 복제** 링크 합니다.
   
    ![][3]
3. Hello 로컬 복사본의 hello 위치를 지정 하 고 hello를 눌러 **복제** 단추입니다.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: 프로젝트를 만들고 toohello 저장소 커밋
1. **팀 탐색기**, hello에 **솔루션** 섹션에서 hello **새로** toocreate hello 로컬 저장소에서 새 프로젝트를 연결 합니다.
   
    ![][4]
2. 웹 앱을 배포할 수 또는이 연습 단계를 다음 hello 사용 하 여 클라우드 서비스 (Azure 응용 프로그램). 새 Azure 클라우드 서비스 프로젝트 또는 새 ASP.NET MVC 프로젝트를 만듭니다. Hello 프로젝트의 대상.NET Framework 4 hello 하 고 있는지 확인 합니다. Visual Studio 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할과 작업자 역할을 추가합니다.
   Toocreate 웹 응용 프로그램을 사용 하도록 하려는 경우 선택 hello **ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 선택한 후 **MVC**합니다. 자세한 내용은 [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md) 를 참조하세요.
3. Hello 솔루션에 대 한 hello 바로 가기 메뉴를 열고 **커밋**합니다.
   
    ![][7]
4. 인 경우 hello 처음으로 Visual Studio Team Services에서 Git를 사용한 해야 tooprovide 일부 정보 tooidentify 직접 Git에서 합니다. Hello에 **보류 중인 변경 내용** 부문의 **팀 탐색기**사용자 이름을 입력 하 고 전자 메일 주소입니다. Hello 커밋에 대 한 설명을 입력 한 다음 hello **커밋** 단추입니다.
   
    ![][8]
5. Hello 옵션 tooinclude 또는 특정 변경 내용을 체크 인할 때 제외. Hello 변경한 경우 하려는 제외 된를 **모두 포함**합니다.
6. 했습니다. 이제 hello 저장소의 로컬 복사본으로 커밋된 hello 변경 합니다. 다음으로 hello를 선택 하 여 hello 서버와 해당 변경 내용을 동기화 **동기화** 링크 합니다.

## <a name="3-connect-hello-project-tooazure"></a>3: hello 프로젝트 tooAzure 연결
1. 준비 tooconnect는 일부 소스 코드를 Visual Studio Team Services의 Git 리포지토리를가지고 git 리포지토리 tooAzure 합니다.  Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)클라우드 서비스나 웹 응용 프로그램을 선택 하거나 hello + 왼쪽 아래 hello 및 선택 아이콘을 선택 하 여 새로 만들 **클라우드 서비스** 또는 **웹 응용 프로그램**차례로 **빨리 만들기**합니다.
   
    ![][9]
2. 클라우드 서비스에 대 한 선택 hello **Visual Studio Team Services를 통해 게시 설정** 링크 합니다. 웹 앱에 대 한 선택 hello **소스 제어에서 배포 설정** 링크 합니다.
   
    ![][10]
3. Hello 마법사에서 hello 텍스트 상자에 hello Visual Studio Team Services 계정 이름을 입력 하 고 hello 선택 **이제 권한을 부여** 링크 합니다. toosign을 메시지가 나타날 수 있습니다.
   
    ![][11]
4. Hello에 **연결 요청** 팝업 대화 상자에서 선택 **Accept** tooauthorize Azure tooconfigure Visual Studio Team Services에서 팀 프로젝트입니다.
   
    ![][12]
5. 권한 부여가 완료된 후, Visual Studio Team Services 팀 프로젝트를 포함하는 드롭다운 목록이 표시됩니다.  Hello 이전 단계에서 만든 팀 프로젝트의 hello 이름 선택한 hello 마법사의 확인 표시 단추를 선택 합니다.
   
    ![][13]
   
    hello 커밋 tooyour 리포지토리를 Visual Studio Team Services 푸시 다음에 빌드하고 프로젝트 tooAzure 배포 됩니다.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: 프로젝트 다시 빌드 및 다시 배포 트리거
1. Visual Studio에서 파일을 열어 변경합니다. 예를 들어 hello 파일을 변경 `_Layout.cshtml` hello 보기에서\\MVC 웹 역할에서 공유 폴더입니다.
   
    ![][17]
2. Hello 사이트에 대 한 hello 바닥글 텍스트를 편집 하 고 hello 파일을 저장 합니다.
   
    ![][18]
3. **솔루션 탐색기**를 hello 솔루션 노드, 프로젝트 노드 또는 hello 파일 변경 hello 바로 가기 메뉴를 열고 다음 선택 **커밋**합니다.
4. 설명을 입력하고 **커밋**을 선택합니다.
   
    ![][20]
5. Hello 선택 **동기화** 링크 합니다.
   
    ![][38]
6. Hello 선택 **푸시** toopush Visual Studio Team Services에서 커밋 toohello 리포지토리에 연결 합니다. (Hello를 사용할 수도 있습니다 **동기화** toocopy 커밋 toohello 리포지토리에 단추입니다. hello 차이점은 **동기화** 도 끌어오는 소스 hello hello 리포지토리에서 최근 변경 내용을.)
   
    ![][39]
7. Hello 선택 **홈** 단추 tooreturn toohello **팀 탐색기** 홈 페이지입니다.
   
    ![][21]
8. 선택 **빌드** tooview hello 빌드 진행 중에서입니다.
   
    ![][22]
   
    **팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.
   
    ![][23]
9. 자세한 로그 tooview hello 빌드 진행 과정에서 이름을 두 번 클릭 hello hello 빌드가 진행 중입니다.
10. Hello 빌드가 진행 중인 hello 마법사 toolink tooAzure를 사용할 때 생성 된 hello 빌드 정의에서 살펴보겠습니다.  Hello 빌드 정의 대 한 hello 바로 가기 메뉴를 열고 **빌드 정의 편집**합니다.
    
    ![][25]
11. Hello에 **트리거** 탭 표시 됩니다는 hello 빌드 정의 toobuild 모든 체크 인에 기본적으로 설정 됩니다. (클라우드 서비스에 대 한 Visual Studio Team Services 빌드 및 배포 환경을 자동으로 준비 하는 hello 마스터 분기 toohello. 해야 toodo 수동 단계 toodeploy toohello 라이브 사이트 합니다. 웹 앱에는 스테이징 환경 없는 hello 마스터 분기 toohello 라이브 사이트에 직접 배포 합니다.
    
    ![][26]
12. Hello에 **프로세스** 탭 hello 배포 환경에 클라우드 서비스 또는 웹 응용 프로그램의 toohello 이름을 설정 되어을 확인할 수 있습니다.
    
     ![][27]
13. Hello 기본값 값은 다른 hello 속성에 대 한 값을 지정 합니다. hello Azure 게시에 대 한 속성에에서 있는 hello **배포** 섹션과 있습니다 tooset MSBuild 매개 변수 필요할 수도 있습니다. 예를 들어 toospecify "클라우드" 이외의 다른 서비스 구성 클라우드 서비스 프로젝트에서 hello MSbuild 매개 변수를 너무 설정`/p:TargetProfile=[YourProfile]` 여기서 *[YourProfile]* 일치와 같은 이름 가진 서비스 구성 파일 ServiceConfiguration입니다. *YourProfile*.cscfg입니다.
    
     hello 다음 표에 나와 hello 사용 가능한 속성 hello **배포** 섹션:
    
    | 속성 | 기본값 |
    | --- | --- |
    | 신뢰할 수 없는 인증서 허용 |false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다. |
    | 업그레이드 허용 |Hello 배포 tooupdate 새로 만드는 대신 기존 배포를 허용 합니다. Hello IP 주소를 유지합니다. |
    | 삭제 안 함 |true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨). |
    | 경로 tooDeployment 설정 |hello tooyour.pubxml 파일 경로 웹 앱, 상대 toohello hello 리 포 루트 폴더에 대 한 합니다. 클라우드 서비스의 경우 무시됩니다. |
    | SharePoint 배포 환경 |hello 서비스 이름으로을 hello 동일 합니다. |
    | Azure 배포 환경 |hello 웹 응용 프로그램 또는 클라우드 서비스 이름입니다. |
14. 이제 빌드가 완료됩니다.
    
     ![][28]
15. Hello 빌드 이름을 두 번 클릭 하면 Visual Studio는 표시는 **빌드 요약**, 연결 된 단위 테스트 프로젝트의 모든 테스트 결과 포함 합니다.
    
     ![][29]
16. Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), hello에 관련 된 hello 배포를 볼 수 있습니다 **배포** hello 스테이징 환경 선택 된 경우를 탭 합니다.
    
     ![][30]
17. 찾아보기 tooyour 사이트의 URL입니다. 웹 앱에 대 한 선택 hello **찾아보기** hello 포털에서 단추입니다. 클라우드 서비스에 대 한 hello에 hello URL 선택 **빠른 보기** hello 섹션 **대시보드** hello 스테이징 환경을 보여 주는 페이지.
    
    클라우드 서비스에 대 한 연속 통합에서 배포는 기본적으로 게시 된 toohello 스테이징 환경입니다. Hello 설정 하 여 변경할 수 있습니다 **대체 클라우드 서비스 환경** 속성 너무**프로덕션**합니다. 여기서 hello 사이트 URL을 hello 클라우드 서비스의 대시보드 페이지에는 다음과 같습니다.
    
    ![][31]
    
    새 브라우저 탭이 열립니다 실행 중인 사이트 tooreveal 됩니다.
    
    ![][32]
18. 만들면 tooyour 프로젝트 변경 된 기타, 하면 트리거 더 빌드 및 배포를 여러 개를 누적 합니다. hello 최신 중 하나가 활성으로 표시 됩니다.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: 초기 빌드 다시 배포
이 단계는 옵션입니다. 에 Azure 클래식 포털 hello 이전 배포를 선택 하 고 선택 **재배포** toorewind 사이트 tooan를 앞에서 체크 인 합니다. 그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: hello 프로덕션 배포를 변경 합니다.
준비 되 면 선택 하 여 hello 준비 toohello 프로덕션 환경의 승격할 수 있습니다 **교체** hello Azure 클래식 포털의에서. 새로 배포 된 hello 스테이징 환경 승격된 tooProduction 이며 hello 이전 프로덕션 환경에서는 있는 경우 스테이징 환경 있게 됩니다. 활성 배포 hello hello 프로덕션 및 스테이징 환경에 대해 다를 수 있습니다 하지만 최근 빌드 hello 배포 기록을 hello 동일 환경에 관계 없이 합니다.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: 작업 분기에서 배포
Git를 사용 하면 일반적으로 변경 작업 분기에서 하 고 개발에는 완료 된 상태에 도달할 때 hello 마스터 분기에 통합 합니다. 프로젝트를 hello 개발 단계 동안 toobuild 원하는 고 hello 작업 분기 tooAzure를 배포 합니다.

1. **팀 탐색기**, hello 선택 **홈** 단추를 선택한 후 hello **분기** 단추입니다.
   
    ![][40]
2. Hello 선택 **새 분기** 링크 합니다.
   
    ![][41]
3. "Working"와 같은 hello 분기의 hello 이름을 입력 하 고 선택 **분기 생성**합니다. 그러면 새 로컬 분기가 생성됩니다.
   
    ![][42]
4. Hello 분기를 게시 합니다. Hello 분기 이름에 선택 **분기 게시 되지 않은**, 선택 **게시**합니다.
   
    ![][44]
5. 기본적으로 toohello 마스터 분기는 연속 빌드 트리거를 변경 됩니다. 작업 분기에 대 한 연속 빌드 설치 tooset 선택 hello **빌드** 페이지에 **팀 탐색기**, 선택 **빌드 정의 편집**합니다.
6. 열기 hello **소스 설정** 탭 합니다. 아래 **연속 통합 및 빌드에 대 한 분기 모니터링**, 선택 **tooadd 새 행 여기를 클릭**합니다.
   
    ![][47]
7. Refs/헤드/작업 같이 사용자가 만든 hello 분기를 지정 합니다.
   
    ![][48]
8. 선택 hello 코드를 변경 하는 hello 파일에 대 한 바로 가기 메뉴를 열고 hello에 변경 내용을 확인 한 다음 **커밋**합니다.
   
    ![][43]
9. Hello 선택 **되지 않은 커밋** 링크를 선택한 hello **동기화** 단추나 hello **푸시** 링크 toocopy hello toohello 복사본 Visual Studio에서 hello 작업 분기의 변경 Team Services입니다.
   
   ![][45]
10. Toohello 이동 **빌드** 보기 및 hello 작업 분기에 대 한 hello 빌드를 방금 트리거한 (를) 가져왔습니다.

## <a name="next-steps"></a>다음 단계
toolearn Visual Studio Team Services를 통해 Git를 사용 하 여에 관한 자세한 정보 참조 [개발 하 고 Visual Studio를 사용 하 여 Git에서 코드를 공유할](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) toopublish Visual Studio Team Services에서 관리 되지 않는 한 Git 리포지토리를 사용 하 여에 대 한 정보 tooAzure, 참조 [연속 배포 tooAzure 앱 서비스](../app-service-web/app-service-continuous-deployment.md)합니다. Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.

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
