---
title: "Azure microservices의 오류를 aaaSimulate | Microsoft Docs"
description: "어떻게 tooharden 정상 및 비정상 오류에 대 한 서비스입니다."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: 
ms.assetid: 44af01f0-ed73-4c31-8ac0-d9d65b4ad2d6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: 05467e291dfc0f12a021955f8ea540881ec10746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="simulate-failures-during-service-workloads"></a><span data-ttu-id="bc657-103">서비스 워크로드 중 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-103">Simulate failures during service workloads</span></span>
<span data-ttu-id="bc657-104">Azure 서비스 패브릭의 테스트 용이성 시나리오 hello 활성화 처리 개별 오류에 대 한 개발자 toonot 걱정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bc657-104">hello testability scenarios in Azure Service Fabric enable developers toonot worry about dealing with individual faults.</span></span> <span data-ttu-id="bc657-105">그러나 클라이언트 워크로드 및 오류의 명시적인 인터리빙이 필요한 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-105">There are scenarios, however, where an explicit interleaving of client workload and failures might be needed.</span></span> <span data-ttu-id="bc657-106">클라이언트 작업 및 오류 hello 인터리빙 hello 서비스 오류가 발생 하는 경우 일부 동작 수행 실제로 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-106">hello interleaving of client workload and faults ensures that hello service is actually performing some action when failure happens.</span></span> <span data-ttu-id="bc657-107">테스트 가능성을 제공 하는 컨트롤의 hello 수준이 제공 이러한 hello 작업 실행의 정확한 시점에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-107">Given hello level of control that testability provides, these could be at precise points of hello workload execution.</span></span> <span data-ttu-id="bc657-108">Hello 응용 프로그램에서 다양 한 상태의에서 오류의이 유도 버그 찾은 품질을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-108">This induction of faults at different states in hello application can find bugs and improve quality.</span></span>

## <a name="sample-custom-scenario"></a><span data-ttu-id="bc657-109">사용자 지정 샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="bc657-109">Sample custom scenario</span></span>
<span data-ttu-id="bc657-110">이 테스트 시나리오가 나와 있습니다. 해당 interleaves hello 비즈니스 카디널리티 평가기로 작업 [정상 및 비정상 오류](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-110">This test shows a scenario that interleaves hello business workload with [graceful and ungraceful failures](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span></span> <span data-ttu-id="bc657-111">서비스 작업 또는 최상의 결과 계산의 중간 hello에에서 hello 오류를 일으킨 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-111">hello faults should be induced in hello middle of service operations or compute for best results.</span></span>

<span data-ttu-id="bc657-112">4 개 작업을 노출 하는 서비스의 예를 살펴보겠습니다: A, B, C, 4. 각 워크플로의 tooa 집합에 해당 하 고 계산 될 수 없습니다, 저장소 또는 혼합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-112">Let's walk through an example of a service that exposes four workloads: A, B, C, and D. Each corresponds tooa set of workflows and could be compute, storage, or a mix.</span></span> <span data-ttu-id="bc657-113">간단한 hello 위해서 예에서 hello 작업 아웃 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-113">For hello sake of simplicity, we will abstract out hello workloads in our example.</span></span> <span data-ttu-id="bc657-114">이 예에서 실행 하는 hello 다른 오류는:</span><span class="sxs-lookup"><span data-stu-id="bc657-114">hello different faults executed in this example are:</span></span>

* <span data-ttu-id="bc657-115">RestartNode: 비정상적 오류 toosimulate 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-115">RestartNode: Ungraceful fault toosimulate a machine restart.</span></span>
* <span data-ttu-id="bc657-116">RestartDeployedCodePackage: 비정상적 오류 toosimulate 서비스 호스트 프로세스 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-116">RestartDeployedCodePackage: Ungraceful fault toosimulate service host process crashes.</span></span>
* <span data-ttu-id="bc657-117">RemoveReplica: 정상적인 오류 toosimulate 복제본 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-117">RemoveReplica: Graceful fault toosimulate replica removal.</span></span>
* <span data-ttu-id="bc657-118">MovePrimary: 정상적인 오류 toosimulate 복제본 hello 서비스 패브릭 부하 분산 장치에 의해 트리거된 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bc657-118">MovePrimary: Graceful fault toosimulate replica moves triggered by hello Service Fabric load balancer.</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with hello actual version for your cluster and application.
        string clusterConnection = "localhost:19000";
        Uri applicationName = new Uri("fabric:/samples/PersistentToDoListApp");
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Workload Test...");
        try
        {
            RunTestAsync(clusterConnection, applicationName, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Workload Test failed: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Workload Test completed successfully.");
        return 0;
    }

    public enum ServiceWorkloads
    {
        A,
        B,
        C,
        D
    }

    public enum ServiceFabricFaults
    {
        RestartNode,
        RestartCodePackage,
        RemoveReplica,
        MovePrimary,
    }

    public static async Task RunTestAsync(string clusterConnection, Uri applicationName, Uri serviceName)
    {
        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);
        // Maximum time toowait for a service toostabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want tooexecute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start hello workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While hello task is running, induce faults into hello service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from hello given service tootest.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run hello selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate hello health and stability of hello service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for hello workload toofinish successfully.
            await workloadTask;
        }
    }

    private static async Task RunFaultAsync(Uri applicationName, ServiceFabricFaults fault, ReplicaSelector selector, FabricClient client)
    {
        switch (fault)
        {
            case ServiceFabricFaults.RestartNode:
                await client.ClusterManager.RestartNodeAsync(selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RestartCodePackage:
                await client.ApplicationManager.RestartDeployedCodePackageAsync(applicationName, selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RemoveReplica:
                await client.ServiceManager.RemoveReplicaAsync(selector, CompletionMode.Verify, false);
                break;
            case ServiceFabricFaults.MovePrimary:
                await client.ServiceManager.MovePrimaryAsync(selector.PartitionSelector);
                break;
        }
    }

    private static Task RunWorkloadAsync(ServiceWorkloads workload)
    {
        throw new NotImplementedException();
        // This is where you trigger and complete your service workload.
        // Note that hello faults induced while your service workload is running will
        // fault hello primary service. Hence, you will need tooreconnect toocomplete or check
        // hello status of hello workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
