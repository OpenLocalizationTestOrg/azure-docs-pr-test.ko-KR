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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Hello 노드 시작 및 중지 노드 Api hello 노드 전환 API로 교체

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>노드 중지 hello 수행 기능 하 고 노드 Api 시작 합니까?

hello 노드 API 중지 (관리 되는: [StopNodeAsync()][stopnode], PowerShell: [중지 ServiceFabricNode][stopnodeps]) 서비스 패브릭 노드를 중지 합니다.  서비스 패브릭 노드는 프로세스, VM 또는 컴퓨터 아닙니다. – hello VM 또는 컴퓨터는 계속 실행 됩니다.  Hello 나머지 hello 문서에 대 한 "노드" 서비스 패브릭 노드를 의미 합니다.  가져와 노드를 중지 한 *중지* 상태 hello 클러스터의 구성원이 아니므로 하 고 시뮬레이션할 서비스를 호스팅할 수 없습니다는 *아래로* 노드.  이 응용 프로그램 시스템 tootest hello에 오류를 삽입 하는 데 유용 합니다.  hello 노드 API 시작 (관리 되는: [StartNodeAsync()][startnode], PowerShell: [시작 ServiceFabricNode][startnodeps]]) 역방향 hello 노드 API 중지  hello 노드 백 tooa 정상 상태로 표시 합니다.

## <a name="why-are-we-replacing-these"></a>이러한 API를 교체하는 이유는 무엇일까요?

앞에서 설명한 대로 *중지* 서비스 패브릭 노드는 의도적으로 hello 중지 노드 API를 사용 하 여 대상 노드입니다.  A *아래로* (VM 또는 컴퓨터 예: hello 해제 되어 있음) 되는 다른 어떤 이유로 아래에 있는 노드.  Hello 시스템 노드 API 중지 hello로 사이의 toodifferentiate 정보를 노출 하지 않습니다 *중지* 노드 및 *아래로* 노드.

또한 이러한 API에서 반환하는 일부 오류는 충분한 설명을 포함하지 않습니다.  예를 들어 호출에 중지 노드 API hello는 이미 *중지* 노드는 hello 오류를 반환 하는 *InvalidAddress*합니다.  이러한 환경을 향상시킬 수 있습니다.

또한 hello 기간에 대 한 노드 중지 된은 "무제한" hello 시작 노드 API를 호출할 때까지 합니다.  이로 인해 문제가 발생하고 오류가 발생하기 쉬워질 수 있습니다.  예를 들어 여기서 사용자 노드에서 hello 중지 노드 API를 호출 하 고 다음 항목에 대 한 찾기 문제 살펴보았습니다.  Hello 노드가 명확 없었습니다 나중 *아래로* 또는 *중지*합니다.


## <a name="introducing-hello-node-transition-apis"></a>Hello 노드 전환 Api 소개

새로운 API 집합에서 이러한 문제를 살펴보았습니다.  hello 새 노드 전환 API (관리 되는: [StartNodeTransitionAsync()][snt]) 서비스 패브릭 노드 tooa 사용된 tootransition 수 *중지* 상태나 tootransition 것 *중지* 상태를 정상 상태로 tooa 합니다.  Hello API의 hello 이름에 해당 hello "Start" toostarting 노드를 참조 하지 않는 note 하십시오.  Toobeginning hello 시스템은 tootransition hello 노드 tooeither를 실행 하는 비동기 작업 참조 *중지* 또는 상태를 시작 합니다.

**사용 현황**

Hello 노드 전환 API에서 호출 될 때 예외를 throw 하지 않습니다, hello 시스템에서 hello 비동기 작업을 수락 및 실행 됩니다.  호출이 성공 hello 작업이 아직 완료 하는 것을 의미 하지 않습니다.  hello hello 작업을 호출 hello 노드 전환 진행률 API의 현재 상태에 대 한 tooget 정보 (관리 되는: [GetNodeTransitionProgressAsync()][gntp]) 노드를 호출할 때 사용 되는 hello guid를 가진 이 작업에 대 한 전환 API입니다.  hello 노드 전환 진행률 API NodeTransitionProgress 개체를 반환 합니다.  이 개체의 State 속성이 hello hello 작업의 현재 상태를 지정합니다.  Hello 상태가 "Running" hello 작업이 중입니다.  완료 되 면 hello 작업이 오류 없이 완료 되었습니다.  Faulted 인 경우 hello 작업을 실행 하는 문제가 발생 했습니다.  속성은 어떤 hello 발급 나타냅니다 hello 결과 속성의 예외는입니다.  Https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate hello State 속성 및 코드 예제에 대 한 아래의 hello "샘플 사용" 섹션에 대 한 자세한 내용은 참조 하십시오.


