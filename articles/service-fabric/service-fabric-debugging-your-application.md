---
title: "Visual Studio에서 응용 프로그램 디버그 | Microsoft Docs"
description: "로컬 개발 클러스터의 Visual Studio에서 개발하고 디버그하여 서비스의 안정성과 성능을 향상시킵니다."
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="b390e-103">Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="b390e-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b390e-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="b390e-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="b390e-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="b390e-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="b390e-106">로컬 서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="b390e-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="b390e-107">로컬 컴퓨터 개발 클러스터에서 Azure 서비스 패브릭 응용 프로그램을 배포하고 디버그하여 시간과 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="b390e-108">Visual Studio 2017 또는 Visual Studio 2015는 로컬 클러스터에 응용 프로그램을 배포하고 응용 프로그램의 모든 인스턴스에 디버거를 자동으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="b390e-109">[서비스 패브릭 개발 환경 설정](service-fabric-get-started.md)의 단계를 따라 로컬 개발 클러스터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="b390e-110">**F5** 키를 누르거나 **디버그** > **디버깅 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![응용 프로그램 디버깅 시작][startdebugging]
3. <span data-ttu-id="b390e-112">코드의 중단점을 설정하고 **디버그** 메뉴의 명령을 클릭하여 응용 프로그램의 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b390e-113">Visual Studio는 응용 프로그램의 모든 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="b390e-114">단계별로 코드를 실행하는 동안 중단점은 동시 세션에서 발생하는 여러 프로세스에 히트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="b390e-115">스레드 ID의 각 중단점을 조건부로 생성하거나 진단 이벤트를 사용하여 히트된 후에 중단점을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="b390e-116">**진단 이벤트** 창이 자동으로 열려서 실시간으로 진단 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![실시간으로 진단 이벤트 보기][diagnosticevents]
5. <span data-ttu-id="b390e-118">클라우드 탐색기의 **진단 이벤트** 창도 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="b390e-119">**Service Fabric**에서 아무 노드를 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![진단 이벤트 창 열기][viewdiagnosticevents]
   
    <span data-ttu-id="b390e-121">특정 서비스 또는 응용 프로그램에 대해 추적을 필터링하려는 경우, 간단히 해당 특정 서비스 또는 응용 프로그램에서 스트리밍 추적을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="b390e-122">진단 이벤트는 자동으로 생성되는 **ServiceEventSource.cs** 파일에서 볼 수 있으며 응용 프로그램 코드에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="b390e-123">**진단 이벤트** 창은 필터링, 일시 중지 및 실시간 이벤트 검사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="b390e-124">필터는 해당 콘텐츠를 포함하는 이벤트 메시지의 단순 문자열 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![실시간으로 이벤트를 필터링, 일시 중지, 다시 시작 또는 검사합니다.][diagnosticeventsactions]
