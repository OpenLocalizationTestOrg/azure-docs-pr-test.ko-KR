---
title: "Azure microservices의 aaaSimulate 오류 | Microsoft Docs"
description: "이 문서는 Microsoft Azure 서비스 패브릭에서 찾을 수 hello 테스트 용이성 동작에 대 한 설명입니다."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="0d5c0-103">테스트 용이성 작업</span><span class="sxs-lookup"><span data-stu-id="0d5c0-103">Testability actions</span></span>
<span data-ttu-id="0d5c0-104">순서 toosimulate 신뢰할 수 없는 인프라에서에서 Azure 서비스 패브릭 제공 hello 개발자 toosimulate 방법 사용 하면 다양 한 실제 오류 및 상태 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="0d5c0-105">이러한 작업을 테스트 용이성 작업이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-105">These are exposed as testability actions.</span></span> <span data-ttu-id="0d5c0-106">hello 작업에는 특정 오류 삽입, 상태 전환을 또는 유효성 검사 발생 하는 낮은 수준의 Api hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="0d5c0-107">이러한 작업을 결합하여 서비스에 대한 포괄적인 테스트 시나리오를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="0d5c0-108">서비스 패브릭은 이러한 작업으로 구성된 몇 가지 일반 테스트 시나리오를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="0d5c0-109">Tootest 일반적인 상태 전환 및 실패의 경우 신중 하 게 선택 되는 이러한 기본 제공 시나리오를 활용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="0d5c0-110">그러나 동작 하는 포함 되지 않은 기본 제공 시나리오 hello 아직 또는 사용자 지정 응용 프로그램에 맞게 조정 된 시나리오에 대 한 tooadd 검사 하려는 경우 toocreate 사용 되는 사용자 지정 테스트 시나리오를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="0d5c0-111">C# hello 동작의 구현은 hello System.Fabric.dll 어셈블리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="0d5c0-112">hello 시스템 패브릭 PowerShell 모듈은 hello Microsoft.ServiceFabric.Powershell.dll 어셈블리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="0d5c0-113">런타임 설치의 일환으로, hello ServiceFabric PowerShell 모듈 사용 편의성에 대 한 설치 된 tooallow 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="0d5c0-114">정상적인 오류 작업과 비정상적인 오류 작업 비교</span><span class="sxs-lookup"><span data-stu-id="0d5c0-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="0d5c0-115">테스트 용이성 작업은 두 주요 버킷으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="0d5c0-116">비정상적 오류: 이러한 오류는 컴퓨터 재시작, 프로세스 충돌 같은 실패를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="0d5c0-117">이러한 오류의 경우 프로세스의 실행 컨텍스트 hello 갑자기 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="0d5c0-118">즉, hello 응용 프로그램 다시 시작 하기 전에 hello 상태의 정리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="0d5c0-119">정상적인 오류: 이러한 오류는 부하 분산에 의해 트리거되는 복제본 이동 또는 삭제 등의 정상적인 작업을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="0d5c0-120">이러한 경우 hello 서비스 hello에 대 한 알림을 닫기 가져오고 종료 하기 전에 hello 상태를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="0d5c0-121">더 나은 품질 유효성 검사에 대 한 hello 서비스를 실행 및 다양 한 오류 정상 및 비정상을 유도 하는 동안 비즈니스 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="0d5c0-122">비정상적 오류 hello 서비스 프로세스가 갑자기 일부 워크플로의 hello 중간에 종료 되는 시나리오를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="0d5c0-123">이 서비스 복제본 hello 서비스 패브릭에서 복원 되 면 hello 복구 경로 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="0d5c0-124">데이터의 일관성과 hello 서비스 상태가 실패 후 올바르게 유지 되는지 여부를 테스트 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="0d5c0-125">hello 다른 집합이 실패 (hello 정상적인 실패) 테스트 hello 서비스에 올바르게 tooreplicas 서비스 패브릭에 의해 이동 되 고 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="0d5c0-126">이 hello RunAsync 메서드에서 취소의 처리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="0d5c0-127">hello 서비스는 hello 취소 토큰 중에 설정 하 고, 올바르게 해당 상태를 저장 하 고, hello RunAsync 메서드 종료 toocheck이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="0d5c0-128">테스트 용이성 작업 목록</span><span class="sxs-lookup"><span data-stu-id="0d5c0-128">Testability actions list</span></span>
| <span data-ttu-id="0d5c0-129">작업</span><span class="sxs-lookup"><span data-stu-id="0d5c0-129">Action</span></span> | <span data-ttu-id="0d5c0-130">설명</span><span class="sxs-lookup"><span data-stu-id="0d5c0-130">Description</span></span> | <span data-ttu-id="0d5c0-131">관리 API</span><span class="sxs-lookup"><span data-stu-id="0d5c0-131">Managed API</span></span> | <span data-ttu-id="0d5c0-132">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="0d5c0-132">PowerShell cmdlet</span></span> | <span data-ttu-id="0d5c0-133">정상/비정상 오류</span><span class="sxs-lookup"><span data-stu-id="0d5c0-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0d5c0-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="0d5c0-134">CleanTestState</span></span> |<span data-ttu-id="0d5c0-135">Hello 테스트 드라이버의 잘못 된 시스템 종료 시 hello 클러스터에서 모든 hello 테스트 상태를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="0d5c0-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-136">CleanTestStateAsync</span></span> |<span data-ttu-id="0d5c0-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="0d5c0-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="0d5c0-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0d5c0-138">Not applicable</span></span> |
| <span data-ttu-id="0d5c0-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="0d5c0-139">InvokeDataLoss</span></span> |<span data-ttu-id="0d5c0-140">서비스 파티션으로 데이터 손실을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="0d5c0-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="0d5c0-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="0d5c0-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="0d5c0-143">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-143">Graceful</span></span> |
| <span data-ttu-id="0d5c0-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="0d5c0-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="0d5c0-145">지정된 상태 저장 서비스 파티션을 쿼럼 손실에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="0d5c0-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="0d5c0-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="0d5c0-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="0d5c0-148">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-148">Graceful</span></span> |
| <span data-ttu-id="0d5c0-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="0d5c0-149">Move Primary</span></span> |<span data-ttu-id="0d5c0-150">이동 hello toohello 지정한 클러스터 노드 상태 저장 서비스의 주 복제본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="0d5c0-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-151">MovePrimaryAsync</span></span> |<span data-ttu-id="0d5c0-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="0d5c0-153">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-153">Graceful</span></span> |
| <span data-ttu-id="0d5c0-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="0d5c0-154">Move Secondary</span></span> |<span data-ttu-id="0d5c0-155">상태 저장 서비스 tooa 다른 클러스터 노드에의 hello 현재 보조 복제본으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="0d5c0-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="0d5c0-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="0d5c0-158">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-158">Graceful</span></span> |
| <span data-ttu-id="0d5c0-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-159">RemoveReplica</span></span> |<span data-ttu-id="0d5c0-160">클러스터에서 복제본을 제거하여 복제 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="0d5c0-161">이렇게 하면 hello 복제본 및 toorole 전환 되 'None', hello 클러스터에서 모든 해당 상태를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="0d5c0-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="0d5c0-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="0d5c0-164">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-164">Graceful</span></span> |
| <span data-ttu-id="0d5c0-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="0d5c0-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="0d5c0-166">클러스터의 노드에 배포된 코드 패키지를 다시 시작하여 코드 패키지 프로세스 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="0d5c0-167">해당 프로세스에 호스팅되는 모든 hello 사용자 서비스 복제본 다시 시작 하는 hello 코드 패키지 프로세스를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="0d5c0-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="0d5c0-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="0d5c0-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="0d5c0-170">비정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-170">Ungraceful</span></span> |
| <span data-ttu-id="0d5c0-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-171">RestartNode</span></span> |<span data-ttu-id="0d5c0-172">노드를 다시 시작하여 서비스 패브릭 클러스터 노드 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="0d5c0-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-173">RestartNodeAsync</span></span> |<span data-ttu-id="0d5c0-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="0d5c0-175">비정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-175">Ungraceful</span></span> |
| <span data-ttu-id="0d5c0-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="0d5c0-176">RestartPartition</span></span> |<span data-ttu-id="0d5c0-177">파티션의 일부 또는 모든 복제본을 다시 시작하여 데이터 센터 블랙아웃 또는 클러스터 블랙아웃 시나리오를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="0d5c0-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-178">RestartPartitionAsync</span></span> |<span data-ttu-id="0d5c0-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="0d5c0-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="0d5c0-180">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-180">Graceful</span></span> |
| <span data-ttu-id="0d5c0-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-181">RestartReplica</span></span> |<span data-ttu-id="0d5c0-182">클러스터에서 영구 복제본을 다시 시작, hello 복제본 닫은 후이 복제본 오류를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="0d5c0-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-183">RestartReplicaAsync</span></span> |<span data-ttu-id="0d5c0-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="0d5c0-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="0d5c0-185">정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-185">Graceful</span></span> |
| <span data-ttu-id="0d5c0-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-186">StartNode</span></span> |<span data-ttu-id="0d5c0-187">클러스터에서 이미 중지된 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="0d5c0-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-188">StartNodeAsync</span></span> |<span data-ttu-id="0d5c0-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="0d5c0-190">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0d5c0-190">Not applicable</span></span> |
| <span data-ttu-id="0d5c0-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-191">StopNode</span></span> |<span data-ttu-id="0d5c0-192">클러스터의 노드를 중지하여 노드 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="0d5c0-193">hello 노드 StartNode를 호출할 때까지 아래로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="0d5c0-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-194">StopNodeAsync</span></span> |<span data-ttu-id="0d5c0-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="0d5c0-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="0d5c0-196">비정상</span><span class="sxs-lookup"><span data-stu-id="0d5c0-196">Ungraceful</span></span> |
| <span data-ttu-id="0d5c0-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="0d5c0-197">ValidateApplication</span></span> |<span data-ttu-id="0d5c0-198">Hello 가용성 및 hello 시스템에 일부 오류를 발생 시켜 후 일반적으로 응용 프로그램 내에서 모든 서비스 패브릭 서비스의 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="0d5c0-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="0d5c0-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="0d5c0-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="0d5c0-201">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0d5c0-201">Not applicable</span></span> |
| <span data-ttu-id="0d5c0-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="0d5c0-202">ValidateService</span></span> |<span data-ttu-id="0d5c0-203">일반적으로 hello 시스템에 일부 오류를 발생 시켜 후 hello 가용성 및 서비스 패브릭 서비스의 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="0d5c0-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="0d5c0-204">ValidateServiceAsync</span></span> |<span data-ttu-id="0d5c0-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="0d5c0-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="0d5c0-206">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0d5c0-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="0d5c0-207">PowerShell을 사용하여 테스트 용이성 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="0d5c0-208">이 자습서에서는 어떻게 toorun PowerShell을 사용 하 여 테스트 용이성 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="0d5c0-209">에 대해 설명 합니다 방법을 toorun 로컬 (1-상자) 클러스터 또는 Azure 클러스터에 대해 테스트 용이성 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="0d5c0-210">Microsoft.Fabric.Powershell.dll-hello 서비스 패브릭 PowerShell 모듈-자동으로 설치 됩니다 hello Microsoft 서비스 패브릭 MSI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="0d5c0-211">hello 모듈은 PowerShell 프롬프트를 열 때 자동으로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="0d5c0-212">자습서 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="0d5c0-212">Tutorial segments:</span></span>

