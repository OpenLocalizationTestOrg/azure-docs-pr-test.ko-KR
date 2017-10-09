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
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="8860c-103">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="8860c-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8860c-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="8860c-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="8860c-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="8860c-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="8860c-106">로컬 서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="8860c-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="8860c-107">로컬 컴퓨터 개발 클러스터에서 Azure 서비스 패브릭 응용 프로그램을 배포하고 디버그하여 시간과 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="8860c-108">Visual Studio 2017 또는 Visual Studio 2015 hello 응용 프로그램 toohello 로컬 클러스터를 배포할 수 있으며 응용 프로그램의 hello 디버거 tooall 인스턴스를 자동으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="8860c-109">로컬 개발 클러스터에 hello 단계에 따라 시작 [서비스 패브릭 개발 환경 설정](service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="8860c-110">**F5** 키를 누르거나 **디버그** > **디버깅 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![응용 프로그램 디버깅 시작][startdebugging]
3. <span data-ttu-id="8860c-112">Hello에 대 한 명령을 클릭 하 여 코드와 hello 응용 프로그램을 통해 단계에 중단점을 설정 **디버그** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="8860c-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8860c-113">Visual Studio 응용 프로그램의 tooall 인스턴스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="8860c-114">단계별로 코드를 실행하는 동안 중단점은 동시 세션에서 발생하는 여러 프로세스에 히트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="8860c-115">공격을 각 중단점 조건 hello 스레드 ID 별로 만들거나 진단 이벤트를 사용 하 여 후 hello 중단점을 사용 하지 않도록 설정 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="8860c-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="8860c-116">hello **진단 이벤트** 실시간으로 진단 이벤트를 볼 수 있도록에 자동으로 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![실시간으로 진단 이벤트 보기][diagnosticevents]
5. <span data-ttu-id="8860c-118">Hello를 열 수도 있습니다 **진단 이벤트** 클라우드 탐색기에서 창.</span><span class="sxs-lookup"><span data-stu-id="8860c-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="8860c-119">**Service Fabric**에서 아무 노드를 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![열기 hello 진단 이벤트 창][viewdiagnosticevents]
   
    <span data-ttu-id="8860c-121">추적 tooa 특정 서비스 또는 응용 프로그램과 toofilter를 원하는 경우에 해당 특정 서비스 또는 응용 프로그램에서 스트리밍 추적 사용 하도록 설정 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="8860c-122">자동으로 생성 하는 hello hello 진단 이벤트를 볼 수 **ServiceEventSource.cs** 파일 및 응용 프로그램 코드에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="8860c-123">hello **진단 이벤트** 창에서 필터링, 일시 중지 및 검사를 실시간으로 이벤트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="8860c-124">hello 필터는 해당 내용을 포함 하는 hello 이벤트 메시지의 간단한 문자열 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![실시간으로 이벤트를 필터링, 일시 중지, 다시 시작 또는 검사합니다.][diagnosticeventsactions]
