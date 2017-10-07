---
title: "연속 통합 (Team Services)와 Azure 서비스 패브릭 응용 프로그램 aaaDeploy | Microsoft Docs"
description: "자세한 방법을 tooset 연속 통합 및 Visual Studio Team Services를 사용 하 여 서비스 패브릭 응용 프로그램에 대 한 배포를 구성 합니다.  Azure에서 응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>CI/CD tooa 서비스 패브릭 클러스터와 응용 프로그램 배포
이 자습서는 일련의 3 개 속하며 설명 방법을 tooset 연속 통합 및 Visual Studio Team Services를 사용 하 여 Azure 서비스 패브릭 응용 프로그램에 대 한 배포를 구성 합니다.  기존 서비스 패브릭 응용 프로그램에 필요한, hello 응용 프로그램에서 만든 [.NET 응용 프로그램 빌드](service-fabric-tutorial-create-dotnet-app.md) 예제로 사용 합니다.

에서는 hello 계열의 세 부분에 학습 하는 방법:

> [!div class="checklist"]
> * 소스 제어 tooyour 프로젝트 추가
> * Team Services에서 빌드 정의 만들기
> * Team Services에서 릴리스 정의 만들기
> * 응용 프로그램 자동 배포 및 업그레이드

이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * [.NET Service Fabric 응용 프로그램 빌드](service-fabric-tutorial-create-dotnet-app.md)
> * [Hello 응용 프로그램 tooa 원격 클러스터 배포](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Visual Studio Team Services를 사용하여 CI/CD 구성

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에:
- Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.
- [Visual Studio 2017 설치](https://www.visualstudio.com/) hello를 설치 하 고 **Azure 개발** 및 **ASP.NET 및 웹 개발** 작업 합니다.
- [Hello 서비스 패브릭 SDK 설치](service-fabric-get-started.md)
- 예를 들어 [이 자습서를 따라](service-fabric-tutorial-create-dotnet-app.md) Service Fabric 응용 프로그램을 만듭니다. 
- 예를 들어 [이 자습서를 따라](service-fabric-tutorial-create-cluster-azure-ps.md) Windows Service Fabric 클러스터를 Azure에 만듭니다.
- [Team Services 계정](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)을 만듭니다.

## <a name="download-hello-voting-sample-application"></a>Hello 응답 샘플 응용 프로그램 다운로드
hello 응답 예제 응용 프로그램을 작성 하지 않은 경우 [이 자습서 시리즈의 1 부](service-fabric-tutorial-create-dotnet-app.md)를 다운로드할 수 있습니다. 명령 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>게시 프로필 준비
이제 [응용 프로그램을 만든](service-fabric-tutorial-create-dotnet-app.md) 있고 [hello 응용 프로그램 tooAzure 배포](service-fabric-tutorial-deploy-app-to-party-cluster.md), 연속 통합을 준비 tooset 넌입니다.  첫째, Team Services 내에서 실행 되는 hello 배포 프로세스에서 사용 하기 위해 응용 프로그램 내에서 게시 프로필을 준비 합니다.  게시 프로필 hello 이전에 만든 구성된 tootarget hello 클러스터 여야 합니다.  Visual Studio를 시작하고 기존 Service Fabric 응용 프로그램 프로젝트를 엽니다.  **솔루션 탐색기**hello 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시...** .

예를 들어 클라우드, 연속 통합 워크플로에 대 한 응용 프로그램 프로젝트 toouse 프로그램 내에서 대상 프로필을 선택 합니다.  Hello 클러스터 연결 끝점을 지정 합니다.  Hello 확인 **업그레이드 hello 응용 프로그램** 확인란 Team Services에서 각 배포에 대 한 응용 프로그램 업그레이드 수 있도록 합니다.  Hello 클릭 **저장** 하이퍼링크 toosave hello 설정 toohello 게시 프로필을 클릭 한 다음 **취소** tooclose hello 대화 상자.  

![푸시 프로필][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Visual Studio 솔루션 tooa 새 Team Services Git 리포지토리의 공유
생성할 수 있도록 Team Services에서 tooa 팀 프로젝트 빌드 응용 프로그램 소스 파일을 공유 합니다.  

선택 하 여 프로젝트에 대 한 새 로컬 Git 리포지토리를 만들 **tooSource 컨트롤 추가** -> **Git** hello 오른쪽 아래 모서리의 Visual Studio에서 hello 상태 표시줄에 있습니다. 

Hello에 **푸시** 의 **팀 탐색기**선택, hello **Git 리포지토리를 게시** 단추 **tooVisual Studio Team Services 푸시**합니다.

![Git 리포지토리 푸시][push-git-repo]

사용자의 전자 메일을 확인 하 고 hello에서 계정을 선택 **Team Services 도메인** 드롭 다운 합니다. 리포지토리 이름을 입력하고 **리포지토리 게시**를 선택합니다.

![Git 리포지토리 푸시][publish-code]

Hello 리포지토리에 게시 hello 로컬 리포지토리 이름이 hello로 계정에서 새 팀 프로젝트를 만듭니다. 기존 팀 프로젝트에 toocreate hello 리포지토리 클릭 **고급** 다음 너무**리포지토리** 이름을 지정 하 고 팀 프로젝트를 선택 합니다. 선택 하 여 hello 웹에서 코드를 볼 수 **hello 웹에서 참조**합니다.

## <a name="configure-continuous-delivery-with-vsts"></a>VSTS를 사용한 지속적인 업데이트 구성
Team Services 빌드 정의는 순차적으로 실행되는 빌드 단계 집합으로 구성된 워크플로를 설명합니다. 서비스 패브릭 응용 프로그램 패키지를 다른 아티팩트, toodeploy tooa 서비스 패브릭 클러스터를 생성 하는 빌드 정을 만듭니다. [Team Services 빌드 정의](https://www.visualstudio.com/docs/build/define/create)에 대해 자세히 알아봅니다. 

Team Services 릴리스 정의는 응용 프로그램 패키지 tooa 클러스터를 배포 하는 워크플로에 대해 설명 합니다. Hello 빌드 정의 함께 사용 하 고 릴리스 정의 클러스터에서 실행 중인 응용 프로그램과 소스 파일 tooending로 시작 하는 hello 전체 워크플로 실행 합니다. Team Services [릴리스 정의](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)에 대해 자세히 알아봅니다.

### <a name="create-a-build-definition"></a>빌드 정의 만들기
웹 브라우저를 열고 tooyour 새 팀 프로젝트에서 이동: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting 합니다. 

선택 hello **빌드 및 릴리스** 탭 한 다음 **빌드**, 다음 **+ 새 정의**합니다.  **´ ï ´**선택, hello **Azure 서비스 패브릭 응용 프로그램** 템플릿을 **적용**합니다. 

![빌드 템플릿 선택][select-build-template] 

.NET Core 프로젝트를 포함 하는 응용 프로그램 투표 hello, 하므로 hello 종속성을 복원 하는 작업을 추가 합니다. Hello에 **작업** 보기를 **+ 추가 작업** hello 왼쪽 아래에 있습니다. "명령줄" toofind hello 명령줄 작업을 검색 한 다음 클릭 **추가**합니다. 

![작업 추가][add-task] 

Hello 새 작업 입력 "dotnet.exe 실행"에서 **표시 이름**, "dotnet.exe"에서 **도구**, 및의 "restore" **인수**합니다. 

![새 작업][new-task] 

Hello에 **트리거** 보기에서 hello **이 트리거를 사용 하도록 설정** 에서 전환 **연속 통합**합니다. 

선택 **저장 후 큐** hello로 "VS2017 호스트"를 입력 하 고 **에이전트 큐**합니다. 선택 **큐** toomanually 빌드를 시작 합니다.  푸시 또는 체크 인 시 트리거도 빌드합니다.

toocheck 빌드 진행률, 스위치 toohello **빌드** 탭 합니다.  Hello 빌드 성공적으로 실행 되는지 확인 한 응용 프로그램 tooa 클러스터를 배포 하는 릴리스 정의 정의 합니다. 

### <a name="create-a-release-definition"></a>릴리스 정의 만들기  

선택 hello **빌드 및 릴리스** 탭 한 다음 **릴리스**, 다음 **+ 새 정의**합니다.  **만들기 릴리스 정의**선택, hello **Azure 서비스 패브릭 배포** hello 목록과 클릭에서 템플릿을 **다음**합니다.  선택 hello **빌드** hello 확인, 소스 **연속 배포** 고 클릭 **만들기**합니다. 

Hello에 **환경** 보려면 클릭 하십시오. **추가** 의 오른쪽 toohello **클러스터 연결**합니다.  Hello 클러스터에 대 한 "mysftestcluster", "tcp://mysftestcluster.westus.cloudapp.azure.com:19000" hello Azure Active Directory 또는 인증서 자격 증명 및 클러스터 끝점의 연결 이름을 지정 합니다. Azure Active Directory 자격 증명에 대 한 hello에 toouse tooconnect toohello 클러스터를 구축할 hello 자격 증명을 정의 **Username** 및 **암호** 필드입니다. 인증서 기반 인증에 대 한 hello에 hello 클라이언트 인증서 파일의 hello Base64 인코딩을 정의 **클라이언트 인증서** 필드입니다.  해당 필드는 방법에 대 한 정보에 hello 도움말 팝업을 참조 하십시오. 해당 값을 tooget 합니다.  인증서가 암호 보호 하는 경우 hello 암호 hello에서 정의 **암호** 필드입니다.  클릭 **저장** toosave hello 릴리스 정의 합니다.

![클러스터 연결 추가][add-cluster-connection] 

**에이전트에서 실행**을 선택한 후 **배포 큐**의 **호스팅된 VS2017**을 클릭합니다. 클릭 **저장** toosave hello 릴리스 정의 합니다.

![에이전트에서 실행][run-on-agent]

선택 **릴리스 +** -> **릴리스 만들기** -> **만들기** toomanually 릴리스를 만듭니다.  Hello 배포 성공 hello 클러스터에서 실행 중인 hello 응용 프로그램을 확인 합니다.  웹 브라우저를 열고 너무 이동[http://mysftestcluster.westus.cloudapp.azure.com:19080/탐색기/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)합니다.  Hello 응용 프로그램 버전,이 예제에서는 "1.0.0.20170616.3" note 합니다. 

## <a name="commit-and-push-changes-trigger-a-release"></a>변경 내용 커밋 및 푸시, 릴리스 트리거
연속 통합 파이프라인 hello tooverify 확인 tooTeam 서비스에 일부 코드를 변경 하 여 작동 합니다.    

코드를 작성하면 Visual Studio에서 변경 내용을 자동으로 추적합니다. 변경 내용 아이콘 (보류 중인 hello를 선택 하 여 변경 내용을 tooyour 로컬 Git 리포지토리를 커밋![Pending][pending])에서 hello 상태 표시줄 오른쪽 hello 아래에 있습니다.

Hello에 **변경** 보려면 팀 탐색기에서 업데이트를 설명 하는 메시지를 추가 하 고 변경 내용을 커밋합니다.

![모두 커밋][changes]

선택 hello 게시 되지 않은 변경 상태 표시줄 아이콘 (![변경 내용이 게시 되지 않은][unpublished-changes]) 또는 팀 탐색기에서 동기화 뷰 환영 합니다. 선택 **푸시** tooupdate Team Services/TFS에서 사용자 코드입니다.

![변경 내용 푸시][push]

Hello 변경 tooTeam 푸시 서비스는 자동으로 트리거 빌드 됩니다.  Hello 빌드 정의 성공적으로 완료 되 면 릴리스 자동으로 생성 하 고 hello 클러스터에서 hello 응용 프로그램 업그레이드를 시작 합니다.

toocheck 빌드 진행률, 스위치 toohello **빌드** 탭에서 **팀 탐색기** Visual Studio에서.  Hello 빌드 성공적으로 실행 되는지 확인 한 응용 프로그램 tooa 클러스터를 배포 하는 릴리스 정의 정의 합니다.

Hello 배포 성공 hello 클러스터에서 실행 중인 hello 응용 프로그램을 확인 합니다.  웹 브라우저를 열고 너무 이동[http://mysftestcluster.westus.cloudapp.azure.com:19080/탐색기/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)합니다.  Hello 응용 프로그램 버전,이 예제에서는 "1.0.0.20170815.3" note 합니다.

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Hello 응용 프로그램 업데이트
Hello 응용 프로그램에서 코드 변경 합니다.  저장 하 고 hello 이전 단계를 수행 hello 변경 내용을 커밋하십시오.

hello 업그레이드 되 면 hello 응용 프로그램을 시작, 서비스 패브릭 탐색기에 hello 업그레이드 진행률을 볼 수 있습니다.

![Service Fabric Explorer][sfx2]

응용 프로그램 업그레이드: hello 몇 분 정도 걸릴 수 있습니다. Hello 업그레이드가 완료 되 면 hello 다음 버전 hello 응용 프로그램 실행 됩니다.  이 예제에서는 "1.0.0.20170815.4"입니다.

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 소스 제어 tooyour 프로젝트 추가
> * 빌드 정의 만들기
> * 릴리스 정의 만들기
> * 응용 프로그램 자동 배포 및 업그레이드

응용 프로그램을 배포 하 고 연속 통합을 구성 했으므로 hello 다음을 시도해 보십시오.
- [앱 업그레이드](service-fabric-application-upgrade.md)
- [앱 테스트](service-fabric-testability-overview.md) 
- [모니터링 및 진단](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png