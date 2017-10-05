---
title: "Azure 마이크로 서비스의 시뮬레이션 오류 | Microsoft Docs"
description: "정상/비정상 오류로부터 서비스의 보안을 강화하는 방법"
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
ms.openlocfilehash: 7ec671c23e101d0f7401bd4656fb201111602cad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="simulate-failures-during-service-workloads"></a><span data-ttu-id="68684-103">서비스 워크로드 중 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="68684-103">Simulate failures during service workloads</span></span>
<span data-ttu-id="68684-104">Azure 서비스 패브릭의 테스트 용이성 시나리오를 통해 개발자는 개별 결함의 처리에 대해 걱정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68684-104">The testability scenarios in Azure Service Fabric enable developers to not worry about dealing with individual faults.</span></span> <span data-ttu-id="68684-105">그러나 클라이언트 워크로드 및 오류의 명시적인 인터리빙이 필요한 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68684-105">There are scenarios, however, where an explicit interleaving of client workload and failures might be needed.</span></span> <span data-ttu-id="68684-106">클라이언트 워크로드 및 결함의 인터리빙은 장애가 발생했을 때 서비스가 실제로 일부 작업을 수행하도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="68684-106">The interleaving of client workload and faults ensures that the service is actually performing some action when failure happens.</span></span> <span data-ttu-id="68684-107">제공되는 제어 테스트 용이성 수준을 볼 때, 이것은 워크로드 실행의 정확한 지점일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68684-107">Given the level of control that testability provides, these could be at precise points of the workload execution.</span></span> <span data-ttu-id="68684-108">응용프로그램 내의 다양한 상태에서 결함의 유도를 통해 버그를 찾고 품질을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68684-108">This induction of faults at different states in the application can find bugs and improve quality.</span></span>

## <a name="sample-custom-scenario"></a><span data-ttu-id="68684-109">사용자 지정 샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="68684-109">Sample custom scenario</span></span>
<span data-ttu-id="68684-110">이 테스트는 [정상 및 비정상 오류](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions)가 발생한 비즈니스 워크로드의 인터리빙 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68684-110">This test shows a scenario that interleaves the business workload with [graceful and ungraceful failures](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span></span> <span data-ttu-id="68684-111">최상의 결과를 위해 서비스 작업 또는 계산 중에 결함을 유도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68684-111">The faults should be induced in the middle of service operations or compute for best results.</span></span>

<span data-ttu-id="68684-112">4개의 워크로드(A, B, C, D)를 노출하는 서비스를 예로 들어보겠습니다. 각 작업은 일련의 워크플로에 해당되며 계산, 저장소 또는 혼합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68684-112">Let's walk through an example of a service that exposes four workloads: A, B, C, and D. Each corresponds to a set of workflows and could be compute, storage, or a mix.</span></span> <span data-ttu-id="68684-113">간단한 설명을 위해 워크로드를 예를 들어 요약해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68684-113">For the sake of simplicity, we will abstract out the workloads in our example.</span></span> <span data-ttu-id="68684-114">다음은 이 예제에서 실행되는 여러 결함입니다.</span><span class="sxs-lookup"><span data-stu-id="68684-114">The different faults executed in this example are:</span></span>

* <span data-ttu-id="68684-115">RestartNode: 컴퓨터 재시작을 시뮬레이트하기 위한 비정상 결함</span><span class="sxs-lookup"><span data-stu-id="68684-115">RestartNode: Ungraceful fault to simulate a machine restart.</span></span>
* <span data-ttu-id="68684-116">RestartDeployedCodePackage: 서비스 호스트 프로세스 충돌을 시뮬레이트하기 위한 비정상 결함</span><span class="sxs-lookup"><span data-stu-id="68684-116">RestartDeployedCodePackage: Ungraceful fault to simulate service host process crashes.</span></span>
* <span data-ttu-id="68684-117">RemoveReplica: 복제본 제거를 시뮬레이트하기 위한 정상 결함</span><span class="sxs-lookup"><span data-stu-id="68684-117">RemoveReplica: Graceful fault to simulate replica removal.</span></span>
* <span data-ttu-id="68684-118">MovePrimary: 서비스 패브릭 부하 분산 장치에 의해 트리거되는 복제본 이동을 시뮬레이트하기 위한 정상 결함</span><span class="sxs-lookup"><span data-stu-id="68684-118">MovePrimary: Graceful fault to simulate replica moves triggered by the Service Fabric load balancer.</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with the actual version for your cluster and application.
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
        // Maximum time to wait for a service to stabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want to execute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start the workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While the task is running, induce faults into the service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from the given service to test.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run the selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate the health and stability of the service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for the workload to finish successfully.
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
        // Note that the faults induced while your service workload is running will
        // fault the primary service. Hence, you will need to reconnect to complete or check
        // the status of the workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