8. <span data-ttu-id="8860c-126">서비스 디버깅은 다른 모든 응용 프로그램의 디버깅과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="8860c-127">손쉬운 디버깅을 위해 일반적으로 Visual Studio를 통해 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="8860c-128">신뢰할 수 있는 컬렉션은 여러 노드에 걸쳐 복제하더라도 여전히 IEnumerable을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="8860c-129">즉, 사용할 수 있는 결과 보기 hello Visual Studio에서 toosee 디버깅 하는 동안 내부 저장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="8860c-130">코드의 아무 곳에나 중단점을 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![응용 프로그램 디버깅 시작][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="8860c-132">원격 서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="8860c-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="8860c-133">수 있다면 서비스 패브릭 응용 프로그램에서 Azure 서비스 패브릭 클러스터를 실행 중인 경우 Visual Studio에서 직접 이러한 tooremotely 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="8860c-134">hello 기능을 사용 하려면 [서비스 패브릭 SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="8860c-135">원격 디버깅을 위한 데이터베이스 개발/테스트 시나리오 및 응용 프로그램을 실행 하는 hello에 hello 미치는 영향 때문에 프로덕션 환경에서 사용 하는 toobe 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="8860c-136">Tooyour 클러스터에 이동 **클라우드 탐색기**마우스 오른쪽 단추로 클릭 하 고 선택 **디버깅 사용**</span><span class="sxs-lookup"><span data-stu-id="8860c-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![원격 디버깅 사용][enableremotedebugging]
   
    <span data-ttu-id="8860c-138">이 원격 클러스터 노드에 대 한 확장 디버깅 hello를 사용 하도록 설정 hello 프로세스 일정도으로 필요한 네트워크 구성.</span><span class="sxs-lookup"><span data-stu-id="8860c-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="8860c-139">마우스 오른쪽 단추로 클릭 hello 클러스터 노드 **클라우드 탐색기**, 선택 **디버거 연결**</span><span class="sxs-lookup"><span data-stu-id="8860c-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![디버거 연결][attachdebugger]
3. <span data-ttu-id="8860c-141">Hello에 **tooprocess 연결** 대화 상자를 누르고 toodebug, 원하는 hello 프로세스 선택 **연결**</span><span class="sxs-lookup"><span data-stu-id="8860c-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![프로세스 선택][chooseprocess]
   
    <span data-ttu-id="8860c-143">hello 이름 hello 프로세스의를 tooattach 5d; equals hello 프로그램 서비스 프로젝트 어셈블리의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="8860c-144">hello 디버거에서는 hello 프로세스를 실행 하는 tooall 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="8860c-145">상태 비저장 서비스 디버깅할 hello 경우에서 모든 노드에서 hello 서비스의 모든 인스턴스를 사용 하면 hello 디버그 세션에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="8860c-146">상태 저장 서비스를 디버깅 하는 경우 파티션의의 주 복제본 hello만 활성화 되 고 따라서 hello 디버거에 의해 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="8860c-147">주 복제본 hello hello 디버그 세션 중를 이동할 경우 해당 복제본의 hello 처리 여전히 hello 디버그 세션의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="8860c-148">순서 tooonly catch 관련 파티션만 또는 지정된 된 서비스의 인스턴스는 특정 파티션에 조건부 중단점 tooonly break 또는 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![조건부 중단점][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="8860c-150">현재 지원 하지 않습니다 hello의 여러 인스턴스를 사용 하 여 서비스 패브릭 클러스터 디버깅 동일한 서비스 실행 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="8860c-151">응용 프로그램 디버깅을 완료 한 후에 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 여 hello 원격 디버깅 확장을 비활성화할 수 있습니다 **클라우드 탐색기** 선택 **디버깅 사용 안 함**</span><span class="sxs-lookup"><span data-stu-id="8860c-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![원격 디버깅 사용 안 함][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="8860c-153">원격 클러스터 노드에서 스트리밍 추적</span><span class="sxs-lookup"><span data-stu-id="8860c-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="8860c-154">원격 클러스터 노드 tooVisual Studio에서 직접 수 toostream 추적 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="8860c-155">이 기능은 서비스 패브릭 클러스터 노드에서 만들어지는 toostream ETW 추적 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="8860c-156">이 기능은 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="8860c-157">이 기능은 Azure에서 실행되는 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="8860c-158">추적 스트리밍 개발/테스트 시나리오 및 응용 프로그램을 실행 하는 hello에 hello 미치는 영향 때문에 프로덕션 환경에서 사용 하는 toobe 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="8860c-159">프로덕션 시나리오에서는 Azure 진단을 통해 이벤트 전달을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="8860c-160">Tooyour 클러스터에 이동 **클라우드 탐색기**마우스 오른쪽 단추로 클릭 하 고 선택 **스트리밍 추적을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="8860c-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 사용][enablestreamingtraces]
   
    <span data-ttu-id="8860c-162">이 클러스터 노드에서 추적 확장 스트리밍 hello를 사용 하도록 설정 hello 프로세스 일정도으로 필요한 네트워크 구성.</span><span class="sxs-lookup"><span data-stu-id="8860c-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="8860c-163">Hello 확장 **노드** 요소 **클라우드 탐색기**, hello 노드를 마우스 오른쪽 단추 클릭에서 toostream 추적을 선택 **스트리밍 추적 보기**</span><span class="sxs-lookup"><span data-stu-id="8860c-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 보기][viewremotestreamingtraces]
   
    <span data-ttu-id="8860c-165">많은 노드에서 toosee 추적에 대 한 2 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="8860c-166">각 노드 스트림은 전용 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="8860c-167">서비스 패브릭 및 서비스에서 내보낸 수 toosee hello 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="8860c-168">특정 응용 프로그램 toofilter hello 이벤트 tooonly 표시 하려는 경우 hello 필터에서 hello 응용 프로그램의 hello 이름에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8860c-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![스트리밍 추적 보기][viewingstreamingtraces]
3. <span data-ttu-id="8860c-170">클러스터에서 스트리밍 추적 작업이 완료 되 면 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 여 원격 스트리밍 추적을 해제할 수 있습니다 **클라우드 탐색기** 선택 **스트리밍 추적 사용 안 함**</span><span class="sxs-lookup"><span data-stu-id="8860c-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 사용 안 함][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="8860c-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8860c-172">Next steps</span></span>
* <span data-ttu-id="8860c-173">[서비스 패브릭 서비스 테스트](service-fabric-testability-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8860c-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="8860c-174">[Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="8860c-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
