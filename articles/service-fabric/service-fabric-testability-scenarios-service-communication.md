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
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a><span data-ttu-id="f6c8c-104">서비스 패브릭 테스트 용이성 시나리오: 서비스 통신</span><span class="sxs-lookup"><span data-stu-id="f6c8c-104">Service Fabric testability scenarios: Service communication</span></span>
<span data-ttu-id="f6c8c-105">Azure 서비스 패브릭에서 마이크로 서비스 및 서비스 지향 아키텍처 스타일이 자연스럽게 드러납니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-105">Microservices and service-oriented architectural styles surface naturally in Azure Service Fabric.</span></span> <span data-ttu-id="f6c8c-106">이러한 종류의 분산된 아키텍처에서 마이크로 서비스 구성 요소화 된 응용 프로그램 여러 해야 하는 서비스 tootalk tooeach 다른 일반적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-106">In these types of distributed architectures, componentized microservice applications are typically composed of multiple services that need tootalk tooeach other.</span></span> <span data-ttu-id="f6c8c-107">가장 간단한 경우에 hello 하면 일반적으로 상태 비저장 웹 서비스 및 toocommunicate 해야 하는 상태 저장 데이터 저장소 서비스.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-107">In even hello simplest cases, you generally have at least a stateless web service and a stateful data storage service that need toocommunicate.</span></span>

<span data-ttu-id="f6c8c-108">서비스 간 통신 응용 프로그램의 중요 한 통합 지점이 되므로 각 서비스는 원격 API tooother 서비스를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-108">Service-to-service communication is a critical integration point of an application, because each service exposes a remote API tooother services.</span></span> <span data-ttu-id="f6c8c-109">I/O와 관련된 API 경계 집합을 사용하여 작업하려면 일반적으로 적절한 테스트 및 유효성 검사가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-109">Working with a set of API boundaries that involves I/O generally requires some care, with a good amount of testing and validation.</span></span>

<span data-ttu-id="f6c8c-110">이러한 서비스 경계는 분산된 시스템에 함께 연결 하는 경우 다양 한 고려 사항 toomake 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-110">There are numerous considerations toomake when these service boundaries are wired together in a distributed system:</span></span>

* <span data-ttu-id="f6c8c-111">*전송 프로토콜*.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-111">*Transport protocol*.</span></span> <span data-ttu-id="f6c8c-112">상호 운용성을 높이기 위해 HTTP를 사용할까요 아니면 처리량을 극대화하기 위해 사용자 지정 이진 프로토콜을 사용할까요?</span><span class="sxs-lookup"><span data-stu-id="f6c8c-112">Will you use HTTP for increased interoperability, or a custom binary protocol for maximum throughput?</span></span>
* <span data-ttu-id="f6c8c-113">*오류 처리*.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-113">*Error handling*.</span></span> <span data-ttu-id="f6c8c-114">영구 및 임시 오류는 어떻게 처리되나요?</span><span class="sxs-lookup"><span data-stu-id="f6c8c-114">How will permanent and transient errors be handled?</span></span> <span data-ttu-id="f6c8c-115">서비스가 tooa 다른 노드로 이동 하는 경우 어떻게?</span><span class="sxs-lookup"><span data-stu-id="f6c8c-115">What will happen when a service moves tooa different node?</span></span>
* <span data-ttu-id="f6c8c-116">*제한 시간 및 대기 시간*.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-116">*Timeouts and latency*.</span></span> <span data-ttu-id="f6c8c-117">다중 계층 응용 프로그램에서 각 서비스 계층 처리 하는 방법을 통해 hello 스택과 toohello 사용자 대기 시간?</span><span class="sxs-lookup"><span data-stu-id="f6c8c-117">In multitiered applications, how will each service layer handle latency through hello stack and toohello user?</span></span>

<span data-ttu-id="f6c8c-118">Hello 기본 제공 서비스 통신 구성 요소를 서비스 패브릭에서 제공 하는 중 하나를 사용 하거나 직접 작성에서 응용 프로그램에서 중요 한 tooensuring 복원 력을 서비스 간의 hello 상호 작용을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-118">Whether you use one of hello built-in service communication components provided by Service Fabric or you build your own, testing hello interactions between your services is critical tooensuring resiliency in your application.</span></span>

