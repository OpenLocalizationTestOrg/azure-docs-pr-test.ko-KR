---
title: "Azure에서 .NET Service Fabric 응용 프로그램 만들기 | Microsoft Docs"
description: "Service Fabric 빠른 시작 샘플을 사용하여 Azure에 대한 .NET 응용 프로그램을 만듭니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: d11b9af982112db8ba94b62110c18be843f1abb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Azure에서 .NET Service Fabric 응용 프로그램 만들기
Azure Service Fabric은 확장성 있고 안정성이 뛰어난 마이크로 서비스 및 컨테이너를 배포 및 관리하기 위한 분산 시스템 플랫폼입니다. 

이 빠른 시작에서는 Service Fabric에 첫 번째 .NET 응용 프로그램을 배포하는 방법을 보여 줍니다. 완료하면 투표 결과를 클러스터의 상태 저장 백 엔드 서비스에 저장하는 ASP.NET Core 웹 프런트 엔드가 있는 투표 응용 프로그램이 생깁니다.

![응용 프로그램 스크린샷](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

이 응용 프로그램을 사용하여 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * .NET 및 Service Fabric을 사용하여 응용 프로그램 만들기
> * 웹 프런트 엔드로 ASP.NET core 사용
> * 상태 저장 서비스에 응용 프로그램 데이터 저장
> * 로컬에서 응용 프로그램 디버그
> * Azure에서 응용 프로그램을 클러스터에 배포
> * 응용 프로그램을 여러 노드에 걸쳐 스케일 아웃
> * 응용 프로그램 롤링 업그레이드 수행

## <a name="prerequisites"></a>필수 조건
이 빠른 시작을 완료하려면 다음이 필요합니다.
1. **Azure 개발**과 **ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017 설치](https://www.visualstudio.com/)
2. [Git 설치](https://git-scm.com/)
3. [Microsoft Azure Service Fabric SDK 설치](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. 다음 명령을 실행하여 Visual Studio에서 로컬 Service Fabric 클러스터에 배포하도록 합니다.
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-the-sample"></a>샘플 다운로드
명령 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-the-application-locally"></a>로컬에서 응용 프로그램 실행
시작 메뉴에서 Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 디버거를 서비스에 연결하려면 관리자 권한으로 Visual Studio를 실행해야 합니다.

복제한 리포지토리에서 **Voting.sln** Visual Studio 솔루션을 엽니다.

응용 프로그램을 배포하려면 **F5** 키를 누릅니다.

> [!NOTE]
> 처음으로 응용 프로그램을 실행하고 배포할 때 Visual Studio는 디버깅을 위해 로컬 클러스터를 만듭니다. 이 작업에는 다소 시간이 걸릴 수 있습니다. Visual Studio 출력 창에 클러스터 생성 상태가 표시됩니다.

배포가 완료되면 브라우저를 시작하고 응용 프로그램의 웹 프런트 엔드인 페이지(`http://localhost:8080`)를 엽니다.

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

이제 투표 옵션 집합을 추가하고 투표 하기를 시작할 수 있습니다. 응용 프로그램이 실행되고 모든 데이터가 Service Fabric 클러스터에 저장되며 별도의 데이터베이스가 필요하지 않습니다.

## <a name="walk-through-the-voting-sample-application"></a>투표 응용 프로그램 예제 연습
투표 응용 프로그램은 두 가지 서비스로 구성됩니다.
- 웹 프런트 엔드 서비스(VotingWeb) - ASP.NET Core 웹 프런트 엔드 서비스로, 웹 페이지를 제공하며 백 엔드 서비스와 통신하기 위한 Web API를 공개합니다.
- 백 엔드 서비스(VotingData) - ASP.NET Core 웹 서비스로, 투표 결과를 디스크에 보관된 신뢰할 수 있는 사전에 저장하기 위한 API를 공개합니다.

![응용 프로그램 다이어그램](./media/service-fabric-quickstart-dotnet/application-diagram.png)

응용 프로그램에 투표하는 경우 다음 이벤트가 발생합니다.
1. JavaScript가 투표 요청을 웹 프런트 엔드 서비스의 Web API에 HTTP PUT 요청으로 보냅니다.

2. 웹 프런트 엔드 서비스는 프록시를 사용하여 HTTP PUT 요청을 찾아 백 엔드 서비스에 전달합니다.

3. 백 엔드 서비스는 들어오는 요청을 받고 업데이트된 결과를, 클러스터 내의 여러 노드에 복제되고 디스크에 보관된 신뢰할 수 있는 사전에 저장합니다. 응용 프로그램의 모든 데이터가 클러스터에 저장되므로 데이터베이스가 필요하지 않습니다.

## <a name="debug-in-visual-studio"></a>Visual Studio에서 디버그
Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다. 사용자 시나리오에 대해 디버깅 환경을 조정하는 옵션이 있습니다. 이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다. Visual Studio는 디버거를 중지하는 경우 기본값에 대해 응용 프로그램을 제거합니다. 응용 프로그램을 제거하면 백 엔드 서비스의 데이터도 제거됩니다. 디버깅 세션 간에 데이터를 유지하려면 **응용 프로그램 디버그 모드**를 Visual Studio에서 **Voting** 프로젝트의 속성으로 변경할 수 있습니다.

코드에서 수행되는 작업을 살펴보려면 다음 단계를 완료합니다.
1. **VotesController.cs** 파일을 열고 Web API의 **Put** 메서드(47줄)에서 중단점을 설정합니다. Visual Studio의 솔루션 탐색기에서 파일을 검색할 수 있습니다.

2. **VoteDataController.cs** 파일을 열고 이 Web API의 **Put** 메서드(50줄)에서 중단점을 설정합니다.

3. 브라우저로 돌아가서 투표 옵션을 클릭하거나 새 투표 옵션을 추가합니다. 웹 프런트 엔드의 api 컨트롤러에서 첫 번째 중단점에 도달합니다.
    - 여기서 브라우저의 JavaScript가 프런트 엔드 서비스의 Web API 컨트롤러에 요청을 보냅니다.
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - 먼저 백 엔드 서비스 **(1)**에 대해 ReverseProxy에 대한 URL을 구성해야 합니다.
    - 그런 다음 ReverseProxy **(2)**에 HTTP PUT 요청을 보냅니다.
    - 마지막으로로 백 엔드 서비스로부터 클라이언트 **(3)**에 응답을 반환합니다.

4. 계속하려면 **F5** 키를 누릅니다.
    - 이제 백 엔드 서비스의 중단점에 있습니다.
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - 메서드의 첫 번째 줄**(1)**에서는 신뢰할 수 있는 사전 `counts`를 가져오거나 추가하기 위해 `StateManager`를 사용합니다.
    - 신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.
    - 트랜잭션에서는 투표 옵션에 대한 관련 키 값을 업데이트하고 작업을 커밋합니다**(3)**. 커밋 메서드가 반환되면 사전에 데이터가 업데이트되고 클러스터의 다른 노드에 복제됩니다. 이제 데이터는 클러스터에 안전하게 저장되며 백 엔드 서비스는 데이터를 계속 제공하면서 다른 노드로 장애 조치할 수 있습니다.
5. 계속하려면 **F5** 키를 누릅니다.

디버깅 세션을 중지하려면 **Shift+F5** 키를 누릅니다.

## <a name="deploy-the-application-to-azure"></a>Azure에 응용 프로그램 배포
응용 프로그램을 Azure의 클러스터에 배포하려면 사용자 고유의 클러스터를 만들거나 Party 클러스터를 만들도록 선택할 수 있습니다.

Party 클러스터는 평가판으로, Azure에서 호스트되고 Service Fabric 팀이 실행하는 제한 시간 Service Fabric 클러스터입니다. 여기서 누구나 응용 프로그램을 배포하고 플랫폼에 대해 알아볼 수 있습니다. 파티 클러스터에 대한 액세스 권한을 얻으려면 [지침에 따릅니다](http://aka.ms/tryservicefabric). 

사용자 고유의 클러스터를 만드는 방법은 [Azure에서 첫 번째 Service Fabric 클러스터 만들기](service-fabric-get-started-azure-cluster.md)를 참조하세요.

> [!Note]
> 웹 프런트 엔드 서비스는 들어오는 트래픽에 대해 포트 8080에서 수신 대기하도록 구성됩니다. 클러스터에 대해 포트가 열려 있는지 확인합니다. Party 클러스터를 사용하는 경우 이 포트가 열려 있습니다.
>

### <a name="deploy-the-application-using-visual-studio"></a>Visual Studio를 사용하여 응용 프로그램 배포
응용 프로그램이 준비되면 Visual Studio에서 클러스터에 직접 배포할 수 있습니다.

1. 솔루션 탐색기에서 **Voting**을 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다. [게시] 대화 상자가 나타납니다.

    ![[게시] 대화 상자](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. **연결 끝점** 필드에 클러스터의 연결 끝점을 입력하고 **게시**를 클릭합니다. Party 클러스터에 등록하면 연결 끝점이 브라우저에 제공됩니다. - 예를 들면 `winh1x87d1d.westus.cloudapp.azure.com:19000`입니다.

3. 브라우저를 열고 클러스터 주소에 입력합니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com`). 이제 Azure의 클러스터에서 실행 중인 응용 프로그램이 표시됩니다.

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>클러스터에서 응용 프로그램 및 서비스 크기 조정
Service Fabric 서비스는 해당 서비스에 대한 로드 변동량을 수용하도록 클러스터 간에 쉽게 크기를 조정할 수 있습니다. 클러스터에서 실행되는 인스턴스 수를 변경하여 서비스 크기를 조정합니다. 서비스의 크기를 조정하는 여러 가지 방법이 있으며 PowerShell 또는 Service Fabric CLI(sfctl)의 스크립트 또는 명령을 사용할 수 있습니다. 이 예제에서는 Service Fabric Explorer를 사용합니다.

Service Fabric Explorer는 모든 Service Fabric 클러스터에서 실행되고 클러스터 HTTP 관리 포트(19080)로 이동하여 브라우저에서 액세스할 수 있습니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).

웹 프런트 엔드 서비스의 크기를 조정하려면 다음 단계를 수행합니다.

1. 클러스터에서 Service Fabric Explorer를 엽니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).
2. 트리 뷰에서 **fabric:/Voting/VotingWeb** 노드 옆에 있는 줄임표(...)를 클릭하고 **Scale Service**를 선택합니다.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    이제 웹 프런트 엔드 서비스의 인스턴스 수를 조정하도록 선택할 수 있습니다.

3. 이 수를 **2**로 변경하고 **Scale Service**를 클릭합니다.
4. 트리 뷰에서 **fabric:/Voting/VotingWeb** 노드를 클릭하고 파티션 노드(GUID로 표현됨)를 확장합니다.

    ![Service Fabric Explorer Scale Service](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    이제 두 개의 인스턴스가 있는 서비스를 인스턴스가 실행되는 노드를 볼 수 있는 트리 뷰에서 볼 수 있습니다.

이 간단한 관리 작업으로 사용자 로드를 처리하는 프런트 엔드 서비스에 사용 가능한 리소스를 두 배로 증가시킬 수 있습니다. 서비스를 안정적으로 실행하기 위해 서비스의 여러 인스턴스가 필요하지 않다는 것을 이해하는 것이 중요합니다. 서비스가 실패하면 Service Fabric은 클러스터에서 새 서비스 인스턴스가 실행되는지 확인합니다.

## <a name="perform-a-rolling-application-upgrade"></a>응용 프로그램 롤링 업그레이드 수행
새 업데이트를 응용 프로그램에 배포할 때는 Service Fabric이 안전한 방식으로 업데이트를 공개합니다. 롤링 업그레이드를 사용하면 업그레이드하는 동안 가동 중지 시간이 없으며 오류가 발생하면 자동화된 롤백을 수행합니다.

응용 프로그램을 업그레이드하려면 다음을 수행합니다.

1. Visual Studio에서 **Index.cshtml** 파일을 엽니다. Visual Studio의 솔루션 탐색기에서 파일을 검색할 수 있습니다.
2. 예를 들어 일부 텍스트를 추가하여 페이지 머리글을 변경합니다.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. 파일을 저장합니다.
4. 솔루션 탐색기에서 **Voting**을 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다. [게시] 대화 상자가 나타납니다.
5. **매니페스트 버전** 단추를 클릭하여 서비스 및 응용 프로그램의 버전을 변경합니다.
6. **VotingWebPkg** 아래에서 **Code** 요소의 버전을, 예를 들어 “2.0.0”으로 변경하고 **저장**을 클릭합니다.

    ![[버전 변경] 대화 상자](./media/service-fabric-quickstart-dotnet/change-version.png)
7. **Service Fabric 응용 프로그램 게시** 대화 상자에서 [응용 프로그램 업그레이드] 확인란을 선택하고 **게시**를 클릭합니다.

    ![게시 대화 상자 업그레이드 설정](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. 브라우저를 열고 포트 19080에서 클러스터 주소로 이동합니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).
9. 트리 뷰의 **응용 프로그램** 노드를 클릭한 후 오른쪽 창에서 **Upgrades in Progress(진행 중인 업그레이드)**를 클릭합니다. 업그레이드가 클러스터에서 업그레이드 도메인을 어떻게 통과하고 다음으로 진행하기 전에 각 도메인 상태가 정상인지 확인하게 됩니다.
    ![Service Fabric Explorer에서 업그레이드 보기](./media/service-fabric-quickstart-dotnet/upgrading.png)

    Service Fabric에서는 클러스터의 각 노드에서 서비스를 업그레이드 한 후 2분 대기함으로써 안전하게 업그레이드합니다. 전체 업데이트에는 약 8분이 소요될 것으로 예상됩니다.

10. 업그레이드가 실행되는 동안 응용 프로그램을 계속 사용할 수 있습니다. 클러스터에서 실행되는 서비스에는 두 인스턴스가 있으므로 일부 요청은 응용 프로그램의 업그레이드된 버전을 가질 수 있는 반면 일부는 이전 버전을 가질 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 빠른 시작에서는 다음을 수행하는 방법을 알아보았습니다.

> [!div class="checklist"]
> * .NET 및 Service Fabric을 사용하여 응용 프로그램 만들기
> * 웹 프런트 엔드로 ASP.NET core 사용
> * 상태 저장 서비스에 응용 프로그램 데이터 저장
> * 로컬에서 응용 프로그램 디버그
> * Azure에서 응용 프로그램을 클러스터에 배포
> * 응용 프로그램을 여러 노드에 걸쳐 스케일 아웃
> * 응용 프로그램 롤링 업그레이드 수행

Service Fabric 및 .NET에 대해 자세히 알아보기 위해 다음 자습서를 살펴보겠습니다.
> [!div class="nextstepaction"]
> [Service Fabric에서 .NET 응용 프로그램](service-fabric-tutorial-create-dotnet-app.md)