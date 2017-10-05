---
title: "Azure 마이크로 서비스에서 시뮬레이션 실패 | Microsoft 문서"
description: "이 문서에서는 Microsoft Azure 서비스 패브릭에서 발견되는 테스트 용이성 작업에 대해 다룹니다."
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="c681d-103">테스트 용이성 작업</span><span class="sxs-lookup"><span data-stu-id="c681d-103">Testability actions</span></span>
<span data-ttu-id="c681d-104">불안정한 인프라를 시뮬레이트할 수 있도록 Azure 서비스 패브릭에서는 개발자에게 다양한 실제 오류 및 상태 전환을 시뮬레이트할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="c681d-105">이러한 작업을 테스트 용이성 작업이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-105">These are exposed as testability actions.</span></span> <span data-ttu-id="c681d-106">이러한 작업은 특정 오류 주입, 상태 전환 또는 유효성 검사를 발생시키는 저수준 API입니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="c681d-107">이러한 작업을 결합하여 서비스에 대한 포괄적인 테스트 시나리오를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="c681d-108">서비스 패브릭은 이러한 작업으로 구성된 몇 가지 일반 테스트 시나리오를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="c681d-109">이러한 기본 제공 시나리오는 일반 상태 전환 및 장애 사례를 테스트하기 위해 신중하게 선택된 시나리오이므로 적극적으로 활용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="c681d-110">그러나 기본 제공 시나리오에 포함되지 않거나 사용자 지정 응용 프로그램에 맞게 조정된 범위를 추가하려는 경우 작업을 사용하여 사용자 지정 테스트 시나리오를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="c681d-111">C#으로 구현한 작업은 System.Fabric.dll 어셈블리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="c681d-112">시스템 패브릭 PowerShell 모듈은 Microsoft.ServiceFabric.Powershell.dll 어셈블리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="c681d-113">런타임 설치의 일부로 간편한 사용을 위해 ServiceFabric PowerShell 모듈이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="c681d-114">정상적인 오류 작업과 비정상적인 오류 작업 비교</span><span class="sxs-lookup"><span data-stu-id="c681d-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="c681d-115">테스트 용이성 작업은 두 주요 버킷으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="c681d-116">비정상적 오류: 이러한 오류는 컴퓨터 재시작, 프로세스 충돌 같은 실패를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="c681d-117">이러한 실패의 경우 프로세스의 실행 컨텍스트가 갑자기 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="c681d-118">즉, 응용 프로그램을 다시 시작하기 전에 상태 정리를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="c681d-119">정상적인 오류: 이러한 오류는 부하 분산에 의해 트리거되는 복제본 이동 또는 삭제 등의 정상적인 작업을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="c681d-120">이러한 경우에는 서비스에서 종료에 대한 알림을 가져와서 상태 정리 후 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="c681d-121">다양한 정상 및 비정상 오류를 유도하면서 서비스 및 비즈니스 작업을 실행하면 보다 완벽하게 품질을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="c681d-122">비정상적 오류의 경우 워크플로 도중에 서비스 프로세스가 갑자기 종료되는 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="c681d-123">이 시나리오는 Service Fabric에서 서비스 복제본을 복원할 때 복구 경로를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="c681d-124">데이터 일관성을 테스트하고 실패 후 서비스 상태가 올바르게 유지되는지 테스트하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="c681d-125">다른 실패 집합(정상적인 실패)은 서비스 패브릭에 의해 이동되는 복제본에 대해 서비스가 올바르게 반응하는지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="c681d-126">이 테스트는 RunAsync 메서드의 취소 처리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="c681d-127">서비스에서 설정되는 취소 토큰을 확인하고 상태를 올바르게 저장한 후 RunAsync 메서드를 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="c681d-128">테스트 용이성 작업 목록</span><span class="sxs-lookup"><span data-stu-id="c681d-128">Testability actions list</span></span>
| <span data-ttu-id="c681d-129">작업</span><span class="sxs-lookup"><span data-stu-id="c681d-129">Action</span></span> | <span data-ttu-id="c681d-130">설명</span><span class="sxs-lookup"><span data-stu-id="c681d-130">Description</span></span> | <span data-ttu-id="c681d-131">관리 API</span><span class="sxs-lookup"><span data-stu-id="c681d-131">Managed API</span></span> | <span data-ttu-id="c681d-132">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="c681d-132">PowerShell cmdlet</span></span> | <span data-ttu-id="c681d-133">정상/비정상 오류</span><span class="sxs-lookup"><span data-stu-id="c681d-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c681d-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="c681d-134">CleanTestState</span></span> |<span data-ttu-id="c681d-135">테스트 드라이버가 비정상적으로 종료될 경우 클러스터에서 모든 테스트 상태를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="c681d-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-136">CleanTestStateAsync</span></span> |<span data-ttu-id="c681d-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="c681d-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="c681d-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c681d-138">Not applicable</span></span> |
| <span data-ttu-id="c681d-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="c681d-139">InvokeDataLoss</span></span> |<span data-ttu-id="c681d-140">서비스 파티션으로 데이터 손실을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="c681d-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="c681d-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="c681d-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="c681d-143">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-143">Graceful</span></span> |
| <span data-ttu-id="c681d-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c681d-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="c681d-145">지정된 상태 저장 서비스 파티션을 쿼럼 손실에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="c681d-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="c681d-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c681d-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="c681d-148">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-148">Graceful</span></span> |
| <span data-ttu-id="c681d-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="c681d-149">Move Primary</span></span> |<span data-ttu-id="c681d-150">상태 저장 서비스의 지정된 주 복제본을 지정된 클러스터 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="c681d-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-151">MovePrimaryAsync</span></span> |<span data-ttu-id="c681d-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="c681d-153">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-153">Graceful</span></span> |
| <span data-ttu-id="c681d-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="c681d-154">Move Secondary</span></span> |<span data-ttu-id="c681d-155">상태 저장 서비스의 현재 보조 복제본을 다른 클러스터 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="c681d-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="c681d-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="c681d-158">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-158">Graceful</span></span> |
| <span data-ttu-id="c681d-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-159">RemoveReplica</span></span> |<span data-ttu-id="c681d-160">클러스터에서 복제본을 제거하여 복제 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="c681d-161">그러면 복제본이 닫히고 역할 '없음'으로 전환되어 클러스터에서 해당 복제본의 모든 상태가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="c681d-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="c681d-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="c681d-164">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-164">Graceful</span></span> |
| <span data-ttu-id="c681d-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="c681d-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="c681d-166">클러스터의 노드에 배포된 코드 패키지를 다시 시작하여 코드 패키지 프로세스 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="c681d-167">그러면 코드 패키지 프로세스가 취소되고 해당 프로세스에서 호스팅되는 모든 사용자 서비스 복제본이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="c681d-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="c681d-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="c681d-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="c681d-170">비정상</span><span class="sxs-lookup"><span data-stu-id="c681d-170">Ungraceful</span></span> |
| <span data-ttu-id="c681d-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="c681d-171">RestartNode</span></span> |<span data-ttu-id="c681d-172">노드를 다시 시작하여 서비스 패브릭 클러스터 노드 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="c681d-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-173">RestartNodeAsync</span></span> |<span data-ttu-id="c681d-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c681d-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="c681d-175">비정상</span><span class="sxs-lookup"><span data-stu-id="c681d-175">Ungraceful</span></span> |
| <span data-ttu-id="c681d-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="c681d-176">RestartPartition</span></span> |<span data-ttu-id="c681d-177">파티션의 일부 또는 모든 복제본을 다시 시작하여 데이터 센터 블랙아웃 또는 클러스터 블랙아웃 시나리오를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="c681d-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-178">RestartPartitionAsync</span></span> |<span data-ttu-id="c681d-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="c681d-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="c681d-180">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-180">Graceful</span></span> |
| <span data-ttu-id="c681d-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-181">RestartReplica</span></span> |<span data-ttu-id="c681d-182">클러스터에 보관된 복제본을 다시 시작하고, 복제본을 닫은 후 다시 열어서 복제본 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="c681d-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-183">RestartReplicaAsync</span></span> |<span data-ttu-id="c681d-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="c681d-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="c681d-185">정상</span><span class="sxs-lookup"><span data-stu-id="c681d-185">Graceful</span></span> |
| <span data-ttu-id="c681d-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="c681d-186">StartNode</span></span> |<span data-ttu-id="c681d-187">클러스터에서 이미 중지된 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="c681d-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-188">StartNodeAsync</span></span> |<span data-ttu-id="c681d-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c681d-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="c681d-190">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c681d-190">Not applicable</span></span> |
| <span data-ttu-id="c681d-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="c681d-191">StopNode</span></span> |<span data-ttu-id="c681d-192">클러스터의 노드를 중지하여 노드 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="c681d-193">StartNode가 호출될 때까지 노드가 계속 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="c681d-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-194">StopNodeAsync</span></span> |<span data-ttu-id="c681d-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c681d-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="c681d-196">비정상</span><span class="sxs-lookup"><span data-stu-id="c681d-196">Ungraceful</span></span> |
| <span data-ttu-id="c681d-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="c681d-197">ValidateApplication</span></span> |<span data-ttu-id="c681d-198">일반적으로 시스템에 일부 오류를 유도한 후 응용 프로그램 내의 모든 서비스 패브릭 서비스의 가용성 및 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="c681d-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="c681d-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="c681d-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="c681d-201">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c681d-201">Not applicable</span></span> |
| <span data-ttu-id="c681d-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="c681d-202">ValidateService</span></span> |<span data-ttu-id="c681d-203">일반적으로 시스템에 일부 오류를 유도한 후 서비스 패브릭 서비스의 가용성 및 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="c681d-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="c681d-204">ValidateServiceAsync</span></span> |<span data-ttu-id="c681d-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="c681d-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="c681d-206">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c681d-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="c681d-207">PowerShell을 사용하여 테스트 용이성 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="c681d-208">이 자습서에서는 PowerShell을 사용하여 테스트 용이성 작업을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="c681d-209">로컬(one-box) 클러스터 또는 Azure 클러스터에 대해 테스트 용이성 작업을 실행하는 방법을 배울 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="c681d-210">Microsoft.Fabric.Powershell.dll(서비스 패브릭PowerShell 모듈)은 Microsoft 서비스 패브릭 MSI를 설치할 때 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="c681d-211">PowerShell 프롬프트를 열면 이 모듈이 자동으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="c681d-212">자습서 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="c681d-212">Tutorial segments:</span></span>