## <a name="prepare-for-services-toomove"></a><span data-ttu-id="f6c8c-119">서비스 toomove 준비</span><span class="sxs-lookup"><span data-stu-id="f6c8c-119">Prepare for services toomove</span></span>
<span data-ttu-id="f6c8c-120">서비스 인스턴스는 시간이 지남에 따라 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-120">Service instances may move around over time.</span></span> <span data-ttu-id="f6c8c-121">사용자 지정된 최적의 리소스 균형에 대한 부하 메트릭을 사용하여 구성된 경우에 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-121">This is especially true when they are configured with load metrics for custom-tailored optimal resource balancing.</span></span> <span data-ttu-id="f6c8c-122">서비스 패브릭 서비스 인스턴스 toomaximize 가능성 업그레이드, 장애 조치, 수평 및 분산된 시스템 hello 기간 동안 발생 하는 기타 상황 중에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-122">Service Fabric moves your service instances toomaximize their availability even during upgrades, failovers, scale-out, and other situations that occur over hello lifetime of a distributed system.</span></span>

<span data-ttu-id="f6c8c-123">서비스는 hello 클러스터에서 이동, 클라이언트 및 기타 서비스 있어야 준비 toohandle 두 가지 시나리오 tooa 서비스를 설명 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="f6c8c-123">As services move around in hello cluster, your clients and other services should be prepared toohandle two scenarios when they talk tooa service:</span></span>

* <span data-ttu-id="f6c8c-124">hello 서비스 인스턴스 또는 파티션의 복제본 hello tooit 설명이 마지막 시간 이후 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-124">hello service instance or partition replica has moved since hello last time you talked tooit.</span></span> <span data-ttu-id="f6c8c-125">서비스 기간의 정상적인 일부 이며 응용 프로그램의 hello 수명 동안 예상된 toohappen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-125">This is a normal part of a service lifecycle, and it should be expected toohappen during hello lifetime of your application.</span></span>
* <span data-ttu-id="f6c8c-126">hello 서비스 인스턴스 또는 파티션의 복제본이 이동 하는 hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-126">hello service instance or partition replica is in hello process of moving.</span></span> <span data-ttu-id="f6c8c-127">장애 조치 노드 tooanother 하나에서 서비스의 서비스 패브릭에서 매우 빠르게 수행 하지만에 있을 수 있습니다 지연 가용성 느린 toostart 경우 서비스의 hello 통신 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-127">Although failover of a service from one node tooanother occurs very quickly in Service Fabric, there may be a delay in availability if hello communication component of your service is slow toostart.</span></span>

<span data-ttu-id="f6c8c-128">시스템이 원활하게 실행되도록 이러한 시나리오를 정상적으로 처리하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-128">Handling these scenarios gracefully is important for a smooth-running system.</span></span> <span data-ttu-id="f6c8c-129">toodo 따라서 염두에입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-129">toodo so, keep in mind that:</span></span>

