---
title: "Azure에서.NET 서비스 패브릭 응용 프로그램 aaaCreate | Microsoft Docs"
description: "Hello 서비스 패브릭 빠른 시작 예제를 사용 하 여 Azure에 대 한.NET 응용 프로그램을 만듭니다."
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
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Azure에서 .NET Service Fabric 응용 프로그램 만들기
Azure Service Fabric은 확장성 있고 안정성이 뛰어난 마이크로 서비스 및 컨테이너를 배포 및 관리하기 위한 분산 시스템 플랫폼입니다. 

이 퀵 스타트의 표시 방법을 toodeploy 프로그램 첫 번째.NET 응용 프로그램 tooService 패브릭 합니다. 완료 되 면 hello 클러스터에서 상태 저장 백 엔드 서비스의 응답 결과 저장 하는 프런트 엔드는 ASP.NET Core 웹 응용 프로그램을 응답 해야 합니다.

![응용 프로그램 스크린샷](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

이 응용 프로그램을 사용하여 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * .NET 및 Service Fabric을 사용하여 응용 프로그램 만들기
> * 웹 프런트 엔드로 ASP.NET core 사용
> * 상태 저장 서비스에 응용 프로그램 데이터 저장
> * 로컬에서 응용 프로그램 디버그
> * Azure의 hello 응용 프로그램 tooa 클러스터 배포
> * 여러 노드에 걸쳐 확장 hello 응용 프로그램
> * 응용 프로그램 롤링 업그레이드 수행

## <a name="prerequisites"></a>필수 조건
toocomplete이 빠른이 시작:
1. [Visual Studio 2017 설치](https://www.visualstudio.com/) hello로 **Azure 개발** 및 **ASP.NET 및 웹 개발** 작업 합니다.
2. [Git 설치](https://git-scm.com/)
3. [Hello Microsoft Azure Service Fabric SDK 설치](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. Hello 명령 tooenable Visual Studio toodeploy toohello 로컬 서비스 패브릭 클러스터를 다음을 실행 합니다.
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a>Hello 샘플 다운로드
명령 창에서 hello 명령 tooclone hello 샘플 응용 프로그램 저장소 tooyour 로컬 컴퓨터에 다음을 실행 합니다.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행
Hello 시작 메뉴에서에서 hello Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다. 순서 tooattach hello 디버거 tooyour 서비스를 관리자 권한으로 Visual Studio toorun이 필요합니다.

열기 hello **Voting.sln** hello 리포지토리를 복제에서 Visual Studio 솔루션입니다.

toodeploy hello 응용 프로그램 키를 눌러 **F5**합니다.

> [!NOTE]
> hello 처음으로 실행 하 고 배포 hello 응용 프로그램을 Visual Studio 디버깅에 대 한 로컬 클러스터를 만듭니다. 이 작업에는 다소 시간이 걸릴 수 있습니다. hello 클러스터 만들기 상태 hello Visual Studio 출력 창에 표시 됩니다.

Hello 배포 완료 되 면 브라우저를 시작 하 고이 페이지를 열려면: `http://localhost:8080` -hello의 웹 프런트 엔드 hello 응용 프로그램입니다.

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

이제 투표 옵션 집합을 추가하고 투표 하기를 시작할 수 있습니다. hello 응용 프로그램 실행 하 고 별도 데이터베이스에 대 한 hello 필요 없이 서비스 패브릭 클러스터의 모든 데이터를 저장 합니다.

## <a name="walk-through-hello-voting-sample-application"></a>샘플 응용 프로그램 투표 hello 안내
두 서비스의 응용 프로그램 투표 hello 구성 됩니다.
- 웹 프런트 엔드 서비스 (VotingWeb)-An ASP.NET Core 웹 hello 웹 페이지를 사용 되는 프런트 엔드 서비스 및 노출 웹 Api toocommunicate hello 백 엔드 서비스와 함께 합니다.
- 백 엔드 서비스 (VotingData)-노출 API toostore hello 투표를 신뢰할 수 있는 사전으로 인해 디스크에 저장 되는 ASP.NET Core 웹 서비스입니다.

![응용 프로그램 다이어그램](./media/service-fabric-quickstart-dotnet/application-diagram.png)

다음 hello 응용 프로그램 hello에 투표 이벤트가 발생 합니다.
1. JavaScript은 hello 웹 프런트 엔드 서비스 hello 투표 요청 toohello web을 API HTTP PUT 요청으로 보냅니다.

2. hello 웹 프런트 엔드 서비스 프록시 toolocate를 사용 하 여 하 고는 HTTP PUT 요청 toohello 백 엔드 서비스에 전달 합니다.

3. hello 백 엔드 서비스는 hello 들어오는 요청을 사용 하 고 저장소 hello hello 클러스터 내에서 복제 된 toomultiple 노드를 가져오고 디스크에 저장 하는 신뢰할 수 있는 사전에서 결과 업데이트 합니다. 모든 hello 응용 프로그램의 데이터는 데이터베이스가 필요 하므로 hello 클러스터에 저장 됩니다.

## <a name="debug-in-visual-studio"></a>Visual Studio에서 디버그
Visual Studio에서 응용 프로그램을 디버깅할 때 로컬 Service Fabric 개발 클러스터를 사용합니다. Hello 옵션 tooadjust 디버깅 환경을 tooyour 시나리오를 해야합니다. 이 응용 프로그램에서는 신뢰할 수 있는 사전을 사용하여 데이터를 백 엔드 서비스에 저장합니다. Visual Studio hello 디버거를 중지 하는 경우 기본 당 hello 응용 프로그램을 제거 합니다. Hello 백 엔드에 hello 데이터 hello 응용 프로그램을 제거 하면 서비스 tooalso 제거할 수 있습니다. 디버깅 세션 간에 toopersist hello 데이터를 hello 변경할 수 있습니다 **응용 프로그램 디버그 모드** hello 속성으로 **응답** Visual Studio에서 프로젝트.

hello 코드에서는 다음 단계 완료 hello toolook에 어떤 상황이 발생 합니다.
1. 열기 hello **VotesController.cs** hello 웹 API에에서 중단점을 설정 하 고 파일 **배치** 메서드 (47 선)-hello Visual Studio의 솔루션 탐색기에서에서 hello 파일을 검색할 수 있습니다.

2. 열기 hello **VoteDataController.cs** 파일을 웹 API이 중단점을 설정할 **배치** 메서드 (라인 50).

3. Toohello 브라우저 돌아가서 투표 옵션을 클릭 하거나 새 응답 옵션을 추가 합니다. Hello hello 웹 프런트 엔드에서 api 컨트롤러의 첫 번째 중단점을 누르면 있습니다.
    - 이 hello 브라우저에서 JavaScript hello hello 프런트 엔드 서비스에 요청 toohello web API 컨트롤러를 보냅니다.
    
    ![투표 프런트 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - 백 엔드 서비스에 대 한 hello URL toohello ReverseProxy 생성 먼저 **(1)**합니다.
    - म ध hello HTTP PUT 요청 toohello ReverseProxy 다음 **(2)**합니다.
    - 마지막으로 hello 반환 hello 응답 hello 백 엔드 서비스 toohello 클라이언트로부터 **(3)**합니다.

4. 키를 눌러 **F5** toocontinue
    - 현재 위치는 hello 중단점의 hello 백 엔드 서비스입니다.
    
    ![투표 백 엔드 서비스 추가](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - Hello hello 메서드 첫 번째 줄에 **(1)** hello 사용 하 여 `StateManager` tooget 라는 신뢰할 수 있는 사전 추가 또는 `counts`합니다.
    - 신뢰할 수 있는 사전에 있는 값과의 모든 상호 작용에는 트랜잭션이 필요하며 using 문**(2)**으로 트랜잭션이 만들어집니다.
    - Hello 트랜잭션에서 다음 업데이트 옵션 투표 hello에 대 한 hello 관련 키의 hello 값 및 커밋 작업 hello **(3)**합니다. Hello 커밋하면 메서드가 반환 hello 데이터 hello 사전에서 업데이트 되 고 tooother hello 클러스터 노드를 복제 합니다. 이제 hello 데이터는 hello 클러스터에 안전 하 게 저장 하 고 hello 백 엔드 서비스 데 계속 사용할 수 있는 hello 데이터 tooother 노드를 장애 조치할 수 있습니다.
5. 키를 눌러 **F5** toocontinue

세션 키를 눌러 디버깅 toostop hello **Shift + f 5**합니다.

## <a name="deploy-hello-application-tooazure"></a>Hello 응용 프로그램 tooAzure 배포
toodeploy hello 응용 프로그램 tooa Azure의 클러스터, 클러스터 또는 타사 클러스터를 사용 하 여 사용자 고유의 toocreate 선택할 수 있습니다.

파티 클러스터는 무료, 제한 시간 서비스 패브릭 클러스터 Azure에서 호스트 및 누구 든 지 수 응용 프로그램을 배포 하 고 hello 플랫폼에 대 한 자세한 내용은 hello 서비스 패브릭 팀에서 실행 합니다. tooget 액세스 tooa 파티 클러스터 [hello 지침에 따라](http://aka.ms/tryservicefabric)합니다. 

사용자 고유의 클러스터를 만드는 방법은 [Azure에서 첫 번째 Service Fabric 클러스터 만들기](service-fabric-get-started-azure-cluster.md)를 참조하세요.

> [!Note]
> hello 웹 프런트 엔드 서비스는 들어오는 트래픽에 대해 포트 8080에서 구성 된 toolisten 합니다. 클러스터에 대해 포트가 열려 있는지 확인합니다. Hello 파티 클러스터를 사용 하는 경우이 포트가 열려 있습니다.
>

### <a name="deploy-hello-application-using-visual-studio"></a>Visual Studio를 사용 하 여 hello 응용 프로그램 배포
Hello 응용 프로그램 준비 되 면 했으므로 tooa 클러스터 Visual Studio에서 직접 배포할 수 있습니다.

1. 마우스 오른쪽 단추로 클릭 **응답** hello 솔루션 탐색기에서 선택한 **게시**합니다. hello 게시 대화 상자가 나타납니다.

    ![[게시] 대화 상자](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. Hello에 hello 클러스터의 hello 연결 끝점을 입력 **연결 끝점** 필드를 클릭 **게시**합니다. Hello 클러스터 파티, 등록할 때 hello 연결 끝점 hello 브라우저에서 제공 됩니다. - 예를 들면 `winh1x87d1d.westus.cloudapp.azure.com:19000`입니다.

3. 브라우저를 형식 hello 클러스터 주소-예를 들어 열고 `http://winh1x87d1d.westus.cloudapp.azure.com`합니다. 이제 Azure의 hello 클러스터에서 실행 되는 hello 응용 프로그램을 표시 됩니다.

![응용 프로그램 프런트 엔드](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>클러스터에서 응용 프로그램 및 서비스 크기 조정
서비스 패브릭 서비스는 hello 서비스에서 hello 부하가 변경에 대 한 클러스터 tooaccommodate 쉽게 확장할 수 있습니다. Hello hello 클러스터에서 실행 되는 인스턴스 수를 변경 하 여 서비스를 확장 합니다. 서비스의 크기를 조정하는 여러 가지 방법이 있으며 PowerShell 또는 Service Fabric CLI(sfctl)의 스크립트 또는 명령을 사용할 수 있습니다. 이 예제에서는 Service Fabric Explorer를 사용합니다.

서비스 패브릭 탐색기 모든 서비스 패브릭 클러스터에서 실행 되 고 예를 들어 toohello HTTP 클러스터 관리 포트 (19080)를 검색 하 여 브라우저에서 액세스할 수 `http://winh1x87d1d.westus.cloudapp.azure.com:19080`합니다.

tooscale hello 웹 프런트 엔드 서비스, 다음 단계 hello지 않습니다.

1. 클러스터에서 Service Fabric Explorer를 엽니다(예: `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).
2. Hello 줄임표 (...) 다음 toohello 클릭 **패브릭: / 응답/VotingWeb** 노드 treeview hello와 선택 **배율 서비스**합니다.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    이제 tooscale hello hello 웹 프런트 엔드 서비스의 인스턴스 수를 선택할 수 있습니다.

3. Hello 번호를 너무 변경**2** 클릭 **배율 서비스**합니다.
4. Hello 클릭 **패브릭: / 응답/VotingWeb** 의 노드 트리 뷰 hello 고 hello 파티션 노드 (GUID로 표현 됨)를 확장 합니다.

    ![Service Fabric Explorer Scale Service](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    이제 hello 서비스에는 두 개의 인스턴스에 및 hello 인스턴스가에서 실행 하는 노드를 확인 하면 hello 트리 보기에서 볼 수 있습니다.

이 간단한 관리 작업에 의해 우리의 프런트 엔드 서비스 tooprocess 사용자 부하에 대해 사용할 수 있는 hello 리소스 배가. 이것은 안정적으로 실행 하는 서비스 toohave의 여러 인스턴스가 필요 하지 않은 중요 한 toounderstand 것 합니다. 서비스가 실패 하면 서비스 패브릭 되도록 hello 클러스터에서 새 서비스 인스턴스를 실행 합니다.

## <a name="perform-a-rolling-application-upgrade"></a>응용 프로그램 롤링 업그레이드 수행
새 업데이트 tooyour 응용 프로그램을 배포할 때는 안전한 방식으로 서비스 패브릭 hello 업데이트 롤업 합니다. 롤링 업그레이드를 사용하면 업그레이드하는 동안 가동 중지 시간이 없으며 오류가 발생하면 자동화된 롤백을 수행합니다.

tooupgrade hello 응용 프로그램, 다음 hello지 않습니다.

1. 열기 hello **Index.cshtml** 파일에서 Visual Studio-hello Visual Studio의 솔루션 탐색기에서에서 hello 파일을 검색 합니다.
2. 예를 들어-일부 텍스트를 추가 하 여 hello 페이지 hello 머리글을 변경 합니다.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. Hello 파일을 저장 합니다.
4. 마우스 오른쪽 단추로 클릭 **응답** hello 솔루션 탐색기에서 선택한 **게시**합니다. hello 게시 대화 상자가 나타납니다.
5. Hello 클릭 **매니페스트 버전** hello 서비스와 응용 프로그램 단추 toochange hello 버전입니다.
6. 변경 hello 버전의 hello **코드** 요소 아래의 **VotingWebPkg** 너무 "2.0.0" 예를 들어 클릭 **저장**합니다.

    ![[버전 변경] 대화 상자](./media/service-fabric-quickstart-dotnet/change-version.png)
7. Hello에 **서비스 패브릭 응용 프로그램 게시** 대화 상자, 확인 hello 업그레이드 hello 응용 프로그램 확인란 및 클릭 **게시**합니다.

    ![게시 대화 상자 업그레이드 설정](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. 브라우저를 열고 toohello 클러스터 주소에 포트 19080-예를 들어 찾아보기 `http://winh1x87d1d.westus.cloudapp.azure.com:19080`합니다.
9. Hello 클릭 **응용 프로그램** hello 트리 뷰에서 노드 차례로 **진행 중인 업그레이드** hello 오른쪽 창에서. 사용자 표시 계산 방법 hello 업그레이드 12 hello 업그레이드 도메인을 통해 클러스터의 각 도메인 정상 인지 toohello 계속 진행 하기 전에 다음 있습니다.
    ![Service Fabric Explorer에서 업그레이드 보기](./media/service-fabric-quickstart-dotnet/upgrading.png)

    서비스 패브릭 업그레이드에 안전 하 게 대기 hello 클러스터의 각 노드에서 hello 서비스를 업그레이드 한 후 2 분 여 합니다. Hello 전체 update tootake 약 8 분을 기대 합니다.

10. Hello 업그레이드가 실행 되는 동안에 hello 응용 프로그램을 여전히 사용할 수 있습니다. Hello 클러스터에서 실행 되는 hello 서비스의 두 인스턴스를 가지기 때문에 여전히 hello 이전 버전을 가져올 수 있습니다 다른 동안 업그레이드 된 버전의 hello 응용 프로그램 발생할 수 일부 사용자의 요청.

## <a name="next-steps"></a>다음 단계
이 빠른 시작에서는 다음을 수행하는 방법을 알아보았습니다.

> [!div class="checklist"]
> * .NET 및 Service Fabric을 사용하여 응용 프로그램 만들기
> * 웹 프런트 엔드로 ASP.NET core 사용
> * 상태 저장 서비스에 응용 프로그램 데이터 저장
> * 로컬에서 응용 프로그램 디버그
> * Azure의 hello 응용 프로그램 tooa 클러스터 배포
> * 여러 노드에 걸쳐 확장 hello 응용 프로그램
> * 응용 프로그램 롤링 업그레이드 수행

서비스 패브릭 및.NET에 대해 자세히 toolearn이이 자습서에서 살펴보겠습니다.
> [!div class="nextstepaction"]
> [Service Fabric에서 .NET 응용 프로그램](service-fabric-tutorial-create-dotnet-app.md)