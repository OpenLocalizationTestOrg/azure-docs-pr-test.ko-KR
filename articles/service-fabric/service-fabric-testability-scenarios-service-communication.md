---
title: "테스트 용이성: 서비스 통신 | Microsoft Docs"
description: "서비스 간 통신은 서비스 패브릭 응용 프로그램의 중요 한 통합점입니다. 이 문서에서는 설계 고려 사항 및 테스트 기술에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c182cc2062ada40029504de5b2b64b021c614ce6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a><span data-ttu-id="42216-104">서비스 패브릭 테스트 용이성 시나리오: 서비스 통신</span><span class="sxs-lookup"><span data-stu-id="42216-104">Service Fabric testability scenarios: Service communication</span></span>
<span data-ttu-id="42216-105">Azure 서비스 패브릭에서 마이크로 서비스 및 서비스 지향 아키텍처 스타일이 자연스럽게 드러납니다.</span><span class="sxs-lookup"><span data-stu-id="42216-105">Microservices and service-oriented architectural styles surface naturally in Azure Service Fabric.</span></span> <span data-ttu-id="42216-106">이러한 유형의 분산 아키텍처에서 구성 요소화된 마이크로 서비스 응용 프로그램은 서로 통신이 필요한 여러 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="42216-106">In these types of distributed architectures, componentized microservice applications are typically composed of multiple services that need to talk to each other.</span></span> <span data-ttu-id="42216-107">가장 간단한 경우에도 일반적으로 상태 비저장 웹 서비스 그리고 통신이 필요한 상태 저장 데이터 저장소 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-107">In even the simplest cases, you generally have at least a stateless web service and a stateful data storage service that need to communicate.</span></span>

<span data-ttu-id="42216-108">각 서비스에서 다른 서비스에 원격 API를 노출하기 때문에 서비스 간 통신은 응용 프로그램의 중요한 통합점입니다.</span><span class="sxs-lookup"><span data-stu-id="42216-108">Service-to-service communication is a critical integration point of an application, because each service exposes a remote API to other services.</span></span> <span data-ttu-id="42216-109">I/O와 관련된 API 경계 집합을 사용하여 작업하려면 일반적으로 적절한 테스트 및 유효성 검사가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-109">Working with a set of API boundaries that involves I/O generally requires some care, with a good amount of testing and validation.</span></span>

<span data-ttu-id="42216-110">분산 시스템에서 이러한 서비스 경계를 연결할 때 여러 가지 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-110">There are numerous considerations to make when these service boundaries are wired together in a distributed system:</span></span>

* <span data-ttu-id="42216-111">*전송 프로토콜*.</span><span class="sxs-lookup"><span data-stu-id="42216-111">*Transport protocol*.</span></span> <span data-ttu-id="42216-112">상호 운용성을 높이기 위해 HTTP를 사용할까요 아니면 처리량을 극대화하기 위해 사용자 지정 이진 프로토콜을 사용할까요?</span><span class="sxs-lookup"><span data-stu-id="42216-112">Will you use HTTP for increased interoperability, or a custom binary protocol for maximum throughput?</span></span>
* <span data-ttu-id="42216-113">*오류 처리*.</span><span class="sxs-lookup"><span data-stu-id="42216-113">*Error handling*.</span></span> <span data-ttu-id="42216-114">영구 및 임시 오류는 어떻게 처리되나요?</span><span class="sxs-lookup"><span data-stu-id="42216-114">How will permanent and transient errors be handled?</span></span> <span data-ttu-id="42216-115">서비스가 다른 노드로 이동하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="42216-115">What will happen when a service moves to a different node?</span></span>
* <span data-ttu-id="42216-116">*제한 시간 및 대기 시간*.</span><span class="sxs-lookup"><span data-stu-id="42216-116">*Timeouts and latency*.</span></span> <span data-ttu-id="42216-117">다중 계층 응용 프로그램에서 각 서비스 계층이 스택을 거쳐 사용자에 도달하는 대기 시간을 어떻게 처리합니까?</span><span class="sxs-lookup"><span data-stu-id="42216-117">In multitiered applications, how will each service layer handle latency through the stack and to the user?</span></span>