* <span data-ttu-id="f6c8c-130">연결 된 toohas 일 수 있는 모든 서비스는 *주소* 를 (예: HTTP 또는 Websocket)에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-130">Every service that can be connected toohas an *address* that it listens on (for example, HTTP or WebSockets).</span></span> <span data-ttu-id="f6c8c-131">서비스 인스턴스 또는 파티션이 이동하면 주소 끝점이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-131">When a service instance or partition moves, its address endpoint changes.</span></span> <span data-ttu-id="f6c8c-132">(다른 IP 주소로 tooa 다른 노드로 이동 합니다.) Hello 기본 제공 통신 구성 요소를 사용 하는 경우 사용자에 대 한 서비스 주소를 확인 하 고 다시 처리 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-132">(It moves tooa different node with a different IP address.) If you're using hello built-in communication components, they will handle re-resolving service addresses for you.</span></span>
* <span data-ttu-id="f6c8c-133">있을 수 있습니다는 임시 해당 수신기를 hello 서비스 인스턴스가 시작 될 때 서비스 대기 시간 증가 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-133">There may be a temporary increase in service latency as hello service instance starts up its listener again.</span></span> <span data-ttu-id="f6c8c-134">이 hello 서비스 인스턴스를 이동한 후 hello 서비스 hello 수신기 열립니다 속도에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-134">This depends on how quickly hello service opens hello listener after hello service instance is moved.</span></span>
* <span data-ttu-id="f6c8c-135">모든 기존 연결은 toobe hello 서비스에 새 노드를 연 후 닫았다가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-135">Any existing connections need toobe closed and reopened after hello service opens on a new node.</span></span> <span data-ttu-id="f6c8c-136">정상적인 노드 종료 또는 다시 시작 하면 기존 연결 toobe 정상적으로 종료.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-136">A graceful node shutdown or restart allows time for existing connections toobe shut down gracefully.</span></span>

### <a name="test-it-move-service-instances"></a><span data-ttu-id="f6c8c-137">테스트: 서비스 인스턴스 이동</span><span class="sxs-lookup"><span data-stu-id="f6c8c-137">Test it: Move service instances</span></span>
<span data-ttu-id="f6c8c-138">서비스 패브릭의 테스트 용이성 도구를 사용 하 여 다양 한 방식에서 테스트 시나리오 tootest에 이러한 상황이 작성할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="f6c8c-138">By using Service Fabric's testability tools, you can author a test scenario tootest these situations in different ways:</span></span>

1. <span data-ttu-id="f6c8c-139">상태 저장 서비스의 주 복제본을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-139">Move a stateful service's primary replica.</span></span>
   
    <span data-ttu-id="f6c8c-140">hello 주 복제본의 상태 저장 서비스의 파티션 이동할 수 있습니다에 대 한 여러 가지 이유로.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-140">hello primary replica of a stateful service partition can be moved for any number of reasons.</span></span> <span data-ttu-id="f6c8c-141">특정 파티션에 toosee 서비스 react toohello 매우 제어 된 방식으로 이동 하는 방법의이 tootarget hello 주 복제본을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-141">Use this tootarget hello primary replica of a specific partition toosee how your services react toohello move in a very controlled manner.</span></span>
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. <span data-ttu-id="f6c8c-142">노드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-142">Stop a node.</span></span>
   
    <span data-ttu-id="f6c8c-143">노드 중지 되 면 hello의 모든 서비스 인스턴스 또는 해당 노드 tooone의에 있던 파티션을 이동 합니다. 서비스 패브릭 hello hello 클러스터의 다른 사용 가능한 노드.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-143">When a node is stopped, Service Fabric moves all of hello service instances or partitions that were on that node tooone of hello other available nodes in hello cluster.</span></span> <span data-ttu-id="f6c8c-144">이 경우 노드는 클러스터에서 손실 toomove가 모든 hello 서비스 인스턴스 및 해당 노드의 복제본이이 tootest를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-144">Use this tootest a situation where a node is lost from your cluster and all of hello service instances and replicas on that node have toomove.</span></span>
   
    <span data-ttu-id="f6c8c-145">Hello PowerShell을 사용 하 여 노드를 중지할 수 있습니다 **중지 ServiceFabricNode** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6c8c-145">You can stop a node by using hello PowerShell **Stop-ServiceFabricNode** cmdlet:</span></span>
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a><span data-ttu-id="f6c8c-146">서비스 가용성 유지 관리</span><span class="sxs-lookup"><span data-stu-id="f6c8c-146">Maintain service availability</span></span>
<span data-ttu-id="f6c8c-147">플랫폼 서비스 패브릭 설계 된 tooprovide 고가용성 서비스의 크기는입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-147">As a platform, Service Fabric is designed tooprovide high availability of your services.</span></span> <span data-ttu-id="f6c8c-148">그러나 극단적인 상황에서 기본 인프라 문제로 인해 서비스 제공이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-148">But in extreme cases, underlying infrastructure problems can still cause unavailability.</span></span> <span data-ttu-id="f6c8c-149">너무는 이러한 시나리오에 대 한 중요 한 tootest입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-149">It is important tootest for these scenarios, too.</span></span>

