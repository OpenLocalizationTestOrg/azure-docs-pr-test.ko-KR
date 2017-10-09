---
title: "aaaDebug Visual Studio에서 응용 프로그램 | Microsoft Docs"
description: "개발 하 고 로컬 개발 클러스터에 Visual Studio에서 디버깅 하 여 서비스의 hello 안정성 및 성능을 개선 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>로컬 서비스 패브릭 응용 프로그램 디버깅
로컬 컴퓨터 개발 클러스터에서 Azure 서비스 패브릭 응용 프로그램을 배포하고 디버그하여 시간과 비용을 절약할 수 있습니다. Visual Studio 2017 또는 Visual Studio 2015 hello 응용 프로그램 toohello 로컬 클러스터를 배포할 수 있으며 응용 프로그램의 hello 디버거 tooall 인스턴스를 자동으로 연결 합니다.

1. 로컬 개발 클러스터에 hello 단계에 따라 시작 [서비스 패브릭 개발 환경 설정](service-fabric-get-started.md)합니다.
2. **F5** 키를 누르거나 **디버그** > **디버깅 시작**을 클릭합니다.
   
    ![응용 프로그램 디버깅 시작][startdebugging]
3. Hello에 대 한 명령을 클릭 하 여 코드와 hello 응용 프로그램을 통해 단계에 중단점을 설정 **디버그** 메뉴.
   
   > [!NOTE]
   > Visual Studio 응용 프로그램의 tooall 인스턴스를 연결합니다. 단계별로 코드를 실행하는 동안 중단점은 동시 세션에서 발생하는 여러 프로세스에 히트될 수 있습니다. 공격을 각 중단점 조건 hello 스레드 ID 별로 만들거나 진단 이벤트를 사용 하 여 후 hello 중단점을 사용 하지 않도록 설정 해 보십시오.
   > 
   > 
4. hello **진단 이벤트** 실시간으로 진단 이벤트를 볼 수 있도록에 자동으로 창이 열립니다.
   
    ![실시간으로 진단 이벤트 보기][diagnosticevents]
5. Hello를 열 수도 있습니다 **진단 이벤트** 클라우드 탐색기에서 창.  **Service Fabric**에서 아무 노드를 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 보기**를 선택합니다.
   
    ![열기 hello 진단 이벤트 창][viewdiagnosticevents]
   
    추적 tooa 특정 서비스 또는 응용 프로그램과 toofilter를 원하는 경우에 해당 특정 서비스 또는 응용 프로그램에서 스트리밍 추적 사용 하도록 설정 하기만 합니다.
6. 자동으로 생성 하는 hello hello 진단 이벤트를 볼 수 **ServiceEventSource.cs** 파일 및 응용 프로그램 코드에서 호출 됩니다.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. hello **진단 이벤트** 창에서 필터링, 일시 중지 및 검사를 실시간으로 이벤트를 지원 합니다.  hello 필터는 해당 내용을 포함 하는 hello 이벤트 메시지의 간단한 문자열 검색 합니다.
   
    ![실시간으로 이벤트를 필터링, 일시 중지, 다시 시작 또는 검사합니다.][diagnosticeventsactions]
