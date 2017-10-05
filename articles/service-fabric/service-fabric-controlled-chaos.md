---
title: "Service Fabric 클러스터에서 비정상 상황 유도 | Microsoft Docs"
description: "오류 삽입 및 클러스터 분석 서비스 API를 사용하여 클러스터의 비정상 상황을 관리합니다."
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
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="36903-103">Service Fabric 클러스터에서 제어되는 비정상 상황 유도</span><span class="sxs-lookup"><span data-stu-id="36903-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="36903-104">클라우드 인프라와 같은 대규모 분산 시스템은 기본적으로 안정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="36903-105">Azure Service Fabric을 사용하면 개발자들은 불안정한 인프라 위에 안정적인 분산 서비스를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="36903-106">불안정한 인프라 위에 강력한 분산 서비스를 작성하려는 경우 기반이 되는 불안정한 인프라가 결함으로 인해 복잡한 상태 전환을 겪을 때 개발자는 서비스의 안정성을 테스트할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="36903-107">[오류 삽입 및 클러스터 분석 서비스](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview)(오류 분석 서비스라고도 함)는 개발자에게 서비스를 테스트할 수 있도록 오류를 유도하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="36903-108">[파티션 다시 시작](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps)과 같은 이러한 대상 시뮬레이트 오류는 가장 일반적인 상태 전환을 실행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="36903-109">그러나 대상 시뮬레이트 오류는 기본적으로 편향되어 있으므로 예측하기 어렵고 오래 진행되는 복잡한 상태 전환 시퀀스로만 나타나는 버그는 놓칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="36903-110">편향되지 않는 테스트를 위해서는 비정상 상황을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="36903-111">비정상 상황은 장기간에 걸쳐 클러스터 전체에서 정상적 및 비정상적인 주기적 인터리브 오류를 지속적으로 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="36903-112">오류의 비율 및 종류로 비정상 상황을 구성하면 C# 또는 PowerShell API를 통해 비정상 상황을 시작함으로써 클러스터 및 서비스에서 오류를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="36903-113">지정된 시간(예: 1시간) 동안 실행된 다음 자동으로 중지되도록 비정상 상황을 구성하거나, 언제든지 StopChaos API(C# 또는 PowerShell)를 호출하여 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="36903-114">현재 양식에서, 비정상 상황은 안전 오류만 유도합니다. 즉, 외부 오류가 없으면 쿼럼 손실 또는 데이터 손실이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="36903-115">비정상 상황이 실행되는 동안 현재 실행의 상태를 캡처하는 다양한 이벤트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="36903-116">예를 들어 ExecutingFaultsEvent에는 비정상 상황이 해당 반복에서 실행하기로 결정한 모든 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="36903-117">ValidationFailedEvent에는 클러스터 유효성 검사 동안 발견된 유효성 검사 오류(상태 또는 안정성 문제)의 세부 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="36903-118">GetChaosReport API(C# 또는 PowerShell)를 호출하여 비정상 상황 실행 보고서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="36903-119">이러한 이벤트는 두 가지 구성 **MaxStoredChaosEventCount**(기본값 25000) 및 **StoredActionCleanupIntervalInSeconds**(기본값 3600)에 따라 잘림 정책이 적용되는 [신뢰할 수 있는 사전](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections)에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="36903-120">가장 최근의 *MaxStoredChaosEventCount* 이벤트를 제외하고 비정상 상황이 확인하는 모든 *StoredActionCleanupIntervalInSeconds* 이벤트는 신뢰할 수 있는 사전에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="36903-121">비정상 상황에서 유도되는 오류</span><span class="sxs-lookup"><span data-stu-id="36903-121">Faults induced in Chaos</span></span>
<span data-ttu-id="36903-122">비정상 상황에서는 전체 Service Fabric 클러스터에서 오류가 생성되며 수개월 또는 수년에 걸쳐 확인된 오류가 몇 시간으로 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="36903-123">인터리브 오류를 높은 오류 비율과 결합하면 놓치기 쉬운 특이한 사례를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="36903-124">이러한 비정상 상황에 대처하는 연습을 통해 서비스 코드 품질을 대폭 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="36903-125">비정상 상황은 다음 범주에서 오류를 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="36903-126">노드 다시 시작</span><span class="sxs-lookup"><span data-stu-id="36903-126">Restart a node</span></span>
* <span data-ttu-id="36903-127">배포된 코드 패키지 다시 시작</span><span class="sxs-lookup"><span data-stu-id="36903-127">Restart a deployed code package</span></span>
* <span data-ttu-id="36903-128">복제본 제거</span><span class="sxs-lookup"><span data-stu-id="36903-128">Remove a replica</span></span>
* <span data-ttu-id="36903-129">복제본 다시 시작</span><span class="sxs-lookup"><span data-stu-id="36903-129">Restart a replica</span></span>
* <span data-ttu-id="36903-130">주 복제본 이동(구성 가능)</span><span class="sxs-lookup"><span data-stu-id="36903-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="36903-131">보조 복제본 이동(구성 가능)</span><span class="sxs-lookup"><span data-stu-id="36903-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="36903-132">비정상 상황에서는</span><span class="sxs-lookup"><span data-stu-id="36903-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="36903-133">지정된 기간 동안 오류 및 클러스터 유효성 검사가 여러 차례 반복해서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="36903-134">클러스터가 안정화되고 유효성 검사가 성공하는 데 걸리는 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="36903-135">클러스터 유효성 검사에 오류가 있으면 비정상 상황이 생성되며 UTC 타임스탬프 및 오류 세부 정보로 ValidationFailedEvent가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="36903-136">예를 들어 비정상 상황 인스턴스가 1시간 동안 실행되고 최대 세 가지 오류가 동시에 발생하도록 설정되었다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="36903-137">비정상 상황은 세 개의 오류를 유도한 다음 클러스터 상태의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="36903-138">또한 StopChaosAsync API를 통해 명시적으로 서비스가 중지되거나 1시간이 경과할 때까지 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="36903-139">반복 과정 중에 클러스터가 비정상 상태가 되면(전달된 MaxClusterStabilizationTimeout 내에서 안정화되지 못함) 비정상 상황은 ValidationFailedEvent를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="36903-140">이 이벤트는 무언가 잘못되었으며 자세한 조사가 필요할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36903-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="36903-141">비정상 상황이 유도한 오류를 가져오려면 GetChaosReport API(powershell 또는 C#)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="36903-142">이 API는 전달된 연속 토큰 또는 전달된 시간 범위를 기준으로 비정상 상황 보고서의 다음 세그먼트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36903-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="36903-143">비정상 상황 보고서의 다음 세그먼트를 가져오도록 ContinuationToken을 지정하거나, StartTimeUtc 및 EndTimeUtc를 통해 시간 범위를 지정할 수 있지만 ContinuationToken과 시간 범위를 같은 호출 내에서 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="36903-144">100개가 넘는 비정상 상황 이벤트가 있는 경우 비정상 상황 보고서는 세그먼트에 100개 이하의 비정상 상황 이벤트가 포함되어 있는 세그먼트로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="36903-145">중요 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="36903-145">Important configuration options</span></span>
* <span data-ttu-id="36903-146">**TimeToRun**: 성공적으로 완료될 때까지 비정상 상황이 실행되는 총 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="36903-147">StopChaos API를 통해 TimeToRun 기간 동안 실행되기 전에 비정상 상황을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="36903-148">**MaxClusterStabilizationTimeout**: 클러스터가 정상 상태가 될 때까지 기다리는 최대 시간입니다. 그 이후에는 ValidationFailedEvent가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="36903-149">이를 통해 복구되는 동안 클러스터의 부하를 줄일 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="36903-150">수행되는 검사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-150">The checks performed are:</span></span>
  * <span data-ttu-id="36903-151">클러스터 상태가 정상인 경우</span><span class="sxs-lookup"><span data-stu-id="36903-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="36903-152">서비스 상태가 정상인 경우</span><span class="sxs-lookup"><span data-stu-id="36903-152">If the service health is OK</span></span>
  * <span data-ttu-id="36903-153">서비스 파티션에 대해 목표 복제본 세트 크기가 달성된 경우</span><span class="sxs-lookup"><span data-stu-id="36903-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="36903-154">InBuild 복사본이 없음</span><span class="sxs-lookup"><span data-stu-id="36903-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="36903-155">**MaxConcurrentFaults**: 각 반복에서 유도되는 동시 오류의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="36903-156">이 수가 높을수록 비정상 상황은 좀 더 공격적으로 나타나며, 클러스터에 나타나는 장애 조치 및 상태 전환 조합도 좀 더 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="36903-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="36903-157">*MaxConcurrentFaults* 값 크기에 관계 없이, 비정상 상황은 외부 오류가 없을 때 쿼럼 또는 데이터 손실이 없도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="36903-158">**EnableMoveReplicaFaults**: 주 복제본 또는 보조 복제본을 이동하게 만드는 오류를 설정하거나 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="36903-159">이러한 오류는 기본적으로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="36903-160">**WaitTimeBetweenIterations**: 반복 사이의 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="36903-161">즉, 일련의 오류를 실행하고 클러스터 상태에 대한 해당 유효성 검사를 완료한 후에 비정상 상황이 일시 중지되는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="36903-162">이 값이 높을수록 평균 오류 삽입 속도는 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="36903-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="36903-163">**WaitTimeBetweenFaults**: 단일 반복에서 두 개의 연속 오류 사이에 대기하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="36903-164">이 값이 높을수록 오류의 동시성(또는 오류 간 중복)이 낮아집니다.</span><span class="sxs-lookup"><span data-stu-id="36903-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="36903-165">**ClusterHealthPolicy**: 클러스터 상태 정책은 비정상 상황 반복 간에 클러스터의 상태를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36903-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="36903-166">클러스터 상태에 오류가 있거나 오류 실행 중에 예기치 않은 예외가 발생하면 비정상 상황은 클러스터에 다시 복구할 시간을 제공하기 위해 30분 동안 대기했다가 다음 상태 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="36903-167">**Context**: (string, string) 형식의 키-값 쌍 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="36903-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="36903-168">비정상 상황 실행에 대한 정보를 기록하기 위해 맵이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="36903-169">이러한 쌍은 100개 이하로만 존재할 수 있으며 각 문자열(키 또는 값)은 4095자 이하로만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36903-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="36903-170">비정상 상황 실행 시작 기능이 특정 실행에 대한 컨텍스트를 선택적으로 저장할 수 있게 이러한 맵을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36903-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="36903-171">비정상 상황을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="36903-171">How to run Chaos</span></span>

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
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
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
                // If a StoppedEvent is found, exit the loop.
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