<span data-ttu-id="f6c8c-150">상태 저장 서비스 가용성을 높이기 위한 쿼럼 기반 시스템 tooreplicate 상태를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-150">Stateful services use a quorum-based system tooreplicate state for high availability.</span></span> <span data-ttu-id="f6c8c-151">이 복제본의 쿼럼 toobe 사용할 수 있는 tooperform 쓰기 작업을 해야 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-151">This means that a quorum of replicas needs toobe available tooperform write operations.</span></span> <span data-ttu-id="f6c8c-152">매우 드물기는 해도 광범위한 하드웨어 오류와 같이 복제본의 쿼럼을 사용할 수 없는 경우가 아주 가끔 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-152">In rare cases, such as a widespread hardware failure, a quorum of replicas may not be available.</span></span> <span data-ttu-id="f6c8c-153">이러한 경우 수 tooperform 쓰기 작업 수 있지만 읽기 작업 수 tooperform 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-153">In these cases, you will not be able tooperform write operations, but you will still be able tooperform read operations.</span></span>

### <a name="test-it-write-operation-unavailability"></a><span data-ttu-id="f6c8c-154">테스트: 쓰기 작업 사용 불가</span><span class="sxs-lookup"><span data-stu-id="f6c8c-154">Test it: Write operation unavailability</span></span>
<span data-ttu-id="f6c8c-155">서비스 패브릭에서 hello 테스트 용이성 도구를 사용해 테스트로 쿼럼 손실을 적용 하는 오류를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-155">By using hello testability tools in Service Fabric, you can inject a fault that induces quorum loss as a test.</span></span> <span data-ttu-id="f6c8c-156">이러한 시나리오는 드물지만이 클라이언트와 상태 저장 서비스에 종속 된 서비스 요청 tooit 쓰기를 만들 수 없습니다 것 toohandle 상황에 준비 되어 있는지 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-156">Although such a scenario is rare, it is important that clients and services that depend on a stateful service are prepared toohandle situations where they cannot make write requests tooit.</span></span> <span data-ttu-id="f6c8c-157">Hello 상태 저장 서비스 자체는이 가능성을 인식 하 고 정상적으로 통신할 수 것 toocallers 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-157">It is also important that hello stateful service itself is aware of this possibility and can gracefully communicate it toocallers.</span></span>

<span data-ttu-id="f6c8c-158">쿼럼 손실 hello PowerShell을 사용 하 여 실행할 수 있습니다 **Invoke ServiceFabricPartitionQuorumLoss** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6c8c-158">You can induce quorum loss by using hello PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:</span></span>

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

<span data-ttu-id="f6c8c-159">이 예제 설정 `QuorumLossMode` 너무`QuorumReplicas` tooinduce 쿼럼 손실 모든 복제를 중단 하지 않고 원하는 tooindicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-159">In this example, we set `QuorumLossMode` too`QuorumReplicas` tooindicate that we want tooinduce quorum loss without taking down all replicas.</span></span> <span data-ttu-id="f6c8c-160">이러한 방식으로 읽기 작업은 여전히 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-160">This way, read operations are still possible.</span></span> <span data-ttu-id="f6c8c-161">전체 파티션을 사용할 수 없으면 시나리오 tootest 너무이 스위치를 설정할 수 있습니다`AllReplicas`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c8c-161">tootest a scenario where an entire partition is unavailable, you can set this switch too`AllReplicas`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6c8c-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6c8c-162">Next steps</span></span>
[<span data-ttu-id="f6c8c-163">테스트 용이성 작업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f6c8c-163">Learn more about testability actions</span></span>](service-fabric-testability-actions.md)

[<span data-ttu-id="f6c8c-164">테스트 용이성 시나리오에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f6c8c-164">Learn more about testability scenarios</span></span>](service-fabric-testability-scenarios.md)