* [<span data-ttu-id="0d5c0-213">one-box 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="0d5c0-214">Azure 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="0d5c0-215">one-box 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="0d5c0-216">로컬 클러스터에 대 한 테스트 용이성 동작 toorun toohello 클러스터와 관리자 모드에서 열린 hello PowerShell 프롬프트에 먼저 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="0d5c0-217">Hello에 알아보겠습니다 **다시 시작 ServiceFabricNode** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="0d5c0-218">작업을 여기 hello **ServiceFabricNode 다시 시작** "Node1" 이라는 노드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="0d5c0-219">hello 완성 모드 하지 hello 노드 다시 시작 작업 실제로 성공 했는지 여부를 확인 해야 것을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="0d5c0-220">"확인"으로 hello 완성 모드를 지정 하면 tooverify 실제로 hello를 다시 시작 동작의 성공 여부.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="0d5c0-221">Hello 노드 이름을 사용 하 여를 직접 지정 하지 않고 지정할 수 있습니다는 파티션 키와 hello 종류의 복제본을 통해 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="0d5c0-222">**다시 시작 ServiceFabricNode** 서비스 패브릭 노드 클러스터에서 사용 되는 toorestart 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="0d5c0-223">모든 hello 시스템 서비스 및 사용자 서비스에서 호스팅되는 복제본 해당 노드는 다시 시작 하는 hello Fabric.exe 프로세스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="0d5c0-224">이 API tootest를 사용 하 여 서비스 hello 장애 복구 경로 따라 버그를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="0d5c0-225">Hello 클러스터의 노드 오류를 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="0d5c0-226">hello 다음 스크린샷은 hello **다시 시작 ServiceFabricNode** 테스트 용이성 명령 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="0d5c0-227">먼저의 hello 출력 hello **Get ServiceFabricNode** 해당 hello 로컬 클러스터에는 5 개의 노드가 있는 (hello 서비스 패브릭 PowerShell 모듈의 cmdlet)를 보여 줍니다: Node.1 tooNode.5 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="0d5c0-228">Hello 테스트 용이성 동작 (cmdlet) 후 **다시 시작 ServiceFabricNode** hello 노드에서 실행 Node.4 명명 된, 보면 해당 hello 노드 가동 시간을 다시 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="0d5c0-229">Azure 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="0d5c0-230">Azure 클러스터에 대해 테스트 용이성 작업 (PowerShell 사용)에서 실행 하는 것은 로컬 클러스터에 대해 비슷한 toorunning hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="0d5c0-231">hello 차이점은 연결 toohello 로컬 클러스터 대신 hello 동작을 실행 하기 전에 필요한 tooconnect toohello Azure 먼저 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="0d5c0-232">C&#35;을 사용하여 테스트 용이성 작업 실행</span><span class="sxs-lookup"><span data-stu-id="0d5c0-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="0d5c0-233">C#을 사용 하 여 테스트 용이성 작업 toorun 먼저 tooconnect toohello 클러스터 FabricClient를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="0d5c0-234">다음 hello 필요한 매개 변수 toorun hello 동작을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="0d5c0-235">다른 매개 변수를 사용할 수 있습니다 toorun hello 동일한 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="0d5c0-236">Hello 클러스터의 hello hello 노드 정보 (노드 이름과 노드 인스턴스 ID)을 사용 하 여 한 가지 방법은 toorun RestartServiceFabricNode 동작을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="0d5c0-237">매개 변수 설명:</span><span class="sxs-lookup"><span data-stu-id="0d5c0-237">Parameter explanation:</span></span>

* <span data-ttu-id="0d5c0-238">**CompleteMode** 지정 hello 모드를 사용 하는 hello 다시 시작 동작 실제로 성공 했는지 여부를 확인 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="0d5c0-239">"확인"으로 hello 완성 모드를 지정 하면 tooverify 실제로 hello를 다시 시작 동작의 성공 여부.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="0d5c0-240">**OperationTimeout** TimeoutException 예외는 throw 되기 전에 집합 hello 작업 toofinish hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="0d5c0-241">**CancellationToken** 취소는 보류 중인 호출 toobe 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="0d5c0-242">Hello 노드 이름을 사용 하 여를 직접 지정 하지 않고 복제 데이터베이스의 파티션 키와 hello 종류를 통해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="0d5c0-243">자세한 내용은 [PartitionSelector 및 ReplicaSelector](#partition_replica_selector)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="0d5c0-244">PartitionSelector 및 ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="0d5c0-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="0d5c0-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="0d5c0-245">PartitionSelector</span></span>
<span data-ttu-id="0d5c0-246">PartitionSelector 테스트 가능성에 노출 하는 도우미 이며가 사용 되는 tooselect 특정 분할 작업을 어떤 tooperform hello 테스트 용이성 동작 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="0d5c0-247">Hello 파티션 ID가 미리 알려진 경우 사용 되는 특정 파티션에 tooselect 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="0d5c0-248">또는 hello 파티션 키를 제공할 수 있습니다를 hello 작업 hello 파티션 ID를 내부적으로 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="0d5c0-249">임의의 파티션을 선택한 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="0d5c0-250">toouse이이 도우미 hello PartitionSelector 개체를 만들고 hello Select * 방법 중 하나를 사용 하 여 hello 파티션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="0d5c0-251">Hello PartitionSelector 개체 toohello에서 필요로 하는 API에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="0d5c0-252">없음 옵션을 선택 하는 경우 tooa 임의 파티션을 기본값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="0d5c0-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="0d5c0-253">ReplicaSelector</span></span>
<span data-ttu-id="0d5c0-254">ReplicaSelector 테스트 가능성에 노출 하는 도우미 인데은 사용 되는 toohelp 선택 복제본 어떤 tooperform에 hello 테스트 용이성 동작 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="0d5c0-255">Hello 복제본 ID가 미리 알려진 경우 사용 되는 tooselect 특정 복제본 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="0d5c0-256">또한 주 복제본 또는 임의의 보조 데이터베이스를 선택 하면 hello 옵션도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="0d5c0-257">ReplicaSelector PartitionSelector에서 파생 되, 둘 다 hello tooperform hello 테스트 용이성 작업을 원하는 복제 하 고 hello 파티션이 있으므로 tooselect 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="0d5c0-258">toouse이이 도우미 ReplicaSelector 개체를 만들고 원하는 hello 방식으로 tooselect hello 복제본과 hello 파티션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="0d5c0-259">API에서 필요로 하는 hello에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="0d5c0-260">없음 옵션을 선택 하면 tooa 임의의 복제본 및 임의 파티션 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5c0-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="0d5c0-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d5c0-261">Next steps</span></span>
* [<span data-ttu-id="0d5c0-262">테스트 용이성 시나리오</span><span class="sxs-lookup"><span data-stu-id="0d5c0-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="0d5c0-263">어떻게 tootest 서비스</span><span class="sxs-lookup"><span data-stu-id="0d5c0-263">How tootest your service</span></span>
  * [<span data-ttu-id="0d5c0-264">서비스 작업 중 오류 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="0d5c0-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="0d5c0-265">서비스 대 서비스 통신 오류</span><span class="sxs-lookup"><span data-stu-id="0d5c0-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