8. 서비스 디버깅은 다른 모든 응용 프로그램의 디버깅과 같습니다. 손쉬운 디버깅을 위해 일반적으로 Visual Studio를 통해 중단점을 설정할 수 있습니다. 신뢰할 수 있는 컬렉션은 여러 노드에 걸쳐 복제하더라도 여전히 IEnumerable을 구현합니다. 즉, 사용할 수 있는 결과 보기 hello Visual Studio에서 toosee 디버깅 하는 동안 내부 저장 했습니다. 코드의 아무 곳에나 중단점을 설정하기만 하면 됩니다.
   
    ![응용 프로그램 디버깅 시작][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>원격 서비스 패브릭 응용 프로그램 디버깅
수 있다면 서비스 패브릭 응용 프로그램에서 Azure 서비스 패브릭 클러스터를 실행 중인 경우 Visual Studio에서 직접 이러한 tooremotely 디버그 합니다.

> [!NOTE]
> hello 기능을 사용 하려면 [서비스 패브릭 SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)합니다.    
> 
> 

<!-- -->
> [!WARNING]
> 원격 디버깅을 위한 데이터베이스 개발/테스트 시나리오 및 응용 프로그램을 실행 하는 hello에 hello 미치는 영향 때문에 프로덕션 환경에서 사용 하는 toobe 되지 않습니다.
> 
> 

1. Tooyour 클러스터에 이동 **클라우드 탐색기**마우스 오른쪽 단추로 클릭 하 고 선택 **디버깅 사용**
   
    ![원격 디버깅 사용][enableremotedebugging]
   
    이 원격 클러스터 노드에 대 한 확장 디버깅 hello를 사용 하도록 설정 hello 프로세스 일정도으로 필요한 네트워크 구성.
2. 마우스 오른쪽 단추로 클릭 hello 클러스터 노드 **클라우드 탐색기**, 선택 **디버거 연결**
   
    ![디버거 연결][attachdebugger]
3. Hello에 **tooprocess 연결** 대화 상자를 누르고 toodebug, 원하는 hello 프로세스 선택 **연결**
   
    ![프로세스 선택][chooseprocess]
   
    hello 이름 hello 프로세스의를 tooattach 5d; equals hello 프로그램 서비스 프로젝트 어셈블리의 이름이 됩니다.
   
    hello 디버거에서는 hello 프로세스를 실행 하는 tooall 노드를 연결 합니다.
   
   * 상태 비저장 서비스 디버깅할 hello 경우에서 모든 노드에서 hello 서비스의 모든 인스턴스를 사용 하면 hello 디버그 세션에 속합니다.
   * 상태 저장 서비스를 디버깅 하는 경우 파티션의의 주 복제본 hello만 활성화 되 고 따라서 hello 디버거에 의해 검색 되었습니다. 주 복제본 hello hello 디버그 세션 중를 이동할 경우 해당 복제본의 hello 처리 여전히 hello 디버그 세션의 일부가 됩니다.
   * 순서 tooonly catch 관련 파티션만 또는 지정된 된 서비스의 인스턴스는 특정 파티션에 조건부 중단점 tooonly break 또는 인스턴스를 사용할 수 있습니다.
     
     ![조건부 중단점][conditionalbreakpoint]
     
     > [!NOTE]
     > 현재 지원 하지 않습니다 hello의 여러 인스턴스를 사용 하 여 서비스 패브릭 클러스터 디버깅 동일한 서비스 실행 파일 이름입니다.
     > 
     > 
4. 응용 프로그램 디버깅을 완료 한 후에 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 여 hello 원격 디버깅 확장을 비활성화할 수 있습니다 **클라우드 탐색기** 선택 **디버깅 사용 안 함**
   
    ![원격 디버깅 사용 안 함][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>원격 클러스터 노드에서 스트리밍 추적
원격 클러스터 노드 tooVisual Studio에서 직접 수 toostream 추적 수도 있습니다. 이 기능은 서비스 패브릭 클러스터 노드에서 만들어지는 toostream ETW 추적 이벤트입니다.

> [!NOTE]
> 이 기능은 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/)가 필요합니다.
> 이 기능은 Azure에서 실행되는 클러스터만 지원합니다.
> 
> 

<!-- -->
> [!WARNING]
> 추적 스트리밍 개발/테스트 시나리오 및 응용 프로그램을 실행 하는 hello에 hello 미치는 영향 때문에 프로덕션 환경에서 사용 하는 toobe 되지 것입니다.
> 프로덕션 시나리오에서는 Azure 진단을 통해 이벤트 전달을 사용해야 합니다.
> 
> 

1. Tooyour 클러스터에 이동 **클라우드 탐색기**마우스 오른쪽 단추로 클릭 하 고 선택 **스트리밍 추적을 사용 하도록 설정**
   
    ![원격 스트리밍 추적 사용][enablestreamingtraces]
   
    이 클러스터 노드에서 추적 확장 스트리밍 hello를 사용 하도록 설정 hello 프로세스 일정도으로 필요한 네트워크 구성.
2. Hello 확장 **노드** 요소 **클라우드 탐색기**, hello 노드를 마우스 오른쪽 단추 클릭에서 toostream 추적을 선택 **스트리밍 추적 보기**
   
    ![원격 스트리밍 추적 보기][viewremotestreamingtraces]
   
    많은 노드에서 toosee 추적에 대 한 2 단계를 반복 합니다. 각 노드 스트림은 전용 창에 표시됩니다.
   
    서비스 패브릭 및 서비스에서 내보낸 수 toosee hello 추적 됩니다. 특정 응용 프로그램 toofilter hello 이벤트 tooonly 표시 하려는 경우 hello 필터에서 hello 응용 프로그램의 hello 이름에 입력 합니다.
   
    ![스트리밍 추적 보기][viewingstreamingtraces]
3. 클러스터에서 스트리밍 추적 작업이 완료 되 면 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 여 원격 스트리밍 추적을 해제할 수 있습니다 **클라우드 탐색기** 선택 **스트리밍 추적 사용 안 함**
   
    ![원격 스트리밍 추적 사용 안 함][disablestreamingtraces]

## <a name="next-steps"></a>다음 단계
* [서비스 패브릭 서비스 테스트](service-fabric-testability-overview.md)
* [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
