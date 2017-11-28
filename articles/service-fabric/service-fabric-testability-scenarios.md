---
title: "Azure microservices에 대 한 aaaCreate chaos 및 장애 조치 테스트 | Microsoft Docs"
description: "서비스 패브릭 hello를 사용 하 여 chaos 테스트 및 장애 조치 tooinduce 오류 시나리오를 테스트 하 고 서비스의 hello 신뢰성을 확인 합니다."
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
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="d5bb6-103">테스트 용이성 시나리오</span><span class="sxs-lookup"><span data-stu-id="d5bb6-103">Testability scenarios</span></span>
<span data-ttu-id="d5bb6-104">클라우드 인프라 같은 대규모 분산 시스템은 본질적으로 불안정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="d5bb6-105">Azure 서비스 패브릭 제공 개발자 hello 기능 toowrite 서비스 toorun 신뢰할 수 없는 인프라를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="d5bb6-106">순서 toowrite 고품질 서비스에서는 개발자 들이 서비스의 신뢰할 수 없는 인프라 tootest hello 안정성 이러한 toobe 수 tooinduce을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="d5bb6-107">hello 오류 분석 서비스 오류의 hello 존재의 개발자 hello 기능 tooinduce 오류 동작 tootest 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="d5bb6-108">그러나 특정 대상을 통한 오류 시뮬레이션으로는 한계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="d5bb6-109">또한 테스트 tootake hello hello 테스트 시나리오를 사용 하 여 서비스 패브릭에서: chaos 테스트 및 장애 조치 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="d5bb6-110">이러한 시나리오는 정상 및 비정상 시간의 오랜된 기간 동안 hello 클러스터 전체에서 인터리빙된 연속 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="d5bb6-111">테스트 hello 환율 및 종류의 오류와 함께 구성 되 면 C# Api 또는 PowerShell, hello 클러스터에서 toogenerate 오류 및 서비스를 통해 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="d5bb6-112">ChaosTestScenario는 회복력이 뛰어난 서비스 기반 비정상 상황으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="d5bb6-113">Toohello 새 문서를 참조 하십시오 [Chaos 제어](service-fabric-controlled-chaos.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="d5bb6-114">비정상 상황 테스트</span><span class="sxs-lookup"><span data-stu-id="d5bb6-114">Chaos test</span></span>
<span data-ttu-id="d5bb6-115">hello chaos 시나리오 hello 전체 서비스 패브릭 클러스터 전체에서 오류를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="d5bb6-116">hello 시나리오는 일반적으로 볼 수 개월 또는 수 년 tooa에서 몇 시간 오류를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="d5bb6-117">hello 높은 오류 숙박료가 인터리브 오류의 hello 조합 그렇지 않으면 누락 코너 케이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="d5bb6-118">이 hello 서비스 hello 코드 품질에서 향상을 tooa 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="d5bb6-119">Hello chaos 테스트에서 시뮬레이션 된 오류</span><span class="sxs-lookup"><span data-stu-id="d5bb6-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="d5bb6-120">노드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d5bb6-120">Restart a node</span></span>
* <span data-ttu-id="d5bb6-121">배포된 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d5bb6-121">Restart a deployed code package</span></span>
* <span data-ttu-id="d5bb6-122">복제본 제거</span><span class="sxs-lookup"><span data-stu-id="d5bb6-122">Remove a replica</span></span>
* <span data-ttu-id="d5bb6-123">복제본 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d5bb6-123">Restart a replica</span></span>
* <span data-ttu-id="d5bb6-124">주 복제본 이동(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="d5bb6-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="d5bb6-125">보조 복제본 이동(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="d5bb6-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="d5bb6-126">hello chaos 테스트 오류를 여러 차례 반복 실행 하 고 hello에 대 한 클러스터 유효성 검사 일정 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="d5bb6-127">hello 시간 toosucceed 유효성 검사 및 클러스터 toostabilize hello에 대 한 구성 가능한 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="d5bb6-128">hello 시나리오에는 단일 클러스터 유효성 검사 실패에 도달 하면 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="d5bb6-129">예를 들어 테스트는 3 개의 동시 오류 최대 1 시간 동안 toorun를 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="d5bb6-130">hello 테스트 유도 세 개의 오류를 한 다음 hello 클러스터 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="d5bb6-131">hello 테스트 hello 클러스터 비정상 또는 1 시간까지 hello 이전 단계를 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="d5bb6-132">Hello 클러스터는 반복에서 비정상 상태가 되 면, 즉 구성 된 시간 내 안정화 하지 않는 면 hello 테스트 예외와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="d5bb6-133">이 예외는 뭔가가 잘못되었으며 자세한 조사가 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="d5bb6-134">현재 형태의 hello 오류 생성 엔진 hello chaos 테스트에만 안전 오류를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="d5bb6-135">이 hello 없는 경우 외부 오류, 쿼럼 또는 데이터 손실이 발생 하지 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="d5bb6-136">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="d5bb6-136">Important configuration options</span></span>
* <span data-ttu-id="d5bb6-137">**TimeToRun**: 총 시간 해당 hello 테스트가 성공적으로 완료 하기 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="d5bb6-138">hello 테스트 유효성 검사 실패 하는 대신 이전 마칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="d5bb6-139">**MaxClusterStabilizationTimeout**: 시간 toowait hello 클러스터 toobecome hello 테스트 실패 전에 정상 상태에 대 한 최대 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="d5bb6-140">hello 수행 되는 검사 클러스터 상태가 양호함 여부, 서비스 상태를 확인, hello 대상 복제 세트 크기 이루어집니다 hello 서비스 파티션에 대 한 않으며 InBuild 복제본이 없는 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="d5bb6-141">**MaxConcurrentFaults**: 각 반복에서 유도되는 동시 오류의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="d5bb6-142">hello 값이 클수록 hello, 따라서 그 결과 더 복잡 한 장애 조치를 수행 하 고 전환 조합 보다 적극적으로 hello 테스트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="d5bb6-143">hello 테스트 없는 경우 외부 오류 없습니다 것은 어떻습니까이 구성에 관계 없이 쿼럼 또는 데이터 손실 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="d5bb6-144">**EnableMoveReplicaFaults**: 사용 하거나 기본 또는 보조 복제본의 hello hello 이동을 유발 하는 오류를 hello를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="d5bb6-145">이러한 오류는 기본적으로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="d5bb6-146">**WaitTimeBetweenIterations**: 즉, 오류 및 해당 유효성 검사의 라운드 후의 반복 간 시간 toowait입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="d5bb6-147">Toorun hello chaos 테스트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d5bb6-147">How toorun hello chaos test</span></span>
<span data-ttu-id="d5bb6-148">C# 샘플</span><span class="sxs-lookup"><span data-stu-id="d5bb6-148">C# sample</span></span>

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

        // hello chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create hello scenario class and execute it asynchronously.
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

<span data-ttu-id="d5bb6-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5bb6-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="d5bb6-150">장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="d5bb6-150">Failover test</span></span>
<span data-ttu-id="d5bb6-151">hello 장애 조치 테스트 시나리오에는 특정 서비스 파티션을 대상으로 하는 hello chaos 테스트 시나리오의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="d5bb6-152">Hello 다른 서비스 영향을 받지 않고 그대로 유지 하면서 장애 조치의 특정 서비스 파티션에 hello 효과 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="d5bb6-153">Hello 대상 파티션 정보 및 다른 매개 변수와 함께 구성 되 면 서비스 파티션에 대 한 C# Api 또는 PowerShell toogenerate 오류를 사용 하는 클라이언트 쪽 도구도 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="d5bb6-154">비즈니스 논리 실행 hello 쪽 tooprovide에서 작업 하는 동안 hello 시나리오는 일련의 시뮬레이션 된 오류와 서비스 유효성 검사를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="d5bb6-155">서비스 유효성 검사에서 오류가 발생하면 추가 조사가 필요한 문제가 있다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="d5bb6-156">Hello 장애 조치 테스트에서 시뮬레이션 된 오류</span><span class="sxs-lookup"><span data-stu-id="d5bb6-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="d5bb6-157">Hello 파티션 호스팅되는 배포 된 코드 패키지를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d5bb6-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="d5bb6-158">주/보조 복제본 또는 상태 비저장 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="d5bb6-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="d5bb6-159">주/보조 복제본 다시 시작(서비스가 지속되는 경우)</span><span class="sxs-lookup"><span data-stu-id="d5bb6-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="d5bb6-160">주 복제본 이동</span><span class="sxs-lookup"><span data-stu-id="d5bb6-160">Move a primary replica</span></span>
* <span data-ttu-id="d5bb6-161">보조 복제본 이동</span><span class="sxs-lookup"><span data-stu-id="d5bb6-161">Move a secondary replica</span></span>
* <span data-ttu-id="d5bb6-162">Hello 파티션 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d5bb6-162">Restart hello partition</span></span>

<span data-ttu-id="d5bb6-163">선택한 오류를 적용 하 고 hello 서비스 tooensure에서 유효성 검사를의 안정성 실행 하는 hello 장애 조치 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="d5bb6-164">hello 장애 조치 테스트 hello chaos 테스트에서 여러 오류 시간, 달리 toopossible에서 오류 하나에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="d5bb6-165">Hello 서비스 파티션 hello 구성 된 제한 시간 내 각 오류 후 안정화 하지 않는 hello 테스트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="d5bb6-166">hello 테스트를 안전 하 게 보호 오류만 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-166">hello test induces only safe faults.</span></span> <span data-ttu-id="d5bb6-167">다시 말해서 외부 오류가 없으면 쿼럼 또는 데이터 손실이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="d5bb6-168">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="d5bb6-168">Important configuration options</span></span>
* <span data-ttu-id="d5bb6-169">**PartitionSelector**: toobe 대상으로 해야 하는 hello 파티션을 지정 하는 선택기 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="d5bb6-170">**TimeToRun**: 총 시간 hello 테스트를 완료 하기 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="d5bb6-171">**MaxServiceStabilizationTimeout**: 시간 toowait hello 클러스터 toobecome hello 테스트 실패 전에 정상 상태에 대 한 최대 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="d5bb6-172">hello 수행 되는 검사는 서비스 상태 인지 확인 하 고 hello 대상 복제 세트 크기 이루어집니다 모든 파티션에 대 한 InBuild 복제본이 없는 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="d5bb6-173">**WaitTimeBetweenFaults**: 모든 오류 및 유효성 검사 주기 사이의 시간 toowait입니다.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="d5bb6-174">Toorun hello 장애 조치 테스트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d5bb6-174">How toorun hello failover test</span></span>
<span data-ttu-id="d5bb6-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="d5bb6-175">**C#**</span></span>

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

        // hello chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create hello scenario class and execute it asynchronously.
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


<span data-ttu-id="d5bb6-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="d5bb6-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