<span data-ttu-id="42216-118">서비스 패브릭에서 제공하는 기본 제공 서비스 통신 구성 요소 중 하나를 사용하든지 사용자가 고유의 구성 요소를 만들든지 서비스 간의 상호 작용을 테스트하는 것이 응용 프로그램의 복구 기능을 보장하는 데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-118">Whether you use one of the built-in service communication components provided by Service Fabric or you build your own, testing the interactions between your services is critical to ensuring resiliency in your application.</span></span>

## <a name="prepare-for-services-to-move"></a><span data-ttu-id="42216-119">서비스 이동에 대한 준비</span><span class="sxs-lookup"><span data-stu-id="42216-119">Prepare for services to move</span></span>
<span data-ttu-id="42216-120">서비스 인스턴스는 시간이 지남에 따라 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-120">Service instances may move around over time.</span></span> <span data-ttu-id="42216-121">사용자 지정된 최적의 리소스 균형에 대한 부하 메트릭을 사용하여 구성된 경우에 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-121">This is especially true when they are configured with load metrics for custom-tailored optimal resource balancing.</span></span> <span data-ttu-id="42216-122">분산 시스템의 전체 수명 주기에서 발생하는 업그레이드, 장애 조치(failover), 수평 확장 및 기타 상황 동안 가용성을 극대화하기 위해 서비스 패브릭이 서비스 인스턴스를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="42216-122">Service Fabric moves your service instances to maximize their availability even during upgrades, failovers, scale-out, and other situations that occur over the lifetime of a distributed system.</span></span>

<span data-ttu-id="42216-123">클러스터에서 서비스가 이동하는 경우에 서비스와 통신할 때 클라이언트 및 다른 서비스가 두 가지 시나리오를 처리할 수 있도록 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-123">As services move around in the cluster, your clients and other services should be prepared to handle two scenarios when they talk to a service:</span></span>

* <span data-ttu-id="42216-124">마지막으로 통신한 이후에 서비스 인스턴스 또는 파티션 복제본이 이동했습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-124">The service instance or partition replica has moved since the last time you talked to it.</span></span> <span data-ttu-id="42216-125">이는 서비스 수명 주기에서 일반적인 부분이므로 응용 프로그램의 수명 주기 동안 발생할 것으로 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-125">This is a normal part of a service lifecycle, and it should be expected to happen during the lifetime of your application.</span></span>
* <span data-ttu-id="42216-126">서비스 인스턴스 또는 파티션 복제본이 이동하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="42216-126">The service instance or partition replica is in the process of moving.</span></span> <span data-ttu-id="42216-127">서비스 패브릭에서는 한 노드에서 다른 노드로의 서비스 장애 조치(failover)가 매우 빠르게 발생하지만 서비스 통신 구성 요소가 느리게 시작되면 가용성이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-127">Although failover of a service from one node to another occurs very quickly in Service Fabric, there may be a delay in availability if the communication component of your service is slow to start.</span></span>

<span data-ttu-id="42216-128">시스템이 원활하게 실행되도록 이러한 시나리오를 정상적으로 처리하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-128">Handling these scenarios gracefully is important for a smooth-running system.</span></span> <span data-ttu-id="42216-129">이렇게 하려면 다음에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-129">To do so, keep in mind that:</span></span>

