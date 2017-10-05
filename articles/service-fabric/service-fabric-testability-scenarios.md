---
title: "Azure 마이크로 서비스에 대한 비정상 상황 및 장애 조치(Failover) 테스트 만들기 | Microsoft 문서"
description: "서비스 패브릭 Chaos 테스트 및 장애 조치 테스트 시나리오를 통해 결함을 유도하고 서비스의 신뢰성을 확인합니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="93d60-103">테스트 용이성 시나리오</span><span class="sxs-lookup"><span data-stu-id="93d60-103">Testability scenarios</span></span>
<span data-ttu-id="93d60-104">클라우드 인프라 같은 대규모 분산 시스템은 본질적으로 불안정합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="93d60-105">Azure 서비스 패브릭은 개발자에게 불안정한 인프라를 기반으로 실행되는 서비스를 작성할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="93d60-106">고품질 서비스를 작성하려면 개발자는 이처럼 불안정한 인프라에서 서비스의 안정성을 테스트하도록 유도할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="93d60-107">오류 분석 서비스는 개발자에게 오류가 있는 상황에서 서비스를 테스트할 수 있도록 오류 작업을 유도하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="93d60-108">그러나 특정 대상을 통한 오류 시뮬레이션으로는 한계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="93d60-109">테스트를 보다 길게 수행하려면 서비스 패브릭의 테스트 시나리오인 비정상 상황 테스트 및 장애 조치(failover) 테스트를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="93d60-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="93d60-110">이러한 시나리오는 장기간에 걸쳐 클러스터 전체에서 정상적 및 비정상적 인터리브 오류를 지속적으로 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="93d60-111">오류의 비율 및 종류로 테스트를 구성하면 C# API 또는 PowerShell을 통해 시작되어 클러스터 및 서비스에서 오류를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="93d60-112">ChaosTestScenario는 회복력이 뛰어난 서비스 기반 비정상 상황으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="93d60-113">자세한 내용은 새 문서인 [제어되는 비정상 상황](service-fabric-controlled-chaos.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93d60-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="93d60-114">비정상 상황 테스트</span><span class="sxs-lookup"><span data-stu-id="93d60-114">Chaos test</span></span>
<span data-ttu-id="93d60-115">비정상 상황 시나리오는 전체 서비스 패브릭 클러스터에서 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="93d60-116">이 시나리오에서는 일반적으로 수개월 또는 수년 후에 발견되는 오류를 수시간으로 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="93d60-117">인터리브 오류를 높은 오류 비율과 결합하면 놓치기 쉬운 특이한 사례를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="93d60-118">따라서 서비스 코드 품질이 대폭 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="93d60-119">비정상 상황 테스트에서 시뮬레이션하는 오류</span><span class="sxs-lookup"><span data-stu-id="93d60-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="93d60-120">노드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="93d60-120">Restart a node</span></span>
* <span data-ttu-id="93d60-121">배포된 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="93d60-121">Restart a deployed code package</span></span>
* <span data-ttu-id="93d60-122">복제본 제거</span><span class="sxs-lookup"><span data-stu-id="93d60-122">Remove a replica</span></span>
* <span data-ttu-id="93d60-123">복제본 다시 시작</span><span class="sxs-lookup"><span data-stu-id="93d60-123">Restart a replica</span></span>
* <span data-ttu-id="93d60-124">주 복제본 이동(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="93d60-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="93d60-125">보조 복제본 이동(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="93d60-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="93d60-126">비정상 상황 테스트에서는 지정된 기간 동안 오류 및 클러스터 유효성 검사를 여러 차례 반복해서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="93d60-127">클러스터가 안정화되고 유효성 검사가 성공하는 데 걸리는 시간도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="93d60-128">클러스터 유효성 검사에서 단일 오류가 발생하면 시나리오가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="93d60-129">예를 들어 1시간 동안 실행되고 최대 세 가지 오류가 동시에 발생하도록 설정된 테스트를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="93d60-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="93d60-130">이 테스트에서는 세 가지 오류를 유도한 후 클러스터 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="93d60-131">클러스터가 비정상 상태가 되거나 1시간이 지날 때까지 이전 단계가 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="93d60-132">구성된 시간 내에 클러스터가 안정화되지 못한 경우처럼 반복 과정 중에 클러스터가 비정상 상태가 되면 예외와 함께 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="93d60-133">이 예외는 뭔가가 잘못되었으며 자세한 조사가 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="93d60-134">현재 상태에서는 비정상 상황 테스트의 오류 생성 엔진이 안전 오류만 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="93d60-135">다시 말해서 외부 오류가 없으면 쿼럼 또는 데이터 손실이 절대 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="93d60-136">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="93d60-136">Important configuration options</span></span>
* <span data-ttu-id="93d60-137">**TimeToRun**: 테스트가 성공적으로 완료될 때까지 실행되는 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="93d60-138">유효성 검사를 실패하기 전에 테스트가 일찍 완료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="93d60-139">**MaxClusterStabilizationTimeout**: 클러스터가 정상 상태가 될 때까지 기다리는 최대 시간입니다. 이 시간이 지나면 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="93d60-140">클러스터 상태가 정상인지, 서비스 상태가 정상인지, 서비스 파티션에 대해 대상 복제본 세트 크기가 달성되었는지, InBuild 복제본이 없는지에 대한 검사가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="93d60-141">**MaxConcurrentFaults**: 각 반복에서 유도되는 동시 오류의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="93d60-142">숫자가 클수록 테스트가 공격적이므로 더 복잡한 장애 조치(failover)와 전환 조합으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="93d60-143">외부 오류가 없으면 이 숫자를 얼마나 높게 구성하든 쿼럼 또는 데이터 손실이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="93d60-144">**EnableMoveReplicaFaults**: 주 복제본 또는 보조 복제본을 이동하게 만드는 오류를 설정하거나 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="93d60-145">이러한 오류는 기본적으로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="93d60-146">**WaitTimeBetweenIterations**: 반복 사이의 대기 시간입니다(예: 오류 및 그에 해당하는 유효성 검사 후).</span><span class="sxs-lookup"><span data-stu-id="93d60-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="93d60-147">비정상 상황 테스트를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="93d60-147">How to run the chaos test</span></span>
<span data-ttu-id="93d60-148">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="93d60-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="93d60-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d60-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="93d60-150">장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="93d60-150">Failover test</span></span>
<span data-ttu-id="93d60-151">장애 조치(failover) 테스트 시나리오는 비정상 상황 테스트의 한 버전으로써 특정 서비스 파티션을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="93d60-152">다른 서비스에는 영향을 주지 않고 장애 조치(failover)가 특정 서비스 파티션에 미치는 영향을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="93d60-153">대상 파티션 정보 및 기타 매개 변수를 사용하여 테스트를 구성할 경우 C# API 또는 PowerShell을 사용하는 클라이언트 쪽 도구로 실행되어 서비스 파티션에 대한 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="93d60-154">한 쪽에서 비즈니스 논리가 실행되어 작업을 제공하는 동안 일련의 시뮬레이션된 오류 및 서비스 유효성 검사를 통해 시나리오가 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="93d60-155">서비스 유효성 검사에서 오류가 발생하면 추가 조사가 필요한 문제가 있다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="93d60-156">장애 조치(failover) 테스트에서 시뮬레이션하는 오류</span><span class="sxs-lookup"><span data-stu-id="93d60-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="93d60-157">파티션이 호스팅되는 배포된 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="93d60-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="93d60-158">주/보조 복제본 또는 상태 비저장 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="93d60-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="93d60-159">주/보조 복제본 다시 시작(서비스가 지속되는 경우)</span><span class="sxs-lookup"><span data-stu-id="93d60-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="93d60-160">주 복제본 이동</span><span class="sxs-lookup"><span data-stu-id="93d60-160">Move a primary replica</span></span>
* <span data-ttu-id="93d60-161">보조 복제본 이동</span><span class="sxs-lookup"><span data-stu-id="93d60-161">Move a secondary replica</span></span>
* <span data-ttu-id="93d60-162">파티션 다시 시작</span><span class="sxs-lookup"><span data-stu-id="93d60-162">Restart the partition</span></span>

<span data-ttu-id="93d60-163">장애 조치(failover) 테스트는 선택된 오류를 유도한 후 서비스에 대해 유효성 검사를 실행하여 안정화합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="93d60-164">비정상 상황 테스트에서 다중 오류가 가능한 것과는 달리 장애 조치(failover) 테스트는 오류를 한 번에 하나씩만 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="93d60-165">각 오류 후 서비스 파티션이 구성된 제한 시간 내에 안정화되지 않으면 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="93d60-166">이 테스트는 안전 오류만 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-166">The test induces only safe faults.</span></span> <span data-ttu-id="93d60-167">다시 말해서 외부 오류가 없으면 쿼럼 또는 데이터 손실이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="93d60-168">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="93d60-168">Important configuration options</span></span>
* <span data-ttu-id="93d60-169">**PartitionSelector**: 대상으로 삼을 파티션을 지정하는 선택기 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="93d60-170">**TimeToRun**: 테스트가 완료될 때까지 실행되는 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="93d60-171">**MaxServiceStabilizationTimeout**: 클러스터가 정상 상태가 될 때까지 기다리는 최대 시간입니다. 이 시간이 지나면 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="93d60-172">서비스 상태가 정상인지, 모든 파티션에 대해 대상 복제본 세트 크기가 달성되었는지, InBuild 복제본이 없는지에 대한 검사가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="93d60-173">**WaitTimeBetweenFaults**: 모든 오류 및 유효성 검사 주기 사이에 대기하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93d60-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="93d60-174">장애 조치(failover) 테스트를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="93d60-174">How to run the failover test</span></span>
<span data-ttu-id="93d60-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="93d60-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // The chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create the scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="93d60-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="93d60-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
