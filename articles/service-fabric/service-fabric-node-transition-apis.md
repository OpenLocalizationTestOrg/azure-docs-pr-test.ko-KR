---
title: "aaaStart 및 중지할 클러스터 노드의 tootest Azure microservices | Microsoft Docs"
description: "어떻게 toouse 오류 주입 tootest 서비스 패브릭 응용 프로그램을 시작 하 고 클러스터 노드를 중지 하 여에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="4eaa3-103">Hello 노드 시작 및 중지 노드 Api hello 노드 전환 API로 교체</span><span class="sxs-lookup"><span data-stu-id="4eaa3-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="4eaa3-104">노드 중지 hello 수행 기능 하 고 노드 Api 시작 합니까?</span><span class="sxs-lookup"><span data-stu-id="4eaa3-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="4eaa3-105">hello 노드 API 중지 (관리 되는: [StopNodeAsync()][stopnode], PowerShell: [중지 ServiceFabricNode][stopnodeps]) 서비스 패브릭 노드를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="4eaa3-106">서비스 패브릭 노드는 프로세스, VM 또는 컴퓨터 아닙니다. – hello VM 또는 컴퓨터는 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="4eaa3-107">Hello 나머지 hello 문서에 대 한 "노드" 서비스 패브릭 노드를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="4eaa3-108">가져와 노드를 중지 한 *중지* 상태 hello 클러스터의 구성원이 아니므로 하 고 시뮬레이션할 서비스를 호스팅할 수 없습니다는 *아래로* 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="4eaa3-109">이 응용 프로그램 시스템 tootest hello에 오류를 삽입 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="4eaa3-110">hello 노드 API 시작 (관리 되는: [StartNodeAsync()][startnode], PowerShell: [시작 ServiceFabricNode][startnodeps]]) 역방향 hello 노드 API 중지  hello 노드 백 tooa 정상 상태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="4eaa3-111">이러한 API를 교체하는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="4eaa3-111">Why are we replacing these?</span></span>

<span data-ttu-id="4eaa3-112">앞에서 설명한 대로 *중지* 서비스 패브릭 노드는 의도적으로 hello 중지 노드 API를 사용 하 여 대상 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="4eaa3-113">A *아래로* (VM 또는 컴퓨터 예: hello 해제 되어 있음) 되는 다른 어떤 이유로 아래에 있는 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="4eaa3-114">Hello 시스템 노드 API 중지 hello로 사이의 toodifferentiate 정보를 노출 하지 않습니다 *중지* 노드 및 *아래로* 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="4eaa3-115">또한 이러한 API에서 반환하는 일부 오류는 충분한 설명을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="4eaa3-116">예를 들어 호출에 중지 노드 API hello는 이미 *중지* 노드는 hello 오류를 반환 하는 *InvalidAddress*합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="4eaa3-117">이러한 환경을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-117">This experience could be improved.</span></span>

<span data-ttu-id="4eaa3-118">또한 hello 기간에 대 한 노드 중지 된은 "무제한" hello 시작 노드 API를 호출할 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="4eaa3-119">이로 인해 문제가 발생하고 오류가 발생하기 쉬워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="4eaa3-120">예를 들어 여기서 사용자 노드에서 hello 중지 노드 API를 호출 하 고 다음 항목에 대 한 찾기 문제 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="4eaa3-121">Hello 노드가 명확 없었습니다 나중 *아래로* 또는 *중지*합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="4eaa3-122">Hello 노드 전환 Api 소개</span><span class="sxs-lookup"><span data-stu-id="4eaa3-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="4eaa3-123">새로운 API 집합에서 이러한 문제를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="4eaa3-124">hello 새 노드 전환 API (관리 되는: [StartNodeTransitionAsync()][snt]) 서비스 패브릭 노드 tooa 사용된 tootransition 수 *중지* 상태나 tootransition 것 *중지* 상태를 정상 상태로 tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="4eaa3-125">Hello API의 hello 이름에 해당 hello "Start" toostarting 노드를 참조 하지 않는 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="4eaa3-126">Toobeginning hello 시스템은 tootransition hello 노드 tooeither를 실행 하는 비동기 작업 참조 *중지* 또는 상태를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="4eaa3-127">**사용 현황**</span><span class="sxs-lookup"><span data-stu-id="4eaa3-127">**Usage**</span></span>