* <span data-ttu-id="42216-130">연결 가능한 모든 서비스에는 수신하는 *주소*가 있습니다(예: HTTP 또는 WebSockets).</span><span class="sxs-lookup"><span data-stu-id="42216-130">Every service that can be connected to has an *address* that it listens on (for example, HTTP or WebSockets).</span></span> <span data-ttu-id="42216-131">서비스 인스턴스 또는 파티션이 이동하면 주소 끝점이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="42216-131">When a service instance or partition moves, its address endpoint changes.</span></span> <span data-ttu-id="42216-132">(다른 IP 주소로 다른 노드에 이동합니다.) 기본 제공 통신 구성 요소를 사용하는 경우 사용자를 대신하여 구성 요소에서 다시 해결 서비스 주소를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-132">(It moves to a different node with a different IP address.) If you're using the built-in communication components, they will handle re-resolving service addresses for you.</span></span>
* <span data-ttu-id="42216-133">서비스 인스턴스에서 수신기를 다시 시작하기 때문에 서비스 대기 시간이 일시적으로 늘어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-133">There may be a temporary increase in service latency as the service instance starts up its listener again.</span></span> <span data-ttu-id="42216-134">서비스 인스턴스를 이동한 후에 서비스가 수신기를 여는 속도에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="42216-134">This depends on how quickly the service opens the listener after the service instance is moved.</span></span>
* <span data-ttu-id="42216-135">새 노드에서 서비스가 열린 후에 기존 연결을 닫았다가 다시 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-135">Any existing connections need to be closed and reopened after the service opens on a new node.</span></span> <span data-ttu-id="42216-136">정상적인 노드 종료 또는 재시작의 경우 기존 연결이 정상적으로 종료될 때까지 시간이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="42216-136">A graceful node shutdown or restart allows time for existing connections to be shut down gracefully.</span></span>

### <a name="test-it-move-service-instances"></a><span data-ttu-id="42216-137">테스트: 서비스 인스턴스 이동</span><span class="sxs-lookup"><span data-stu-id="42216-137">Test it: Move service instances</span></span>
<span data-ttu-id="42216-138">서비스 패브릭의 테스트 용이성 도구를 사용하여 이러한 상황을 다양한 방법으로 테스트하는 테스트 시나리오를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-138">By using Service Fabric's testability tools, you can author a test scenario to test these situations in different ways:</span></span>

1. <span data-ttu-id="42216-139">상태 저장 서비스의 주 복제본을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-139">Move a stateful service's primary replica.</span></span>
   
    <span data-ttu-id="42216-140">여러 가지 이유로 상태 저장 서비스 파티션의 주 복제본을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-140">The primary replica of a stateful service partition can be moved for any number of reasons.</span></span> <span data-ttu-id="42216-141">특정 파티션의 주 복제본을 대상으로 이 방법을 사용하여 철저하게 제어된 방식으로 서비스가 이동에 어떻게 대응하는지 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-141">Use this to target the primary replica of a specific partition to see how your services react to the move in a very controlled manner.</span></span>
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. <span data-ttu-id="42216-142">노드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-142">Stop a node.</span></span>
   
    <span data-ttu-id="42216-143">노드가 중지되면 서비스 패브릭에서는 해당 노드에 있는 모든 서비스 인스턴스 또는 파티션을 클러스터의 사용 가능한 다른 노드 중 하나로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-143">When a node is stopped, Service Fabric moves all of the service instances or partitions that were on that node to one of the other available nodes in the cluster.</span></span> <span data-ttu-id="42216-144">클러스터의 노드가 손실되어 해당 노드의 모든 서비스 인스턴스 및 복제본을 이동해야 하는 상황을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-144">Use this to test a situation where a node is lost from your cluster and all of the service instances and replicas on that node have to move.</span></span>
   
    <span data-ttu-id="42216-145">PowerShell **Stop-ServiceFabricNode** cmdlet을 사용하여 노드를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-145">You can stop a node by using the PowerShell **Stop-ServiceFabricNode** cmdlet:</span></span>
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a><span data-ttu-id="42216-146">서비스 가용성 유지 관리</span><span class="sxs-lookup"><span data-stu-id="42216-146">Maintain service availability</span></span>
<span data-ttu-id="42216-147">플랫폼인 서비스 패브릭은 서비스 고가용성을 제공하도록 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="42216-147">As a platform, Service Fabric is designed to provide high availability of your services.</span></span> <span data-ttu-id="42216-148">그러나 극단적인 상황에서 기본 인프라 문제로 인해 서비스 제공이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-148">But in extreme cases, underlying infrastructure problems can still cause unavailability.</span></span> <span data-ttu-id="42216-149">이러한 시나리오를 테스트하는 것도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-149">It is important to test for these scenarios, too.</span></span>

