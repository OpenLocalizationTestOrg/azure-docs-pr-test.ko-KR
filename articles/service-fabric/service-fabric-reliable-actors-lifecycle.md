---
title: "행위자 기반 Azure 마이크로 서비스 수명 주기 개요 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actor 수명 주기, 가비지 수집 및 행위자와 해당 상태 수동 삭제에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="89612-103">행위자 수명 주기, 자동 가비지 수집 및 수동 삭제</span><span class="sxs-lookup"><span data-stu-id="89612-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="89612-104">행위자는 해당 메서드 중 하나가 처음 호출되면 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="89612-105">구성 가능한 기간 동안 사용되지 않으면 비활성화됩니다(행위자 런타임에 의한 가비지 수집).</span><span class="sxs-lookup"><span data-stu-id="89612-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="89612-106">행위자와 그 상태를 언제든지 수동으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="89612-107">행위자 활성화</span><span class="sxs-lookup"><span data-stu-id="89612-107">Actor activation</span></span>
<span data-ttu-id="89612-108">행위자가 활성화되면 다음 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="89612-109">행위자를 호출하는 경우 아직 활성화되지 않았으면 새 행위자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89612-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="89612-110">행위자의 상태가 로드됩니다(상태가 유지되는 경우).</span><span class="sxs-lookup"><span data-stu-id="89612-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="89612-111">`OnActivateAsync`(C#) 또는 `onActivateAsync`(Java)메서드(행위자 구현 시 재정의될 수 있음)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="89612-112">이제 행위자가 활성 상태인 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="89612-113">행위자 비활성화</span><span class="sxs-lookup"><span data-stu-id="89612-113">Actor deactivation</span></span>
<span data-ttu-id="89612-114">행위자 비활성화되면 다음과 같은 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="89612-115">행위자를 일정 기간 동안 사용하지 않으면 활성 행위자 테이블에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="89612-116">`OnDeactivateAsync`(C#) 또는 `onDeactivateAsync`(Java)메서드(행위자 구현 시 재정의될 수 있음)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="89612-117">그러면 행위자에 대한 모든 타이머가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="89612-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="89612-118">상태 변경과 같은 행위자 작업은 이 메서드에서 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="89612-119">패브릭 행위자 런타임에서는 일부 [행위자 활성화 및 비활성화 관련 이벤트](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89612-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="89612-120">진단 및 성능 모니터링에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="89612-121">행위자 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="89612-121">Actor garbage collection</span></span>
<span data-ttu-id="89612-122">행위자 비활성화되면 행위자 개체에 대한 참조가 해제되고 가비지가 CLR(공용 언어 런타임) 또는 JVM(Java 가상 컴퓨터) 가비지 수집기에 의해 정상적으로 수집될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="89612-123">가비지 수집에서는 행위자 개체를 정리하기만 하고, 행위자의 상태 관리자에 저장된 상태를 제거하지 **않습니다** .</span><span class="sxs-lookup"><span data-stu-id="89612-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="89612-124">다음에 행위자가 활성화되면 새 행위자 개체가 만들어지고 해당 상태가 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="89612-125">비활성화 및 가비지 수집 목적에서 "사용 중"으로 계산되는 항목</span><span class="sxs-lookup"><span data-stu-id="89612-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="89612-126">호출 수신</span><span class="sxs-lookup"><span data-stu-id="89612-126">Receiving a call</span></span>
* <span data-ttu-id="89612-127">`IRemindable.ReceiveReminderAsync` 메서드(행위자가 미리 알림을 사용하는 경우에만 해당).</span><span class="sxs-lookup"><span data-stu-id="89612-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="89612-128">행위자가 타이머를 사용하고 해당 타이머 콜백이 호출된 경우 "사용 중"으로 계산하지 **않습니다** .</span><span class="sxs-lookup"><span data-stu-id="89612-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="89612-129">비활성화에 대한 세부 정보를 살펴보기 전에 다음과 같은 용어를 정의하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="89612-130">*스캔 간격*.</span><span class="sxs-lookup"><span data-stu-id="89612-130">*Scan interval*.</span></span> <span data-ttu-id="89612-131">행위자 런타임이 비활성화 및 가비지 수집될 수 있는 행위자에 대해 해당 활성 행위자 테이블을 스캔하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="89612-132">기본값은 1분입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="89612-133">*유휴 시간 제한*.</span><span class="sxs-lookup"><span data-stu-id="89612-133">*Idle timeout*.</span></span> <span data-ttu-id="89612-134">행위자가 비활성화 및 가비지 수집되기 전에 미사용(유휴) 상태를 유지해야 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="89612-135">기본값은 60분입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="89612-136">일반적으로 이 기본값은 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="89612-137">그러나 [행위자 서비스](service-fabric-reliable-actors-platform.md)를 등록할 때 필요한 경우 `ActorServiceSettings`를 통해 이러한 간격을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="89612-138">각 활성 행위자에 대해 행위자 런타임은 유휴 상태였던 시간(사용되지 않은 시간)을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="89612-139">행위자 런타임은 `ScanIntervalInSeconds`마다 각 행위자를 검사하여 가비지 수집 가능한지 확인하고 `IdleTimeoutInSeconds` 동안 유휴 상태였는지 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="89612-140">행위자를 사용할 때마다 유휴 시간이 0으로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="89612-141">이후부터는 `IdleTimeoutInSeconds`동안 다시 유휴 상태인 경우에만 행위자가 가비지 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="89612-142">행위자 인터페이스 메서드 또는 행위자 미리 알림 콜백이 실행되는 경우, 행위자가 사용된 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="89612-143">타이머 콜백이 실행되는 경우 해당 행위자는 사용된 것으로 간주되지 **않습니다** .</span><span class="sxs-lookup"><span data-stu-id="89612-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="89612-144">다음 다이어그램에서는 이러한 개념을 설명하는 단일 행위자의 수명 주기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89612-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![유휴 시간의 예][1]

<span data-ttu-id="89612-146">이 예제에서는 행위자 메서드 호출에 대한 영향 및 이 행위자의 수명에 대한 타이머를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89612-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="89612-147">이 예제에 대해 다음과 같은 사항에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="89612-148">ScanInterval 및 IdleTimeout은 각각 5와 10으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="89612-149">이 예제에서는 개념만 보여 주므로 단위는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="89612-150">스캔 간격이 5로 정의되어 있으므로 가비지 수집할 행위자의 스캔은 T=0,5,10,15,20,25에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="89612-151">주기적 타이머는 T=4,8,12,16,20,24에서 발생하며 해당 콜백이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="89612-152">행위자의 유휴 시간에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="89612-153">행위자는 T=7에서 호출되고 유휴 시간을 0으로 재설정하고 행위자의 가비지 수집을 지연시킵니다.</span><span class="sxs-lookup"><span data-stu-id="89612-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="89612-154">행위자 미리 알림 콜백은 T=14에서 실행되며 추가로 행위자의 가비지 수집이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="89612-155">T=25에서 가비지 수집 스캔이 수행되는 동안, 결국 행위자의 유휴 시간이 10으로 설정된 유휴 시간 제한을 초과하고 행위자는 가비지 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="89612-156">메서드 중 하나를 실행하는 동안에는 해당 메서드를 실행하는 데 소요되는 시간에 상관 없이 행위자는 절대 가비지 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="89612-157">앞서 설명한 대로 행위자 인터페이스 메서드 및 미리 알림 콜백을 실행하면 행위자의 유휴 시간을 0으로 다시 설정하여 가비지 수집을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="89612-158">타이머 콜백 실행의 경우는 유휴 시간이 0으로 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="89612-159">하지만 행위자의 가비지 수집은 타이머 콜백의 실행이 완료될 때까지는 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="89612-160">행위자와 해당 상태 삭제</span><span class="sxs-lookup"><span data-stu-id="89612-160">Deleting actors and their state</span></span>
<span data-ttu-id="89612-161">비활성화된 행위자의 가비지 수집에서는 행위자 개체를 정리하기만 하고 행위자의 상태 관리자에 저장된 데이터를 제거하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="89612-162">행위자가 다시 활성화되면 상태 관리자를 통해 해당 데이터를 다시 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="89612-163">행위자가 상태 관리자에 데이터를 저장하고 비활성화되었지만 다시 활성화되지 않는 경우에는 해당 데이터를 정리해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="89612-164">[행위자 서비스](service-fabric-reliable-actors-platform.md) 에서는 원격 호출자에서 행위자를 삭제하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="89612-165">행위자를 삭제하면 행위자가 현재 활성 상태인지 여부에 따라 다음과 같은 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="89612-166">**활성 행위자**</span><span class="sxs-lookup"><span data-stu-id="89612-166">**Active Actor**</span></span>
  * <span data-ttu-id="89612-167">행위자가 활성 행위자 목록에서 제거되고 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="89612-168">해당 상태가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="89612-169">**비활성 행위자**</span><span class="sxs-lookup"><span data-stu-id="89612-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="89612-170">해당 상태가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="89612-171">행위자는 행위자 메서드 중 하나에서 자체를 삭제하도록 호출할 수 없습니다. 행위자 호출 컨텍스트 내에서 실행되는 동안에는 런타임에서 단일 스레드 액세스를 적용하기 위해 행위자 호출에 대한 잠금을 획득하기 때문에 행위자를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89612-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89612-172">Next steps</span></span>
* [<span data-ttu-id="89612-173">행위자 타이머 및 미리 알림</span><span class="sxs-lookup"><span data-stu-id="89612-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="89612-174">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="89612-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="89612-175">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="89612-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="89612-176">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="89612-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="89612-177">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="89612-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="89612-178">C# 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="89612-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="89612-179">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="89612-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
