---
title: "신뢰할 수 있는 서비스의 aaaAdvanced 사용 | Microsoft Docs"
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
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a><span data-ttu-id="88605-103">고급 프로그래밍 모델 hello 신뢰할 수 있는 서비스의 사용</span><span class="sxs-lookup"><span data-stu-id="88605-103">Advanced usage of hello Reliable Services programming model</span></span>
<span data-ttu-id="88605-104">Azure 서비스 패브릭은 신뢰할 수 있는 상태 비저장 및 상태 저장 서비스의 작성과 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span></span> <span data-ttu-id="88605-105">이 가이드 발언 toogain 신뢰할 수 있는 서비스의 고급 사용에 대 한 보다 많은 제어 및 유연성에 서비스를 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-105">This guide talks about advanced usages of Reliable Services toogain more control and flexibility over your services.</span></span> <span data-ttu-id="88605-106">이전 tooreading 안내이 잘 이해 [hello 신뢰할 수 있는 서비스 프로그래밍 모델](service-fabric-reliable-services-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-106">Prior tooreading this guide, familiarize yourself with [hello Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span></span>

<span data-ttu-id="88605-107">상태 저장 서비스와 상태 비저장 서비스 모두 사용자 코드에 대한 두 개의 기본 진입점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-107">Both stateful and stateless services have two primary entry points for user code:</span></span>

* <span data-ttu-id="88605-108">`RunAsync(C#) / runAsync(Java)` 는 서비스 코드에 대한 범용 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="88605-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span></span>
* <span data-ttu-id="88605-109">`CreateServiceReplicaListeners(C#)` 및 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)`는 클라이언트 요청에 대한 통신 수신기를 여는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span></span>

<span data-ttu-id="88605-110">대부분의 서비스에는 이 두 진입점만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-110">For most services, these two entry points are sufficient.</span></span> <span data-ttu-id="88605-111">드문 경우이지만 서비스의 수명 주기에 대한 제어를 강화해야 하는 경우 추가 수명 주기 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span></span>

## <a name="stateless-service-instance-lifecycle"></a><span data-ttu-id="88605-112">상태 비저장 서비스 인스턴스 수명 주기</span><span class="sxs-lookup"><span data-stu-id="88605-112">Stateless service instance lifecycle</span></span>
<span data-ttu-id="88605-113">상태 비저장 서비스의 수명 주기는 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-113">A stateless service's lifecycle is very simple.</span></span> <span data-ttu-id="88605-114">상태 비저장 서비스는 열리거나, 닫히거나, 중단될 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-114">A stateless service can only be opened, closed, or aborted.</span></span> <span data-ttu-id="88605-115">`RunAsync`는 서비스 인스턴스가 열리면 실행되고 서비스 인스턴스가 닫히거나 중단되면 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span></span>

<span data-ttu-id="88605-116">하지만 `RunAsync` 충분 해야에서 거의 모든 경우 hello open, close, 및 중단 이벤트는 상태 비저장 서비스에는 또한 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-116">Although `RunAsync` should be sufficient in almost all cases, hello open, close, and abort events in a stateless service are also available:</span></span>

* <span data-ttu-id="88605-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync는 toobe 사용에 대 한 hello 상태 비저장 서비스 인스턴스가 되는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when hello stateless service instance is about toobe used.</span></span> <span data-ttu-id="88605-118">이때 확장된 서비스 초기화 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-118">Extended service initialization tasks can be started at this time.</span></span>
* <span data-ttu-id="88605-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`Hello 상태 비저장 서비스 인스턴스 toobe 때 OnCloseAsync 호출은 정상적으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when hello stateless service instance is going toobe gracefully shut down.</span></span> <span data-ttu-id="88605-120">이 hello 서비스 코드를 업그레이드 하는 중, tooload 분산 인해 hello 서비스 인스턴스를 이동 하는 일시적인 오류 검색 될 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-120">This can occur when hello service's code is being upgraded, hello service instance is being moved due tooload balancing, or a transient fault is detected.</span></span> <span data-ttu-id="88605-121">OnCloseAsync 수 수 사용된 toosafely 닫고 모든 리소스, 백그라운드 처리를 중지, 외부 상태를 저장 또는 기존 연결을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-121">OnCloseAsync can be used toosafely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span></span>
* <span data-ttu-id="88605-122">`void OnAbort() - C# / void onAbort() - Java`OnAbort는 hello 상태 비저장 서비스 인스턴스가 강제로 종료 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when hello stateless service instance is being forcefully shut down.</span></span> <span data-ttu-id="88605-123">이 서비스 패브릭 toointernal 오류 인해 hello 서비스 인스턴스 수명 주기를 안정적으로 관리할 수 없는 경우 또는 hello 노드 영구 오류가 발견 되 면 일반적으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-123">This is generally called when a permanent fault is detected on hello node, or when Service Fabric cannot reliably manage hello service instance's lifecycle due toointernal failures.</span></span>