<span data-ttu-id="42216-150">상태 저장 서비스에서는 쿼럼 기반 시스템을 사용하여 고가용성에 대한 상태를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-150">Stateful services use a quorum-based system to replicate state for high availability.</span></span> <span data-ttu-id="42216-151">즉, 쓰기 작업을 수행하려면 복제본의 쿼럼을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-151">This means that a quorum of replicas needs to be available to perform write operations.</span></span> <span data-ttu-id="42216-152">매우 드물기는 해도 광범위한 하드웨어 오류와 같이 복제본의 쿼럼을 사용할 수 없는 경우가 아주 가끔 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-152">In rare cases, such as a widespread hardware failure, a quorum of replicas may not be available.</span></span> <span data-ttu-id="42216-153">이러한 경우에 쓰기 작업을 수행할 수 없지만 읽기 작업은 계속 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-153">In these cases, you will not be able to perform write operations, but you will still be able to perform read operations.</span></span>

### <a name="test-it-write-operation-unavailability"></a><span data-ttu-id="42216-154">테스트: 쓰기 작업 사용 불가</span><span class="sxs-lookup"><span data-stu-id="42216-154">Test it: Write operation unavailability</span></span>
<span data-ttu-id="42216-155">서비스 패브릭의 테스트 용이성 도구를 사용하여 쿼럼 손실을 테스트로 유도하는 오류를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-155">By using the testability tools in Service Fabric, you can inject a fault that induces quorum loss as a test.</span></span> <span data-ttu-id="42216-156">이러한 시나리오가 드물지만 상태 저장 서비스를 사용하는 클라이언트 및 서비스에서 이에 대한 쓰기 요청을 만들 수 없는 상황을 처리할 수 있도록 준비하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-156">Although such a scenario is rare, it is important that clients and services that depend on a stateful service are prepared to handle situations where they cannot make write requests to it.</span></span> <span data-ttu-id="42216-157">또한 상태 저장 서비스 자체에서 이 가능성을 인식하고 호출자에게 정상적으로 전달하는 것도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-157">It is also important that the stateful service itself is aware of this possibility and can gracefully communicate it to callers.</span></span>

<span data-ttu-id="42216-158">PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet을 사용하여 쿼럼 손실을 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42216-158">You can induce quorum loss by using the PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:</span></span>

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

<span data-ttu-id="42216-159">이 예제에서는 모든 복제본을 중지하지 않고 쿼럼 손실을 포함하도록 `QuorumLossMode`를 `QuorumReplicas`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-159">In this example, we set `QuorumLossMode` to `QuorumReplicas` to indicate that we want to induce quorum loss without taking down all replicas.</span></span> <span data-ttu-id="42216-160">이러한 방식으로 읽기 작업은 여전히 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-160">This way, read operations are still possible.</span></span> <span data-ttu-id="42216-161">전체 파티션을 사용할 수 없는 시나리오를 테스트하려면 이 스위치를 `AllReplicas`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42216-161">To test a scenario where an entire partition is unavailable, you can set this switch to `AllReplicas`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42216-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42216-162">Next steps</span></span>
[<span data-ttu-id="42216-163">테스트 용이성 작업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="42216-163">Learn more about testability actions</span></span>](service-fabric-testability-actions.md)

[<span data-ttu-id="42216-164">테스트 용이성 시나리오에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="42216-164">Learn more about testability scenarios</span></span>](service-fabric-testability-scenarios.md)