8. <span data-ttu-id="b390e-126">서비스 디버깅은 다른 모든 응용 프로그램의 디버깅과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="b390e-127">손쉬운 디버깅을 위해 일반적으로 Visual Studio를 통해 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="b390e-128">신뢰할 수 있는 컬렉션은 여러 노드에 걸쳐 복제하더라도 여전히 IEnumerable을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="b390e-129">따라서 디버그하는 동안 Visual Studio에서 결과 뷰를 사용하여 내부에 저장한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="b390e-130">코드의 아무 곳에나 중단점을 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![응용 프로그램 디버깅 시작][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="b390e-132">원격 서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="b390e-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="b390e-133">Azure의 서비스 패브릭 클러스터에서 서비스 패브릭 응용 프로그램이 실행 중인 경우, Visual Studio에서 직접 원격으로 이를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="b390e-134">이 기능은 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="b390e-135">원격 디버깅은 실행 중인 응용 프로그램에 영향을 미치기 때문에 개발/테스트 시나리오를 위한 것이며 프로덕션 환경에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="b390e-136">**Cloud Explorer**에 있는 클러스터로 이동하여, 마우스 오른쪽 단추로 클릭하고 **디버깅 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![원격 디버깅 사용][enableremotedebugging]
   
    <span data-ttu-id="b390e-138">이는 필수 네트워크 구성뿐만 아니라 클러스터 노드에서 원격 디버깅 확장을 사용하는 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="b390e-139">**Cloud Explorer**에 있는 클러스터 노드를 마우스 오른쪽 단추로 클릭하고 **디버거 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![디버거 연결][attachdebugger]
3. <span data-ttu-id="b390e-141">**프로세스에 연결** 대화 상자에서 디버깅하려는 프로세스를 선택하고 **연결**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="b390e-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![프로세스 선택][chooseprocess]
   
    <span data-ttu-id="b390e-143">연결하려는 프로세스의 이름은 서비스 프로젝트 어셈블리 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="b390e-144">디버거는 프로세스를 실행하는 모든 노드에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="b390e-145">상태 비저장 서비스를 디버깅하는 경우, 모든 노드에서 서비스의 모든 인스턴스는 디버그 세션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="b390e-146">상태 저장 서비스를 디버깅하는 경우, 파티션의 주 복제본에만 활성화되고 디버거에 의해 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="b390e-147">디버그 세션 중에 주 복제본이 이동한 경우, 해당 복제본의 처리는 여전히 디버그 세션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="b390e-148">지정된 서비스의 관련 파티션 또는 인스턴스만 캐치하려면 조건부 중단점을 사용하여 특정 파티션 또는 인스턴스만 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![조건부 중단점][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="b390e-150">현재 동일한 서비스 실행 파일 이름의 인스턴스가 다수인 패브릭 클러스터 디버깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="b390e-151">응용 프로그램 디버깅을 완료하면 **Cloud Explorer**에 있는 클러스터를 마우스 오른쪽 단추로 클릭하여 **디버깅 사용 안 함**을 선택하여 원격 디버깅 확장을 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![원격 디버깅 사용 안 함][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="b390e-153">원격 클러스터 노드에서 스트리밍 추적</span><span class="sxs-lookup"><span data-stu-id="b390e-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="b390e-154">또한 원격 클러스터 노드에서 Visual Studio까지 추적을 직접 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="b390e-155">이 기능을 통해 Service Fabric 클러스터 노드에서 생성된 ETW 추적 이벤트를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="b390e-156">이 기능은 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 및 [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="b390e-157">이 기능은 Azure에서 실행되는 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="b390e-158">스트리밍 추적은 실행 중인 응용 프로그램에 영향을 미치기 때문에 개발/테스트 시나리오를 위한 것이며 프로덕션 환경에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="b390e-159">프로덕션 시나리오에서는 Azure 진단을 통해 이벤트 전달을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="b390e-160">**Cloud Explorer**에 있는 클러스터로 이동하여, 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 사용][enablestreamingtraces]
   
    <span data-ttu-id="b390e-162">이는 필수 네트워크 구성뿐만 아니라 클러스터 노드에서 스트리밍 추적 확장을 사용하는 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="b390e-163">**Cloud Explorer**에 있는 **노드** 요소를 확장하고, 추적을 스트리밍하려는 노드를 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 보기][viewremotestreamingtraces]
   
    <span data-ttu-id="b390e-165">추적을 보려는 노드 개수만큼 2단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="b390e-166">각 노드 스트림은 전용 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="b390e-167">이제 서비스 패브릭에서 내보낸 추적과 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="b390e-168">특정 응용 프로그램에만 표시하도록 이벤트를 필터링하려는 경우, 필터에서 응용 프로그램의 이름만 간단히 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![스트리밍 추적 보기][viewingstreamingtraces]
3. <span data-ttu-id="b390e-170">클러스터에서 스트리밍 추적을 완료하면 **Cloud Explorer**에 있는 클러스터를 마우스 오른쪽 단추로 클릭하고 **스트리밍 추적 사용 안 함**을 선택하여 원격 스트리밍 추적을 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b390e-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![원격 스트리밍 추적 사용 안 함][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="b390e-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b390e-172">Next steps</span></span>
* <span data-ttu-id="b390e-173">[서비스 패브릭 서비스 테스트](service-fabric-testability-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b390e-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="b390e-174">[Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="b390e-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
