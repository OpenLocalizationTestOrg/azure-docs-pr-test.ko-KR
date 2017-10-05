---
title: "Reliable Actors 상태 관리 | Microsoft Docs"
description: "고가용성을 위해 Reliable Actors 상태를 관리, 유지 및 복제하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="b1cf4-103">Reliable Actors 상태 관리</span><span class="sxs-lookup"><span data-stu-id="b1cf4-103">Reliable Actors state management</span></span>
<span data-ttu-id="b1cf4-104">Reliable Actors는 논리와 상태를 모두 캡슐화할 수 있는 단일 스레드 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="b1cf4-105">행위자가 Reliable Services에서 실행되므로 Reliable Services에서 사용하는 동일한 지속성 및 복제 메커니즘을 사용하여 안전하게 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="b1cf4-106">이러한 방식으로 행위자는 실패한 후에 해당 상태를 손실하지 않고 가비지 수집 후 다시 활성화합니다. 또한 리소스 균형 조정 또는 업그레이드로 인해 클러스터의 노드 간에 이동하는 경우에도 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="b1cf4-107">상태 지속성 및 복제</span><span class="sxs-lookup"><span data-stu-id="b1cf4-107">State persistence and replication</span></span>
<span data-ttu-id="b1cf4-108">각 행위자 인스턴스가 고유 ID에 매핑되기 때문에 모든 Reliable Actors는 *상태 저장* 이라고 여겨집니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="b1cf4-109">즉, 동일한 행위자 ID에 대한 반복된 호출이 동일한 행위자 인스턴스에 라우트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="b1cf4-110">상태 비저장 시스템에서 대조적으로 클라이언트 호출이 매번 동일한 서버에 라우트되도록 보장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="b1cf4-111">따라서 행위자 서비스는 항상 상태 저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="b1cf4-112">행위자가 상태 저장을 고려하더라도 상태를 안정적으로 저장해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="b1cf4-113">행위자는 해당 데이터 저장소 요구 사항에 따라 상태 지속성 및 복제의 수준을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="b1cf4-114">**지속된 상태:** 상태가 디스크에 유지되고 3개 이상의 복제본에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="b1cf4-115">상태가 전체 클러스터 가동 중단을 통해 유지할 수 있는 가장 지속적인 상태 저장 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="b1cf4-116">**일시적 상태:** 상태는 3개 이상의 복제본에 복제되고 메모리에만 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="b1cf4-117">업그레이드 및 리소스 균형을 조정하는 동안 노드 실패 및 행위자 실패에 대한 복원력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="b1cf4-118">그러나 상태는 디스크에 유지되지 않으므로</span><span class="sxs-lookup"><span data-stu-id="b1cf4-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="b1cf4-119">한 번에 모든 복제본이 손실되면 상태도 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="b1cf4-120">**지속된 상태 없음:** 상태가 복제되거나 디스크에 기록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="b1cf4-121">이 수준은 단순히 상태를 안정적으로 유지할 필요가 없는 행위자의 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="b1cf4-122">지속성의 수준은 각각 단순히 *상태 제공자* 및 서비스의 *복제* 구성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="b1cf4-123">상태가 디스크에 기록되는지 여부는 상태를 저장하는 Reliable Service의 구성 요소인 상태 제공자에 따라 달라지며</span><span class="sxs-lookup"><span data-stu-id="b1cf4-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="b1cf4-124">복제는 서비스를 배포한 복제본 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="b1cf4-125">Reliable Services와 마찬가지로 상태 제공자와 복제본 수는 모두 쉽게 수동으로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="b1cf4-126">행위자 프레임워크는 특성을 제공합니다. 이 특성은 행위자에 사용될 경우 자동으로 기본 상태 제공자를 선택하고 이러한 세 가지 지속성 설정 중 하나를 달성하기 위해 복제본 수에 대한 설정을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="b1cf4-127">StatePersistence 특성은 파생 클래스에서 상속되지 않으며 각 행위자 형식은 해당 StatePersistence 수준을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="b1cf4-128">지속된 상태</span><span class="sxs-lookup"><span data-stu-id="b1cf4-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="b1cf4-129">이 설정은 디스크에 데이터를 저장하는 상태 제공자를 사용하고 자동으로 서비스 복제본 수를 3으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="b1cf4-130">일시적 상태</span><span class="sxs-lookup"><span data-stu-id="b1cf4-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="b1cf4-131">이 설정은 메모리내 전용 상태 제공자를 사용하고 복제본 수를 3으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="b1cf4-132">지속된 상태 없음</span><span class="sxs-lookup"><span data-stu-id="b1cf4-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="b1cf4-133">이 설정은 메모리내 전용 상태 제공자를 사용하고 복제본 수를 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="b1cf4-134">기본값 및 생성된 설정</span><span class="sxs-lookup"><span data-stu-id="b1cf4-134">Defaults and generated settings</span></span>
<span data-ttu-id="b1cf4-135">`StatePersistence` 특성을 사용하는 경우 행위자 서비스를 시작할 때 런타임 시 상태 제공자가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="b1cf4-136">그러나 복제본 수는 Visual Studio 행위자 빌드 도구에 의해 컴파일 시점에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="b1cf4-137">빌드 도구는 ApplicationManifest.xml의 행위자 서비스에 대한 *기본 서비스* 를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="b1cf4-138">**최소 복제본 세트 크기** 및 **대상 복제본 세트 크기**에 대한 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="b1cf4-139">이러한 매개 변수를 수동으로 변경할 수 있지만</span><span class="sxs-lookup"><span data-stu-id="b1cf4-139">You can change these parameters manually.</span></span> <span data-ttu-id="b1cf4-140">`StatePersistence` 특성을 변경할 때마다 매개 변수는 이전 값을 재정의하여 선택된 `StatePersistence` 특성에 대한 기본 복제본 세트 크기 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="b1cf4-141">즉, ServiceManifest.xml에서 설정한 값은 `StatePersistence` 특성 값을 변경하는 경우 빌드 시에*만* 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="b1cf4-142">상태 관리자</span><span class="sxs-lookup"><span data-stu-id="b1cf4-142">State manager</span></span>
<span data-ttu-id="b1cf4-143">모든 행위자 인스턴스에는 안정적으로 키/값 쌍을 저장하는 사전 형식의 데이터 구조인 고유한 상태 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="b1cf4-144">상태 관리자는 상태 제공자에 대한 래퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="b1cf4-145">사용되는 지속성 설정에 상관없이 데이터를 저장하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="b1cf4-146">실행 중인 행위자 서비스가 데이터를 유지하는 동안 롤링 업그레이드를 통해 지속된 상태로 설정된 일시적인(메모리 내 전용) 상태에서 변경될 수 있음을 보증하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="b1cf4-147">그러나 실행 중인 서비스에 대한 복제본 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="b1cf4-148">상태 관리자 키는 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-148">State manager keys must be strings.</span></span> <span data-ttu-id="b1cf4-149">값은 제네릭 및 사용자 지정 형식을 포함한 모든 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="b1cf4-150">복제하는 동안 네트워크를 통해 다른 노드로 전송될 수 있기 때문에 상태 관리자에 저장된 값은 데이터 계약을 직렬화 가능해야 하며 행위자의 상태 지속성 설정에 따라 디스크에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="b1cf4-151">상태 관리자는 신뢰할 수 있는 사전에 있는 것과 비슷한 상태를 관리하기 위한 일반적인 사전 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="b1cf4-152">상태 액세스</span><span class="sxs-lookup"><span data-stu-id="b1cf4-152">Accessing state</span></span>
<span data-ttu-id="b1cf4-153">상태 관리자를 통해 키로 상태에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="b1cf4-154">상태 관리자 메서드는 행위자가 지속된 상태인 경우 디스크 I/O가 필요할 수 있기에 모두 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="b1cf4-155">첫 번째 액세스에서 상태 개체는 메모리에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="b1cf4-156">반복 액세스 작업은 메모리에서 직접 개체에 액세스하고 오버헤드를 전환하는 디스크 I/O 또는 비동기 컨텍스트를 발생시키지 않고 동기적으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="b1cf4-157">상태 개체는 다음과 같은 경우에 캐시에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="b1cf4-158">행위자 메서드는 상태 관리자에서 개체를 검색한 후에 처리되지 않은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="b1cf4-159">비활성화되거나 오류 발생 후에 행위자가 다시 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="b1cf4-160">상태 제공자가 디스크에 상태를 페이징합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-160">The state provider pages state to disk.</span></span> <span data-ttu-id="b1cf4-161">이 동작은 상태 제공자 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="b1cf4-162">`Persisted` 설정에 대한 기본 상태 제공자는 이 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="b1cf4-163">키에 대한 항목이 없는 경우 `KeyNotFoundException`(C#) 또는 `NoSuchElementException`(Java)를 throw하는 표준 *Get* 작업을 사용하여 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="b1cf4-164">또한 키에 대한 항목이 없는 경우 throw하지 않는 *TryGet* 메서드를 사용하여 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="b1cf4-165">상태 저장</span><span class="sxs-lookup"><span data-stu-id="b1cf4-165">Saving state</span></span>
<span data-ttu-id="b1cf4-166">상태 관리자 검색 메서드는 로컬 메모리에 개체에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="b1cf4-167">로컬 메모리에서 이 개체를 수정하는 것만으로는 지속적으로 저장하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="b1cf4-168">개체를 상태 관리자에서 검색하고 수정하는 경우 지속적으로 저장되도록 상태 관리자에 다시 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="b1cf4-169">`dictionary["key"] = value` 구문과 동등한 무조건 *설정*을 사용하여 상태를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="b1cf4-170">*Add* 메서드를 사용하여 상태를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="b1cf4-171">이미 존재하는 키를 추가하려고 하면 이 메서드가 `InvalidOperationException`(C#) 또는 `IllegalStateException`(Java)을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="b1cf4-172">*TryAdd* 메서드를 사용하여 상태를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="b1cf4-173">이미 존재하는 키를 추가하려고 하면 이 메서드가 throw하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-173">This method does not throw when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="b1cf4-174">행위자 메서드가 끝날 때 상태 관리자는 삽입 또는 업데이트 작업에 의해 추가되거나 수정된 모든 값을 자동으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="b1cf4-175">"저장"은 사용된 설정에 따라 디스크와 복제를 지속하도록 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="b1cf4-176">수정되지 않은 값은 지속되거나 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="b1cf4-177">수정된 값이 없는 경우 저장 작업은 아무 것도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="b1cf4-178">실패를 저장하는 경우 수정된 상태는 삭제되고 원래 상태를 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="b1cf4-179">또한 행위자 기반의 `SaveStateAsync` 메서드를 호출하여 상태를 수동으로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="b1cf4-180">상태 제거</span><span class="sxs-lookup"><span data-stu-id="b1cf4-180">Removing state</span></span>
<span data-ttu-id="b1cf4-181">*제거* 메서드 호출하여 행위자의 상태 관리자에서 상태를 영구적으로 상태를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="b1cf4-182">존재하지 않는 키를 제거하려고 하면 이 메서드가 `KeyNotFoundException`(C#) 또는 `NoSuchElementException`(Java)을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="b1cf4-183">*TryRemove* 메서드를 사용하여 상태를 영구적으로 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="b1cf4-184">존재하지 않는 키를 제거하려고 하면 이 메서드가 throw하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b1cf4-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1cf4-185">Next steps</span></span>

<span data-ttu-id="b1cf4-186">Reliable Actors에 저장된 상태를 디스크에 기록하고 고가용성을 위해 복제하기 전에 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="b1cf4-187">[행위자 형식 직렬화](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="b1cf4-188">다음으로 [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1cf4-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