**중지 된 노드와 아래쪽 노드가 차별화** 노드를 경우 *중지* 노드 전환 API 노드 쿼리의 hello 출력 hello를 사용 하 여 (관리 되는: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) 노드마다이 표시 됩니다는 *IsStopped* 속성 값이 true입니다.  이 hello의 hello 값과에서 다른 *NodeStatus* 됩니다 속성 *아래로*합니다.  경우 hello *NodeStatus* 속성의 값은 *아래로*, 하지만 *IsStopped* 이며가 false 이면 hello 노드 hello 노드 전환 API를 사용 하 여 중지 되지 않았습니다  *아래로* 다른 이유로 인해 합니다.  경우 hello *IsStopped* 속성은 true와 hello *NodeStatus* 속성은 *아래로*, hello 노드 전환 API를 사용 하 여 중지 합니다.

시작 하는 *중지* hello 노드 전환 API를 사용 하 여 노드는 반환 toofunction hello 클러스터의 정상적인 멤버로 다시 합니다.  hello hello 노드 쿼리 API의 출력 표시 됩니다 *IsStopped* false로 및 *NodeStatus* 축 (예: 작동) 다운 하지 않습니다.


**제한 기간** hello 노드 전환 API toostop 노드를 사용할 때 필수 매개 hello 중 하나 *stopNodeDurationInSeconds*를 나타내는 시간 (초) tookeep hello 노드 hello  *중지*합니다.  이 값은 허용 되는 범위는 600의 최소와 최대 14400 hello에 있어야 합니다.  이 시간이 만료 되 면 hello 노드 됩니다에 자체 상태를 자동으로 다시 시작 합니다.  사용법 tooSample 1 아래를 참조 하십시오.

> [!WARNING]
> 노드 중지 및 시작 노드 Api hello 및 노드 전환 Api 혼합을 방지 합니다.  hello 너무 hello 노드 전환 API를 사용 하 여 좋습니다.  > 노드가 이미 된 경우 hello 중지 노드 API를 사용 하 여 중지 하기 시작 해야 hello를 사용 하기 전에 먼저 hello 시작 노드 API를 사용 > 노드 전환 Api입니다.

> [!WARNING]
> 여러 노드 전환 Api 호출에서 만들 수 없습니다 hello 동시에 동일한 노드.  Hello 노드 전환 API는 이러한 상황에서 > ErrorCode 속성 값이 NodeTransitionInProgress FabricException을 throw 합니다.  특정 노드에서 노드 전환 되 면 > 되었습니다 시작 기다려야 hello 작업에 종료 상태 (Completed, Faulted, 또는 ForceCancelled)을 시작 하기 전에 도달할 때까지 > new 전환 hello에 동일한 노드.  여러 다른 노드에 대한 병렬 노드 전환 호출이 허용됩니다.


#### <a name="sample-usage"></a>샘플 사용


**예제 1** -샘플에서는 다음 hello hello 노드 전환 API toostop 노드.

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

**예제 2** -hello 다음 샘플 시작 되는 *중지* 노드.  Hello 첫 번째 예제에서 일부 도우미 메서드를 사용합니다.

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

**예제 3** -hello 다음 예제에서는 잘못 된 사용을 보여 줍니다.  이 사용이 잘못 되었습니다. 때문에 hello *stopDurationInSeconds* hello 허용 되는 범위 보다 크면를 제공 합니다.  이후 StartNodeTransitionAsync()는 오류를 표시 하며 실패 합니다 hello 작업이 적절 하지 않습니다 및 hello 진행률 API를 호출 하지 않아야 합니다.  이 샘플에서는 hello 첫 번째 예제에서 일부 도우미 메서드를 사용 합니다.

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

**예제 4** -hello 다음 예제에서는 hello hello 노드 전환 API 초기화 된 hello 작업을 허용 하지만 나중에 실행 하는 동안 오류가 발생 하는 경우 노드 전환 진행률 API에서에서 반환 되는 hello 오류 정보를 보여 줍니다.  Hello 경우에는 hello 노드 전환 API toostart 존재 하지 않는 노드를 시도 하기 때문에 실패 합니다.  이 샘플에서는 hello 첫 번째 예제에서 일부 도우미 메서드를 사용 합니다.

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