## <a name="stateful-service-replica-lifecycle"></a><span data-ttu-id="88605-124">상태 저장 서비스 복제본 수명 주기</span><span class="sxs-lookup"><span data-stu-id="88605-124">Stateful service replica lifecycle</span></span>

> [!NOTE]
> <span data-ttu-id="88605-125">상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-125">Stateful reliable services are not supported in Java yet.</span></span>
>
>

<span data-ttu-id="88605-126">상태 저장 서비스 복제본의 수명 주기는 상태 비저장 서비스 인스턴스보다 훨씬 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span></span> <span data-ttu-id="88605-127">또한 tooopen, 닫고, 중단할 이벤트, 상태 저장 서비스 복제본의 수명 동안 역할 변경 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-127">In addition tooopen, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span></span> <span data-ttu-id="88605-128">상태 저장 서비스 복제본 역할 변경 되 면 hello `OnChangeRoleAsync` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-128">When a stateful service replica changes role, hello `OnChangeRoleAsync` event is triggered:</span></span>

* <span data-ttu-id="88605-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync는 hello 상태 저장 서비스 복제본 역할, 예: tooprimary 또는 보조 복제본이 변경 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when hello stateful service replica is changing role, for example tooprimary or secondary.</span></span> <span data-ttu-id="88605-130">주 복제본에는 쓰기 상태가 제공 됩니다 (toocreate 수 및 tooReliable 컬렉션 쓰기).</span><span class="sxs-lookup"><span data-stu-id="88605-130">Primary replicas are given write status (are allowed toocreate and write tooReliable Collections).</span></span> <span data-ttu-id="88605-131">보조 복제본에는 읽기 상태가 지정됩니다(신뢰할 수 있는 기존 컬렉션에서 읽기만 가능).</span><span class="sxs-lookup"><span data-stu-id="88605-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span></span> <span data-ttu-id="88605-132">상태 저장 서비스에서 대부분 작업 hello 주 복제본에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-132">Most work in a stateful service is performed at hello primary replica.</span></span> <span data-ttu-id="88605-133">보조 복제본은 읽기 전용 유효성 검사, 보고서 생성, 데이터 마이닝 또는 다른 읽기 전용 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span></span>

<span data-ttu-id="88605-134">상태 저장 서비스의 hello 주 복제본만 toostate 쓰기 권한을 가지 며 따라서 hello 서비스에서 실제 작업을 수행할 때 일반적으로</span><span class="sxs-lookup"><span data-stu-id="88605-134">In a stateful service, only hello primary replica has write access toostate and thus is generally when hello service is performing actual work.</span></span> <span data-ttu-id="88605-135">hello `RunAsync` hello 상태 저장 서비스 복제본이 주 하는 경우에 상태 저장 서비스의 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88605-135">hello `RunAsync` method in a stateful service is executed only when hello stateful service replica is primary.</span></span> <span data-ttu-id="88605-136">hello `RunAsync` 메서드 hello 중은 물론에서 기본 데이터베이스로 주 복제본의 역할 변경 닫고 이벤트를 중단 하는 경우 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88605-136">hello `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during hello close and abort events.</span></span>

<span data-ttu-id="88605-137">Hello를 사용 하 여 `OnChangeRoleAsync` 이벤트 하면 복제본의 역할에 따라도 응답 toorole 변경 에서처럼 tooperform 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88605-137">Using hello `OnChangeRoleAsync` event allows you tooperform work depending on replica role as well as in response toorole change.</span></span>

<span data-ttu-id="88605-138">상태 저장 서비스도도 제공 동일한 4 hello 수명 주기 이벤트는 상태 비저장 서비스와 동일한 의미 체계 hello 및 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="88605-138">A stateful service also provides hello same four lifecycle events as a stateless service, with hello same semantics and use cases:</span></span>

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a><span data-ttu-id="88605-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88605-139">Next steps</span></span>
<span data-ttu-id="88605-140">고급 항목 관련된 tooService 패브릭, hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="88605-140">For more advanced topics related tooService Fabric, see hello following articles:</span></span>

* [<span data-ttu-id="88605-141">상태 저장 Reliable Services 구성</span><span class="sxs-lookup"><span data-stu-id="88605-141">Configuring stateful Reliable Services</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="88605-142">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="88605-142">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="88605-143">문제 해결을 위해 시스템 상태 보고서 사용</span><span class="sxs-lookup"><span data-stu-id="88605-143">Using system health reports for troubleshooting</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="88605-144">Hello 서비스 패브릭 클러스터 리소스 관리자를 사용 하 여 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="88605-144">Configuring Services with hello Service Fabric Cluster Resource Manager</span></span>](service-fabric-cluster-resource-manager-configure-services.md)