* [<span data-ttu-id="c681d-213">one-box 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="c681d-214">Azure 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="c681d-215">one-box 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="c681d-216">로컬 클러스터에 대해 테스트 용이성 작업을 실행하려면 먼저 클러스터에 연결하고 관리자 모드에서 PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="c681d-217">**Restart-ServiceFabricNode** 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="c681d-218">"Node1"이라는 노드에서 **Restart-ServiceFabricNode** 작업이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="c681d-219">완료 모드는 다시 시작 노드 작업이 실제로 성공했는지 여부를 확인하지 말라고 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="c681d-220">완료 모드를 "Verify"로 지정하면 다시 시작 작업이 실제로 성공했는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="c681d-221">노드 이름을 사용하여 직접 지정하는 대신 다음과 같이 파티션 키와 복제본의 종류를 통해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="c681d-222">**Restart-ServiceFabricNode**를 사용하여 클러스터의 Service Fabric 노드를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="c681d-223">이 방법을 사용하면 Fabric.exe 프로세스가 중지됩니다. 이 프로세스는 해당 노드에 호스팅되는 모든 시스템 서비스 및 사용자 서비스 복제본을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="c681d-224">이 API를 사용하여 서비스를 테스트하면 장애 조치(failover) 복구 경로를 따라 버그를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="c681d-225">이는 클러스터의 노드 오류를 시뮬레이션하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="c681d-226">다음 스크린샷은 동작 중인 **Restart-ServiceFabricNode** 테스트 용이성 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="c681d-227">첫 번째 **Get-ServiceFabricNode** (서비스 패브릭 PowerShell 모듈의 cmdlet)의 출력은 로컬 클러스터에 다섯 개의 노드(Node.1~Node.5)가 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="c681d-228">Node.4 노드에서 테스트 용이성 작업(cmdlet) **Restart-ServiceFabricNode** 를 실행하면 노드의 가동 시간이 다시 설정된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="c681d-229">Azure 클러스터에 대해 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="c681d-230">PowerShell을 사용하여 Azure 클러스터에 대해 테스트 용이성 작업을 실행하는 방법은 로컬 클러스터에 대해 작업을 실행하는 방법과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="c681d-231">작업을 실행하려면 로컬 클러스터 대신 Azure 클러스터에 먼저 연결해야 한다는 점만 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="c681d-232">C&#35;을 사용하여 테스트 용이성 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c681d-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="c681d-233">C#을 사용하여 테스트 용이성 작업을 실행하려면 먼저 FabricClient를 사용하여 클러스터에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="c681d-234">그런 다음 작업 실행에 필요한 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="c681d-235">다른 매개 변수를 사용하여 같은 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="c681d-236">RestartServiceFabricNode 작업을 살펴보면 노드 정보(노드 이름 및 노드 인스턴스 ID)를 사용하여 노드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="c681d-237">매개 변수 설명:</span><span class="sxs-lookup"><span data-stu-id="c681d-237">Parameter explanation:</span></span>

* <span data-ttu-id="c681d-238">**CompleteMode** 는 모드에서 다시 시작 작업이 실제로 성공했는지 여부를 확인하지 말라고 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="c681d-239">완료 모드를 "Verify"로 지정하면 다시 시작 작업이 실제로 성공했는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="c681d-240">**OperationTimeout** 은 TimeoutException 예외가 throw되기 전에 작업이 완료되어야 하는 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="c681d-241">**CancellationToken** 은 보류 중인 호출을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="c681d-242">노드 이름을 사용하여 직접 지정하는 대신 파티션 키와 복제본의 종류를 통해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="c681d-243">자세한 내용은 [PartitionSelector 및 ReplicaSelector](#partition_replica_selector)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c681d-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="c681d-244">PartitionSelector 및 ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="c681d-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="c681d-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="c681d-245">PartitionSelector</span></span>
<span data-ttu-id="c681d-246">PartitionSelector는 테스트 용이성에 노출되는 도우미이며 테스트 용이성 작업을 수행할 특정 파티션을 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="c681d-247">파티션 ID가 이미 알려져 있는 경우 특정 파티션을 선택하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="c681d-248">또는 파티션 키를 제공하면 작업에서 파티션 ID를 내부적으로 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="c681d-249">또한 임의의 파티션을 선택하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="c681d-250">이 도우미를 사용하려면 PartitionSelector 개체를 만들고 Select* 메서드 중 하나를 사용하여 파티션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="c681d-251">그런 다음 PartitionSelector 개체를 필요로 하는 API에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="c681d-252">옵션을 선택하지 않으면 기본적으로 임의의 파티션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="c681d-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="c681d-253">ReplicaSelector</span></span>
<span data-ttu-id="c681d-254">ReplicaSelector는 테스트 용이성에 노출되는 도우미이며 테스트 용이성 작업을 수행할 특정 복제본을 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="c681d-255">복제본 ID가 이미 알려져 있는 경우 특정 복제본을 선택하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="c681d-256">또한 주 복제본 또는 임의의 보조 복제본을 선택하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="c681d-257">ReplicaSelector는 PartitionSelector에서 파생되므로 테스트 용이성 작업을 수행할 복제본과 파티션을 모두 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="c681d-258">이 도우미를 사용하려면 ReplicaSelector 개체를 만들고 복제본 및 파티션을 선택하는 방법을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="c681d-259">그런 다음 개체를 필요로 하는 API에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="c681d-260">옵션을 선택하지 않으면 기본적으로 임의의 복제본 및 파티션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681d-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="c681d-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c681d-261">Next steps</span></span>
* [<span data-ttu-id="c681d-262">테스트 용이성 시나리오</span><span class="sxs-lookup"><span data-stu-id="c681d-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="c681d-263">서비스를 테스트하는 방법</span><span class="sxs-lookup"><span data-stu-id="c681d-263">How to test your service</span></span>
  * [<span data-ttu-id="c681d-264">서비스 작업 중 오류 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="c681d-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="c681d-265">서비스 대 서비스 통신 오류</span><span class="sxs-lookup"><span data-stu-id="c681d-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

