---
title: "Reliable Services 고급 사용법 | Microsoft Docs"
description: "서비스에 유연성을 더해 주는 서비스 패브릭의 Reliable Services 고급 사용법에 대해 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: a87924faaf5c6c43716b06b6d70ab5100c61f097
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-usage-of-the-reliable-services-programming-model"></a><span data-ttu-id="23903-103">신뢰할 수 있는 서비스 프로그래밍 모델 고급 사용법</span><span class="sxs-lookup"><span data-stu-id="23903-103">Advanced usage of the Reliable Services programming model</span></span>
<span data-ttu-id="23903-104">Azure 서비스 패브릭은 신뢰할 수 있는 상태 비저장 및 상태 저장 서비스의 작성과 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="23903-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span></span> <span data-ttu-id="23903-105">이 가이드는 서비스에 대한 더 많은 제어와 유연성을 확보할 수 있는 Reliable Services의 고급 사용법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="23903-105">This guide talks about advanced usages of Reliable Services to gain more control and flexibility over your services.</span></span> <span data-ttu-id="23903-106">이 가이드를 읽기 전에 [신뢰할 수 있는 서비스 프로그래밍 모델](service-fabric-reliable-services-introduction.md)에 대해 숙지하세요.</span><span class="sxs-lookup"><span data-stu-id="23903-106">Prior to reading this guide, familiarize yourself with [the Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span></span>

<span data-ttu-id="23903-107">상태 저장 서비스와 상태 비저장 서비스 모두 사용자 코드에 대한 두 개의 기본 진입점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-107">Both stateful and stateless services have two primary entry points for user code:</span></span>

* <span data-ttu-id="23903-108">`RunAsync(C#) / runAsync(Java)` 는 서비스 코드에 대한 범용 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="23903-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span></span>
* <span data-ttu-id="23903-109">`CreateServiceReplicaListeners(C#)` 및 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)`는 클라이언트 요청에 대한 통신 수신기를 여는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span></span>

<span data-ttu-id="23903-110">대부분의 서비스에는 이 두 진입점만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-110">For most services, these two entry points are sufficient.</span></span> <span data-ttu-id="23903-111">드문 경우이지만 서비스의 수명 주기에 대한 제어를 강화해야 하는 경우 추가 수명 주기 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span></span>

## <a name="stateless-service-instance-lifecycle"></a><span data-ttu-id="23903-112">상태 비저장 서비스 인스턴스 수명 주기</span><span class="sxs-lookup"><span data-stu-id="23903-112">Stateless service instance lifecycle</span></span>
<span data-ttu-id="23903-113">상태 비저장 서비스의 수명 주기는 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="23903-113">A stateless service's lifecycle is very simple.</span></span> <span data-ttu-id="23903-114">상태 비저장 서비스는 열리거나, 닫히거나, 중단될 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-114">A stateless service can only be opened, closed, or aborted.</span></span> <span data-ttu-id="23903-115">`RunAsync`는 서비스 인스턴스가 열리면 실행되고 서비스 인스턴스가 닫히거나 중단되면 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span></span>

<span data-ttu-id="23903-116">`RunAsync` 는 거의 모든 경우에 충분하지만 상태 비저장 서비스의 열기, 닫기 및 중단 이벤트는에 다음을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-116">Although `RunAsync` should be sufficient in almost all cases, the open, close, and abort events in a stateless service are also available:</span></span>

* <span data-ttu-id="23903-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` 상태 비저장 서비스 인스턴스를 사용하려고 할 때 OnOpenAsync가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when the stateless service instance is about to be used.</span></span> <span data-ttu-id="23903-118">이때 확장된 서비스 초기화 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-118">Extended service initialization tasks can be started at this time.</span></span>
* <span data-ttu-id="23903-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` 상태 비저장 서비스 인스턴스가 정상적으로 종료되려고 할 때 OnCloseAsync가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when the stateless service instance is going to be gracefully shut down.</span></span> <span data-ttu-id="23903-120">이는 서비스의 코드를 업그레이드할 때, 로드 균형 조정으로 인해 서비스 인스턴스가 이동할 때 또는 일시적인 오류가 감지되었을 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-120">This can occur when the service's code is being upgraded, the service instance is being moved due to load balancing, or a transient fault is detected.</span></span> <span data-ttu-id="23903-121">OnCloseAsync를 사용하여 모든 리소스를 안전하게 닫거나, 백그라운드 프로세싱을 중지하거나, 외부 상태 저장을 완료하거나, 기존 연결을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-121">OnCloseAsync can be used to safely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span></span>
* <span data-ttu-id="23903-122">`void OnAbort() - C# / void onAbort() - Java` 상태 비저장 서비스 인스턴스가 정상적으로 종료되려고 할 때 OnAbort가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when the stateless service instance is being forcefully shut down.</span></span> <span data-ttu-id="23903-123">이는 일반적으로 노드에서 영구 오류가 감지되거나, 내부 오류로 인해 서비스 패브릭에서 서비스 인스턴스 수명 주기를 안정적으로 관리할 수 없을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-123">This is generally called when a permanent fault is detected on the node, or when Service Fabric cannot reliably manage the service instance's lifecycle due to internal failures.</span></span>

