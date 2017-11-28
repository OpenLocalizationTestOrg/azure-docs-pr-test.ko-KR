---
title: "서비스 패브릭에서 Chaos 클러스터 aaaInduce | Microsoft Docs"
description: "Hello 클러스터의 오류 삽입 및 클러스터 분석 서비스 Api toomanage Chaos를 사용합니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="d0024-103">Service Fabric 클러스터에서 제어되는 비정상 상황 유도</span><span class="sxs-lookup"><span data-stu-id="d0024-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="d0024-104">클라우드 인프라와 같은 대규모 분산 시스템은 기본적으로 안정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="d0024-105">Azure 서비스 패브릭 개발자 toowrite 신뢰할 수 있는 배포 된 서비스를 신뢰할 수 없는 인프라를 기반으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="d0024-106">toowrite 불안정 한 인프라를 기반으로 강력한 분산된 서비스, 개발자 들이 서비스의 toobe 수 tootest hello 안정성 해야 신뢰할 수 없는 인프라 내부 hello 복잡 한 상태 전환 통과 하는 동안 due toofaults 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="d0024-107">hello [오류 삽입 및 클러스터 분석 서비스](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (라고도 hello 오류 Analysis Service)에서는 개발자가 hello 기능 tooinduce 서비스 데 tootest 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="d0024-108">같은 오류를 시뮬레이션 된 대상으로 이러한 [파티션을 다시 시작](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), hello 가장 일반적인 상태 전환을 실행 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="d0024-109">그러나 대상 시뮬레이트 오류는 기본적으로 편향되어 있으므로 예측하기 어렵고 오래 진행되는 복잡한 상태 전환 시퀀스로만 나타나는 버그는 놓칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="d0024-110">편향되지 않는 테스트를 위해서는 비정상 상황을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="d0024-111">Chaos 시간의 오랜된 기간 동안 hello 클러스터 전체에서 정기적으로 인터리브 오류 (정상 및 비정상)을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="d0024-112">Hello 환율 및 hello 종류의 오류와 함께 Chaos를 구성한 후에 hello 클러스터에서 한 서비스에서 오류를 생성 하는 C# 또는 Powershell API toostart 통해 Chaos를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="d0024-113">Chaos toorun Chaos 자동으로 중지 되는 지정한 기간 동안 (예: 1 시간)에 대 한 구성 하거나 toostop StopChaos API (C# 또는 Powershell)을 호출할 수 있습니다 언제 든 지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="d0024-114">현재 형태의 Chaos 적용만 안전 오류 의미 하는 외부 오류 hello 없는 경우 쿼럼 손실, 또는 데이터 손실이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="d0024-115">Chaos 실행 되는 동안 hello 순간에 실행 하는 hello의 hello 상태를 캡처하는 다양 한 이벤트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="d0024-116">예를 들어 한 ExecutingFaultsEvent Chaos가 해당 반복에서 tooexecute를 결정 하는 모든 hello 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="d0024-117">ValidationFailedEvent hello hello 클러스터 유효성 검사 중 발견 된 유효성 검사 실패 (상태 또는 안정성 문제)의 hello 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="d0024-118">Hello Chaos 실행 tooget hello 보고서 GetChaosReport API (C# 또는 Powershell)을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="d0024-119">이러한 이벤트는 두 가지 구성 **MaxStoredChaosEventCount**(기본값 25000) 및 **StoredActionCleanupIntervalInSeconds**(기본값 3600)에 따라 잘림 정책이 적용되는 [신뢰할 수 있는 사전](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections)에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="d0024-120">모든 *StoredActionCleanupIntervalInSeconds* Chaos 검사 및 모든 하지만 hello 가장 최근의 *MaxStoredChaosEventCount* 이벤트 hello 신뢰할 수 있는 사전에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="d0024-121">비정상 상황에서 유도되는 오류</span><span class="sxs-lookup"><span data-stu-id="d0024-121">Faults induced in Chaos</span></span>
<span data-ttu-id="d0024-122">Chaos는 hello 전체 서비스 패브릭 클러스터 전체에서 오류를 생성 하 고 몇 시간에 월 또는 년 단위로 표시 되는 오류를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="d0024-123">hello 높은 오류 숙박료가 인터리브 오류의 hello 조합 그렇지 않으면 누락 될 수 있는 코너 케이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="d0024-124">이 연습 Chaos의 hello 서비스의 코드 품질 hello에에서 tooa 향상을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="d0024-125">Chaos는 hello 다음 범주에서에서 오류를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="d0024-126">노드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d0024-126">Restart a node</span></span>
* <span data-ttu-id="d0024-127">배포된 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d0024-127">Restart a deployed code package</span></span>
* <span data-ttu-id="d0024-128">복제본 제거</span><span class="sxs-lookup"><span data-stu-id="d0024-128">Remove a replica</span></span>
* <span data-ttu-id="d0024-129">복제본 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d0024-129">Restart a replica</span></span>
* <span data-ttu-id="d0024-130">주 복제본 이동(구성 가능)</span><span class="sxs-lookup"><span data-stu-id="d0024-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="d0024-131">보조 복제본 이동(구성 가능)</span><span class="sxs-lookup"><span data-stu-id="d0024-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="d0024-132">비정상 상황에서는</span><span class="sxs-lookup"><span data-stu-id="d0024-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="d0024-133">각 반복 오류와 hello에 대 한 클러스터 유효성 검사 기간이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="d0024-134">Hello 시간 toosucceed 유효성 검사 및 클러스터 toostabilize hello에 대 한 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="d0024-135">클러스터 유효성 검사에 오류가 있으면 Chaos를 생성 하 고는 ValidationFailedEvent hello UTC 타임 스탬프 및 hello 실패 세부 정보를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="d0024-136">예를 들어 인스턴스의 Chaos toorun는 3 개의 동시 오류 최대 한 시간에 설정 된 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="d0024-137">Chaos 세 개의 오류를 적용 한 다음 hello 클러스터 상태에 검증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="d0024-138">반복 하면서 이전 hello 명시적으로 중지 된 hello StopChaosAsync API 통해 또는 한 시간 될 때까지 단계를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="d0024-139">Hello 클러스터 반복에서 비정상 상태가 되는 경우 (즉, 해당 않습니다 하지 안정화 MaxClusterStabilizationTimeout 전달 기능에 hello 내), Chaos는 ValidationFailedEvent를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="d0024-140">이 이벤트는 무언가 잘못되었으며 자세한 조사가 필요할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="d0024-141">Chaos 인 한 오류를 처리 하는 tooget GetChaosReport API (powershell 또는 C#)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="d0024-142">hello API hello hello 전달 된 연속 토큰 또는 hello 전달 된 시간 범위에 따라 hello Chaos 보고서의 다음 세그먼트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="d0024-143">ContinuationToken tooget hello hello Chaos 보고서의 다음 세그먼트 hello 또는 StartTimeUtc 및 EndTimeUtc를 통해 hello 시간 범위를 지정할 수 있지만 hello에 ContinuationToken hello와 hello 시간 범위를 지정할 수 없습니다 지정 하거나 동일한 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="d0024-144">100 개가 넘는 Chaos 이벤트가 없는 hello Chaos 보고서 세그먼트 100 개 이하의 Chaos 이벤트에 포함 된 세그먼트에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="d0024-145">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="d0024-145">Important configuration options</span></span>
* <span data-ttu-id="d0024-146">**TimeToRun**: 성공적으로 완료될 때까지 비정상 상황이 실행되는 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="d0024-147">Hello TimeToRun 기간에 대 한 hello StopChaos API를 통해 실행 되기 전에 Chaos를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="d0024-148">**MaxClusterStabilizationTimeout**: hello 최대한의 정상는 ValidationFailedEvent 발생 하기 전에 hello 클러스터 toobecome에 대 한 시간 toowait 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="d0024-149">이 대기는 복구 되는 동안 hello 클러스터에서 tooreduce hello load입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="d0024-150">수행 되는 hello 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-150">hello checks performed are:</span></span>
  * <span data-ttu-id="d0024-151">Hello 클러스터 상태가 양호함 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d0024-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="d0024-152">Hello 서비스 상태를 확인 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d0024-152">If hello service health is OK</span></span>
  * <span data-ttu-id="d0024-153">Hello 대상 복제본 집합 크기는 이루어졌는지 hello 서비스 파티션에 대 한</span><span class="sxs-lookup"><span data-stu-id="d0024-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="d0024-154">InBuild 복사본이 없음</span><span class="sxs-lookup"><span data-stu-id="d0024-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="d0024-155">**MaxConcurrentFaults**: hello 각 반복에서 발생 하는 동시 오류의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="d0024-156">hello hello 크면, Chaos 이며 hello 장애 조치 및 hello 상태 전환 하는 조합 hello 클러스터 통과 하는 복잡 한도 보다 적극적으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0024-157">이와 상관 없이 어떻게 높은 값 *MaxConcurrentFaults* Chaos에 외부 오류-hello 없는 경우에서 쿼럼 손실 또는 데이터 손실 없습니다-보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="d0024-158">**EnableMoveReplicaFaults**: hello 기본 또는 보조 복제본 toomove 유발 하는 hello 부재를 사용 하지 않도록 설정 하거나 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="d0024-159">이러한 오류는 기본적으로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="d0024-160">**WaitTimeBetweenIterations**: 반복 간 시간 toowait hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="d0024-161">즉, hello Chaos 장애와 hello 클러스터의 hello 상태 hello 해당 유효성 검사를 완료 하지 테스트를 수행 함으로써 후 일시 중지 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="d0024-162">hello hello 값이 높을수록 더 낮은 hello hello 평균 오류 삽입 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="d0024-163">**WaitTimeBetweenFaults**: hello 양의 시간 toowait 단일 반복에서 두 개의 연속 된 오류 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="d0024-164">hello 값을 높게 hello의 더 낮은 hello 동시성 hello (또는 겹치지 hello) 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="d0024-165">**ClusterHealthPolicy**: 클러스터 상태 정책이 사용 되는 toovalidate hello 클러스터 상태에 hello Chaos 반복 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="d0024-166">Hello 클러스터 상태는 오류가 발생 하거나 예기치 않은 예외가 발생 하면 오류 실행 하는 동안 Chaos hello 다음 상태 확인-일부 시간 toorecuperate tooprovide hello 클러스터 30 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="d0024-167">**Context**: (string, string) 형식의 키-값 쌍 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="d0024-168">hello 맵은 실행 Chaos hello에 대 한 정보를 사용 하는 toorecord 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="d0024-169">이러한 쌍은 100개 이하로만 존재할 수 있으며 각 문자열(키 또는 값)은 4095자 이하로만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="d0024-170">이 맵은 hello 특정 실행에 대 한 hello 실행 Chaos toooptionally 저장소 hello 컨텍스트 hello 시작으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0024-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="d0024-171">어떻게 toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="d0024-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