<span data-ttu-id="4eaa3-128">Hello 노드 전환 API에서 호출 될 때 예외를 throw 하지 않습니다, hello 시스템에서 hello 비동기 작업을 수락 및 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="4eaa3-129">호출이 성공 hello 작업이 아직 완료 하는 것을 의미 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="4eaa3-130">hello hello 작업을 호출 hello 노드 전환 진행률 API의 현재 상태에 대 한 tooget 정보 (관리 되는: [GetNodeTransitionProgressAsync()][gntp]) 노드를 호출할 때 사용 되는 hello guid를 가진 이 작업에 대 한 전환 API입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="4eaa3-131">hello 노드 전환 진행률 API NodeTransitionProgress 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="4eaa3-132">이 개체의 State 속성이 hello hello 작업의 현재 상태를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="4eaa3-133">Hello 상태가 "Running" hello 작업이 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="4eaa3-134">완료 되 면 hello 작업이 오류 없이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="4eaa3-135">Faulted 인 경우 hello 작업을 실행 하는 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="4eaa3-136">속성은 어떤 hello 발급 나타냅니다 hello 결과 속성의 예외는입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="4eaa3-137">Https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate hello State 속성 및 코드 예제에 대 한 아래의 hello "샘플 사용" 섹션에 대 한 자세한 내용은 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="4eaa3-138">**중지 된 노드와 아래쪽 노드가 차별화** 노드를 경우 *중지* 노드 전환 API 노드 쿼리의 hello 출력 hello를 사용 하 여 (관리 되는: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) 노드마다이 표시 됩니다는 *IsStopped* 속성 값이 true입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="4eaa3-139">이 hello의 hello 값과에서 다른 *NodeStatus* 됩니다 속성 *아래로*합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="4eaa3-140">경우 hello *NodeStatus* 속성의 값은 *아래로*, 하지만 *IsStopped* 이며가 false 이면 hello 노드 hello 노드 전환 API를 사용 하 여 중지 되지 않았습니다  *아래로* 다른 이유로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="4eaa3-141">경우 hello *IsStopped* 속성은 true와 hello *NodeStatus* 속성은 *아래로*, hello 노드 전환 API를 사용 하 여 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="4eaa3-142">시작 하는 *중지* hello 노드 전환 API를 사용 하 여 노드는 반환 toofunction hello 클러스터의 정상적인 멤버로 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="4eaa3-143">hello hello 노드 쿼리 API의 출력 표시 됩니다 *IsStopped* false로 및 *NodeStatus* 축 (예: 작동) 다운 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="4eaa3-144">**제한 기간** hello 노드 전환 API toostop 노드를 사용할 때 필수 매개 hello 중 하나 *stopNodeDurationInSeconds*를 나타내는 시간 (초) tookeep hello 노드 hello  *중지*합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="4eaa3-145">이 값은 허용 되는 범위는 600의 최소와 최대 14400 hello에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="4eaa3-146">이 시간이 만료 되 면 hello 노드 됩니다에 자체 상태를 자동으로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="4eaa3-147">사용법 tooSample 1 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="4eaa3-148">노드 중지 및 시작 노드 Api hello 및 노드 전환 Api 혼합을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="4eaa3-149">hello 너무 hello 노드 전환 API를 사용 하 여 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="4eaa3-150">> 노드가 이미 된 경우 hello 중지 노드 API를 사용 하 여 중지 하기 시작 해야 hello를 사용 하기 전에 먼저 hello 시작 노드 API를 사용 > 노드 전환 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="4eaa3-151">여러 노드 전환 Api 호출에서 만들 수 없습니다 hello 동시에 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="4eaa3-152">Hello 노드 전환 API는 이러한 상황에서 > ErrorCode 속성 값이 NodeTransitionInProgress FabricException을 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="4eaa3-153">특정 노드에서 노드 전환 되 면 > 되었습니다 시작 기다려야 hello 작업에 종료 상태 (Completed, Faulted, 또는 ForceCancelled)을 시작 하기 전에 도달할 때까지 > new 전환 hello에 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="4eaa3-154">여러 다른 노드에 대한 병렬 노드 전환 호출이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="4eaa3-155">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="4eaa3-155">Sample Usage</span></span>


<span data-ttu-id="4eaa3-156">**예제 1** -샘플에서는 다음 hello hello 노드 전환 API toostop 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="4eaa3-157">**예제 2** -hello 다음 샘플 시작 되는 *중지* 노드.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="4eaa3-158">Hello 첫 번째 예제에서 일부 도우미 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="4eaa3-159">**예제 3** -hello 다음 예제에서는 잘못 된 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="4eaa3-160">이 사용이 잘못 되었습니다. 때문에 hello *stopDurationInSeconds* hello 허용 되는 범위 보다 크면를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="4eaa3-161">이후 StartNodeTransitionAsync()는 오류를 표시 하며 실패 합니다 hello 작업이 적절 하지 않습니다 및 hello 진행률 API를 호출 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="4eaa3-162">이 샘플에서는 hello 첫 번째 예제에서 일부 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="4eaa3-163">**예제 4** -hello 다음 예제에서는 hello hello 노드 전환 API 초기화 된 hello 작업을 허용 하지만 나중에 실행 하는 동안 오류가 발생 하는 경우 노드 전환 진행률 API에서에서 반환 되는 hello 오류 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="4eaa3-164">Hello 경우에는 hello 노드 전환 API toostart 존재 하지 않는 노드를 시도 하기 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="4eaa3-165">이 샘플에서는 hello 첫 번째 예제에서 일부 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaa3-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