## <a name="stateful-service-replica-lifecycle"></a><span data-ttu-id="23903-124">상태 저장 서비스 복제본 수명 주기</span><span class="sxs-lookup"><span data-stu-id="23903-124">Stateful service replica lifecycle</span></span>

> [!NOTE]
> <span data-ttu-id="23903-125">상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-125">Stateful reliable services are not supported in Java yet.</span></span>
>
>

<span data-ttu-id="23903-126">상태 저장 서비스 복제본의 수명 주기는 상태 비저장 서비스 인스턴스보다 훨씬 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="23903-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span></span> <span data-ttu-id="23903-127">열기, 닫기 및 중단 이벤트 외에 상태 저장 서비스 복제본은 수명 동안 역할이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-127">In addition to open, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span></span> <span data-ttu-id="23903-128">상태 저장 서비스 복제본의 역할이 변경된 경우 `OnChangeRoleAsync` 이벤트가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-128">When a stateful service replica changes role, the `OnChangeRoleAsync` event is triggered:</span></span>

* <span data-ttu-id="23903-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` 상태 저장 서비스 복제본이 역할을 변경할 경우(예: 주 또는 보조) OnChangeRoleAsync가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when the stateful service replica is changing role, for example to primary or secondary.</span></span> <span data-ttu-id="23903-130">주 복제본에는 쓰기 상태가 지정됩니다(신뢰할 수 있는 컬렉션을 만들고 쓰도록 허용).</span><span class="sxs-lookup"><span data-stu-id="23903-130">Primary replicas are given write status (are allowed to create and write to Reliable Collections).</span></span> <span data-ttu-id="23903-131">보조 복제본에는 읽기 상태가 지정됩니다(신뢰할 수 있는 기존 컬렉션에서 읽기만 가능).</span><span class="sxs-lookup"><span data-stu-id="23903-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span></span> <span data-ttu-id="23903-132">상태 저장 서비스에서 대부분의 작업은 주 복제본에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-132">Most work in a stateful service is performed at the primary replica.</span></span> <span data-ttu-id="23903-133">보조 복제본은 읽기 전용 유효성 검사, 보고서 생성, 데이터 마이닝 또는 다른 읽기 전용 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span></span>

<span data-ttu-id="23903-134">상태 저장 서비스에서는 주 복제본만 상태에 대한 쓰기 권한을 가지므로 일반적으로 서비스에서 실제 작업을 수행하는 경우에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-134">In a stateful service, only the primary replica has write access to state and thus is generally when the service is performing actual work.</span></span> <span data-ttu-id="23903-135">상태 저장 서비스의 `RunAsync` 메서드는 상태 저장 서비스 복제본이 주 복제본인 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-135">The `RunAsync` method in a stateful service is executed only when the stateful service replica is primary.</span></span> <span data-ttu-id="23903-136">주 복제본의 역할이 변경되거나 닫기 또는 중단 이벤트 중에는 `RunAsync` 메서드가 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="23903-136">The `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during the close and abort events.</span></span>

<span data-ttu-id="23903-137">`OnChangeRoleAsync` 이벤트를 사용하면 복제본의 역할에 따라 작업을 수행하거나 역할 변경에 대한 응답으로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23903-137">Using the `OnChangeRoleAsync` event allows you to perform work depending on replica role as well as in response to role change.</span></span>

<span data-ttu-id="23903-138">또한 상태 저장 서비스는 상태 비저장 서비스와 동일한 4개의 수명 주기 이벤트(의미 체계 및 사용 사례가 동일함)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="23903-138">A stateful service also provides the same four lifecycle events as a stateless service, with the same semantics and use cases:</span></span>

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a><span data-ttu-id="23903-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23903-139">Next steps</span></span>
<span data-ttu-id="23903-140">서비스 패브릭과 관련된 고급 항목을 보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23903-140">For more advanced topics related to Service Fabric, see the following articles:</span></span>

* [<span data-ttu-id="23903-141">상태 저장 Reliable Services 구성</span><span class="sxs-lookup"><span data-stu-id="23903-141">Configuring stateful Reliable Services</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="23903-142">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="23903-142">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="23903-143">문제 해결을 위해 시스템 상태 보고서 사용</span><span class="sxs-lookup"><span data-stu-id="23903-143">Using system health reports for troubleshooting</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="23903-144">서비스 패브릭 클러스터 리소스 관리자를 사용한 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="23903-144">Configuring Services with the Service Fabric Cluster Resource Manager</span></span>](service-fabric-cluster-resource-manager-configure-services.md)
