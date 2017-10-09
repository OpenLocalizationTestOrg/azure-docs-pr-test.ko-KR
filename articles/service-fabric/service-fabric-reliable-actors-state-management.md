---
title: "상태 관리를 aaaReliable 행위자 | Microsoft Docs"
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
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="5cbda-103">Reliable Actors 상태 관리</span><span class="sxs-lookup"><span data-stu-id="5cbda-103">Reliable Actors state management</span></span>
<span data-ttu-id="5cbda-104">Reliable Actors는 논리와 상태를 모두 캡슐화할 수 있는 단일 스레드 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="5cbda-105">행위자 신뢰할 수 있는 서비스를 실행 하기 때문에 유지할 수 있습니다 상태 안정적으로 사용 하 여 hello 신뢰할 수 있는 서비스를 사용 하는 동일한 지 속성 및 복제 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="5cbda-106">이러한 방식으로 행위자 tooresource 분산 또는 업그레이드 인해 클러스터 노드 간에 이동 하는 경우 또는 가비지 수집 후 다시 활성화 되 면 실패 후의 상태를 손실 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="5cbda-107">상태 지속성 및 복제</span><span class="sxs-lookup"><span data-stu-id="5cbda-107">State persistence and replication</span></span>
<span data-ttu-id="5cbda-108">모든 Reliable Actors를 사용 하는 것으로 간주 *stateful* 행위자 인스턴스마다 tooa 고유한 id입니다. 매핑되기 때문에</span><span class="sxs-lookup"><span data-stu-id="5cbda-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="5cbda-109">즉, 동일한 행위자 ID는 해당 반복된 하 여 호출 toohello 라우팅된 toohello 행위자 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="5cbda-110">상태 비저장 시스템에서 반면 클라이언트 호출 되지 않을 수도 라우팅된 toobe toohello 될 때마다 동일한 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="5cbda-111">따라서 행위자 서비스는 항상 상태 저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="5cbda-112">행위자가 상태 저장을 고려하더라도 상태를 안정적으로 저장해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="5cbda-113">행위자 상태 지 속성의 hello 수준을 선택할 수 및 해당 데이터에 따라 복제 저장소 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="5cbda-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="5cbda-114">**영구적인 상태가**: 상태 지속형된 toodisk 이며 복제 too3 또는 이상의 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="5cbda-115">전체 클러스터 가동 중단을 통해 상태 유지할 수 있는 hello 가장 안정적인 상태 저장소 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="5cbda-116">**일시적 상태**: 상태는 복제 된 too3 또는 이상의 복제본 및 메모리에만 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="5cbda-117">업그레이드 및 리소스 균형을 조정하는 동안 노드 실패 및 행위자 실패에 대한 복원력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="5cbda-118">그러나 상태가 지속 된 toodisk 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="5cbda-119">따라서 모든 복제 데이터베이스를 한 번에 손실 되 면 hello 상태가 손실 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="5cbda-120">**지속 된 상태가 없는**: 상태는 복제 또는 toodisk 기록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="5cbda-121">이 수준은 단순히 toomaintain 상태를 안정적으로 필요 하지 않습니다는 행위자를 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="5cbda-122">지속성의 수준은 각각 단순히 *상태 제공자* 및 서비스의 *복제* 구성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="5cbda-123">상태 기록 여부 toodisk hello 상태 공급자--상태를 저장 하는 신뢰할 수 있는 서비스의 hello 구성 요소에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="5cbda-124">복제는 서비스를 배포한 복제본 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="5cbda-125">신뢰할 수 있는 서비스와 마찬가지로 상태 공급자 둘 다 hello 및 복제본 수 수동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="5cbda-126">hello 행위자 프레임 워크에서 사용할 때 행위자를 자동으로 선택 하는 기본 상태 공급자를 복제본 개수 tooachieve 이러한 세 개의 지 속성 설정 중 하나에 대 한 설정을 자동으로 생성 하는 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="5cbda-127">파생된 클래스에서 hello StatePersistence 특성을 상속 하지, 각 행위자 형식이 해당 StatePersistence 수준을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="5cbda-128">지속된 상태</span><span class="sxs-lookup"><span data-stu-id="5cbda-128">Persisted state</span></span>
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
<span data-ttu-id="5cbda-129">이 설정은 디스크에 데이터를 저장 하 고 hello 서비스 복제본 개수 too3를 자동으로 설정 하는 상태 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="5cbda-130">일시적 상태</span><span class="sxs-lookup"><span data-stu-id="5cbda-130">Volatile state</span></span>
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
<span data-ttu-id="5cbda-131">이 설정에서는에서 메모리-전용 상태 공급자를 사용 하 고 집합 hello 복제본 개수 too3.</span><span class="sxs-lookup"><span data-stu-id="5cbda-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="5cbda-132">지속된 상태 없음</span><span class="sxs-lookup"><span data-stu-id="5cbda-132">No persisted state</span></span>
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
<span data-ttu-id="5cbda-133">이 설정에서는에서 메모리-전용 상태 공급자를 사용 하 고 집합 hello 복제본 개수 too1.</span><span class="sxs-lookup"><span data-stu-id="5cbda-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="5cbda-134">기본값 및 생성된 설정</span><span class="sxs-lookup"><span data-stu-id="5cbda-134">Defaults and generated settings</span></span>
<span data-ttu-id="5cbda-135">Hello를 사용 하는 경우 `StatePersistence` 특성 상태 공급자를 자동으로 선택 됩니다 런타임 시 hello 행위자 서비스가 시작 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="5cbda-136">그러나 hello 복제본 수 설정한 컴파일 타임에 Visual Studio 행위자 hello 빌드 도구.</span><span class="sxs-lookup"><span data-stu-id="5cbda-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="5cbda-137">hello 빌드 도구를 자동으로 생성 한 *기본 서비스* applicationmanifest.xml에서 hello 행위자 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="5cbda-138">**최소 복제본 세트 크기** 및 **대상 복제본 세트 크기**에 대한 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="5cbda-139">이러한 매개 변수를 수동으로 변경할 수 있지만</span><span class="sxs-lookup"><span data-stu-id="5cbda-139">You can change these parameters manually.</span></span> <span data-ttu-id="5cbda-140">하지만 각 시간 hello `StatePersistence` 특성이 변경 되거나, hello 매개 변수가 toohello 복제본 집합 크기에 대 한 기본값 선택 hello 설정 `StatePersistence` 특성을 이전 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="5cbda-141">즉, ServiceManifest.xml에 설정한 hello 값은 *만* hello를 변경할 때 빌드 시 재정의 `StatePersistence` 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="5cbda-142">상태 관리자</span><span class="sxs-lookup"><span data-stu-id="5cbda-142">State manager</span></span>
<span data-ttu-id="5cbda-143">모든 행위자 인스턴스에는 안정적으로 키/값 쌍을 저장하는 사전 형식의 데이터 구조인 고유한 상태 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="5cbda-144">hello 상태 관리자는 상태 공급자 주변 래퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="5cbda-145">사용할 수 있습니다 toostore 데이터에 관계 없이 어떤 지 속성 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="5cbda-146">휘발성 (에서 메모리-전용) 상태로 설정 tooa에서 실행 중인 행위자 서비스를 변경할 수 있습니다 보장은 데이터를 유지 하면서 롤링 업그레이드를 통해 상태 설정을 유지는 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="5cbda-147">그러나 것이 실행 중인 서비스에 대 한 가능한 toochange 복제본 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="5cbda-148">상태 관리자 키는 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-148">State manager keys must be strings.</span></span> <span data-ttu-id="5cbda-149">값은 제네릭 및 사용자 지정 형식을 포함한 모든 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="5cbda-150">Hello 상태 관리자에 저장 된 값 복제 하는 동안 hello 네트워크 tooother 노드를 통해 전송 될 수 있습니다 toodisk 행위자의 상태 지 속성 설정에 따라 작성 될 수도 있기 때문에 데이터 계약 직렬화 가능 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="5cbda-151">hello 상태 관리자는 신뢰할 수 있는 사전에서 찾을 수 유사한 toothose, 상태 관리에 대 한 일반적인 사전 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="5cbda-152">상태 액세스</span><span class="sxs-lookup"><span data-stu-id="5cbda-152">Accessing state</span></span>
<span data-ttu-id="5cbda-153">상태 키로 hello 상태 관리자를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="5cbda-154">상태 관리자 메서드는 행위자가 지속된 상태인 경우 디스크 I/O가 필요할 수 있기에 모두 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="5cbda-155">첫 번째 액세스에서 상태 개체는 메모리에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="5cbda-156">반복 액세스 작업은 메모리에서 직접 개체에 액세스하고 오버헤드를 전환하는 디스크 I/O 또는 비동기 컨텍스트를 발생시키지 않고 동기적으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="5cbda-157">상태 개체 hello 비활성화의 hello 캐시에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="5cbda-158">Hello 상태 관리자에서 개체를 검색 한 후에 처리 되지 않은 예외를 throw 하는 행위자 메서드.</span><span class="sxs-lookup"><span data-stu-id="5cbda-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="5cbda-159">비활성화되거나 오류 발생 후에 행위자가 다시 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="5cbda-160">hello 상태 공급자 페이지 toodisk을 사항을 기술 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="5cbda-161">이 동작은 hello 상태 공급자 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="5cbda-162">hello에 대 한 기본 상태 공급자 hello `Persisted` 이 동작을 포함 하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="5cbda-163">표준을 사용 하 여 상태를 검색할 수 있습니다 *가져오기* throw 하는 작업 `KeyNotFoundException`(C#) 또는 `NoSuchElementException`hello 키에 대 한 항목이 없는 경우 (Java):</span><span class="sxs-lookup"><span data-stu-id="5cbda-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="5cbda-164">또한 키에 대한 항목이 없는 경우 throw하지 않는 *TryGet* 메서드를 사용하여 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="5cbda-165">상태 저장</span><span class="sxs-lookup"><span data-stu-id="5cbda-165">Saving state</span></span>
<span data-ttu-id="5cbda-166">hello 상태 관리자 검색 메서드는 로컬 메모리에 참조 방식 tooan 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="5cbda-167">만 로컬 메모리에이 개체를 수정 않을 것 toobe 영구적으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="5cbda-168">개체가, hello 상태 관리자에서 검색 및 수정 하는 경우 영구적으로 저장 하는 hello 상태 관리자 toobe에 다시 삽입할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="5cbda-169">프로그램 무조건를 사용 하 여 상태를 삽입할 수 있습니다 *설정*는 hello의 해당 하는 hello은 `dictionary["key"] = value` 구문:</span><span class="sxs-lookup"><span data-stu-id="5cbda-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="5cbda-170">*Add* 메서드를 사용하여 상태를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="5cbda-171">이 메서드에서 throw `InvalidOperationException`(C#) 또는 `IllegalStateException`tooadd 이미 존재 하는 키를 읽으려고 할 때 (Java).</span><span class="sxs-lookup"><span data-stu-id="5cbda-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="5cbda-172">*TryAdd* 메서드를 사용하여 상태를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="5cbda-173">이 메서드는 tooadd 이미 존재 하는 키를 읽으려고 할 때 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="5cbda-174">행위자 메서드의 hello 끝 hello 상태 관리자 삽입 또는 업데이트 작업에 의해 수정 되거나 추가 된 모든 값을 자동으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="5cbda-175">"저장" 유지 toodisk 및 복제에 사용 되는 hello 설정에 따라 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="5cbda-176">수정되지 않은 값은 지속되거나 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="5cbda-177">값이 없으면이 수정 된 경우 저장 작업이 hello는 아무 작업도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="5cbda-178">저장이 실패할 경우 hello 수정된 상태를 삭제 하 고 hello 원래 상태를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="5cbda-179">Hello를 호출 하 여 상태를 수동으로 저장할 수도 있습니다 `SaveStateAsync` 기본 hello 행위자 메서드:</span><span class="sxs-lookup"><span data-stu-id="5cbda-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="5cbda-180">상태 제거</span><span class="sxs-lookup"><span data-stu-id="5cbda-180">Removing state</span></span>
<span data-ttu-id="5cbda-181">Hello를 호출 하 여 위에 행위자의 상태 관리자에서 상태를 영구적으로 제거할 수 있습니다 *제거* 메서드.</span><span class="sxs-lookup"><span data-stu-id="5cbda-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="5cbda-182">이 메서드에서 throw `KeyNotFoundException`(C#) 또는 `NoSuchElementException`tooremove 존재 하지 않는 키를 읽으려고 할 때 (Java).</span><span class="sxs-lookup"><span data-stu-id="5cbda-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="5cbda-183">Hello를 사용 하 여 상태를 영구적으로 제거할 수도 있습니다 *TryRemove* 메서드.</span><span class="sxs-lookup"><span data-stu-id="5cbda-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="5cbda-184">이 메서드는 tooremove 존재 하지 않는 키를 읽으려고 할 때 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5cbda-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cbda-185">Next steps</span></span>

<span data-ttu-id="5cbda-186">Reliable Actors에 저장 된 상태는 작성 된 toodisk 전에 직렬화 하 고 고가용성을 위해 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="5cbda-187">[행위자 형식 직렬화](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="5cbda-188">다음으로 [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5cbda-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
