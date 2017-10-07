---
title: "Azure microservices 행위자 기반 수명 주기의 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="88096-103">행위자 수명 주기, 자동 가비지 수집 및 수동 삭제</span><span class="sxs-lookup"><span data-stu-id="88096-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="88096-104">행위자가 활성화 hello 처음으로 tooany 메서드 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="88096-105">행위자 비활성화 (가비지 수집된 hello 행위자 런타임에서) 이면 구성 가능한 일정 시간 동안에는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="88096-106">행위자와 그 상태를 언제든지 수동으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="88096-107">행위자 활성화</span><span class="sxs-lookup"><span data-stu-id="88096-107">Actor activation</span></span>
<span data-ttu-id="88096-108">행위자가 활성화 hello 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="88096-109">행위자를 호출하는 경우 아직 활성화되지 않았으면 새 행위자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="88096-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="88096-110">상태를 유지 하는 경우 hello 행위자의 상태가 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="88096-111">hello `OnActivateAsync` (C#) 또는 `onActivateAsync` (있음 hello 행위자 구현에서 재정의할 수 있음) (Java) 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="88096-112">이제 hello 행위자 활성 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="88096-113">행위자 비활성화</span><span class="sxs-lookup"><span data-stu-id="88096-113">Actor deactivation</span></span>
<span data-ttu-id="88096-114">행위자 비활성화 되 면 hello 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="88096-115">행위자 일정 기간을 사용 하지 않으면 hello 활성 작업자 테이블에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="88096-116">hello `OnDeactivateAsync` (C#) 또는 `onDeactivateAsync` (있음 hello 행위자 구현에서 재정의할 수 있음) (Java) 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="88096-117">Hello 작업자에 대해 모든 hello 타이머를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="88096-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="88096-118">상태 변경과 같은 행위자 작업은 이 메서드에서 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="88096-119">hello 패브릭 행위자 런타임에서 내보내는 일부 [tooactor 활성화 및 비활성화와 관련 된 이벤트](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="88096-120">진단 및 성능 모니터링에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="88096-121">행위자 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="88096-121">Actor garbage collection</span></span>
<span data-ttu-id="88096-122">행위자 비활성화 되 면 toohello 행위자 개체를 참조 해제 되 고 hello 공용 언어 런타임 (CLR) 또는 java 가상 컴퓨터 (JVM) 가비지 수집기에서 일반적으로 수집 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="88096-123">가비지 수집만 hello 행위자 개체를 정리 그렇게 **하지** hello 행위자 상태 관리자에 저장 된 상태가 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="88096-124">hello 다음 시간 hello 행위자가 활성화 하 고 새 행위자 개체를 만드는 상태로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="88096-125">"사용"을 비활성화 및 가비지 수집 hello 목적으로 계산 하는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="88096-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="88096-126">호출 수신</span><span class="sxs-lookup"><span data-stu-id="88096-126">Receiving a call</span></span>
* <span data-ttu-id="88096-127">`IRemindable.ReceiveReminderAsync`메서드 호출 (hello 행위자 미리 알림을 사용 하는 경우에 해당)</span><span class="sxs-lookup"><span data-stu-id="88096-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="88096-128">hello 행위자 타이머를 사용 하 여 해당 타이머 콜백이 호출 되는 경우 그렇게 **하지** "사용"로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="88096-129">비활성화의 hello 자세히 살펴보기 전에 것이 중요 한 toodefine hello 아래 계약 내용:</span><span class="sxs-lookup"><span data-stu-id="88096-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="88096-130">*스캔 간격*.</span><span class="sxs-lookup"><span data-stu-id="88096-130">*Scan interval*.</span></span> <span data-ttu-id="88096-131">이 hello 행위자에서 런타임 비활성화 될 수 있는 작업자에 대 한 해당 활성 작업자 테이블을 검색 하는 hello 간격 이므로 가비지가 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="88096-132">이 대 한 hello 기본값은 1 분입니다.</span><span class="sxs-lookup"><span data-stu-id="88096-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="88096-133">*유휴 시간 제한*.</span><span class="sxs-lookup"><span data-stu-id="88096-133">*Idle timeout*.</span></span> <span data-ttu-id="88096-134">이 hello 시간 행위자 필요 함을 tooremain 사용 되지 않는 가비지가 수집 하 고 비활성화할 수 있습니다 (유휴 상태).</span><span class="sxs-lookup"><span data-stu-id="88096-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="88096-135">이 대 한 hello 기본값은 60 분입니다.</span><span class="sxs-lookup"><span data-stu-id="88096-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="88096-136">일반적으로 불필요 toochange이이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="88096-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="88096-137">그러나 [행위자 서비스](service-fabric-reliable-actors-platform.md)를 등록할 때 필요한 경우 `ActorServiceSettings`를 통해 이러한 간격을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="88096-138">각 활성 작업자에 대해 hello 행위자 런타임은 hello 총 시간이 경과 했는데도 문제가 있다면 유휴 상태 (사용 되지 않은)의 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="88096-139">hello 행위자 런타임 검사 각각 hello 행위자의 모든 `ScanIntervalInSeconds` 가비지 수 있으면 toosee 수집 하 고 경우에 대 한 유휴 상태 수집 `IdleTimeoutInSeconds`합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="88096-140">행위자 사용 하는 경우 언제 든 지 고 유휴 시간 재설정 too0입니다.</span><span class="sxs-lookup"><span data-stu-id="88096-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="88096-141">그러면 hello 행위자 다시 유휴 상태로 대기에 대 한 경우에 가비지 수집 될 수 있습니다 `IdleTimeoutInSeconds`합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="88096-142">행위자 toohave 것으로 간주 됩니다 회수 된 행위자 인터페이스 메서드 또는 행위자 미리 알림 콜백이 실행 되는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="88096-143">자가 **하지** toohave 것으로 간주 되어 해당 타이머 콜백이 실행 되는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="88096-144">hello 다음 다이어그램에서는 단일 행위자 tooillustrate의 hello 수명 주기 이러한 개념</span><span class="sxs-lookup"><span data-stu-id="88096-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![유휴 시간의 예][1]

<span data-ttu-id="88096-146">hello 예제에는이 행위자의 lifetime hello에 행위자 메서드 호출, 알림과 타이머의 hello 영향을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88096-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="88096-147">hello hello 예에 대 한 포인트 다음은 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="88096-148">ScanInterval 및 IdleTimeout too5 및 10는 각각 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="88096-149">(단위 않습니다 중요 하지 여기에서는 이러한 목적에만 tooillustrate hello 개념 이므로.)</span><span class="sxs-lookup"><span data-stu-id="88096-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="88096-150">hello 검색 간격을 5에 정의 된 대로 toobe 가비지 수집 T = 0, 5, 10, 15, 20, 25에서 발생 하는 행위자를 위한 hello 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="88096-151">주기적 타이머는 T=4,8,12,16,20,24에서 발생하며 해당 콜백이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="88096-152">Hello hello 행위자의 유휴 시간을 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="88096-153">T = 7에는 행위자 메서드 호출 hello 유휴 시간 too0을 hello 행위자의 hello 가비지 컬렉션을 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="88096-154">T = 14에서 행위자 미리 알림 콜백을 실행 하 고 추가 지연이 hello hello 행위자의 가비지 수집 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="88096-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="88096-155">T = 25 hello 가비지 컬렉션 검사 수행 hello 행위자의 유휴 시간은 마지막으로 10 hello 유휴 시간 제한을 초과 하 고 hello 행위자가 가비지 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="88096-156">메서드 중 하나를 실행하는 동안에는 해당 메서드를 실행하는 데 소요되는 시간에 상관 없이 행위자는 절대 가비지 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="88096-157">앞서 언급 했 듯이 행위자 인터페이스 메서드 및 미리 알림 콜백을 실행 hello hello 행위자의 유휴 시간 too0 다시 설정 하 여 가비지 수집을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="88096-158">타이머 콜백 실행 hello hello 유휴 시간 too0를 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="88096-159">그러나 hello 행위자의 가비지 수집을 hello hello 타이머 콜백을 실행이 완료 될 때까지 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="88096-160">행위자와 해당 상태 삭제</span><span class="sxs-lookup"><span data-stu-id="88096-160">Deleting actors and their state</span></span>
<span data-ttu-id="88096-161">비활성화 된 작업자의 가비지 수집만 hello 행위자 개체를 정리 하지만 행위자의 상태 관리자에 저장 된 데이터는 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="88096-162">행위자 다시 활성화 되 면 해당 데이터 hello 상태 관리자를 통해 사용할 수 있는 tooit은 다시 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="88096-163">여기서 행위자 상태 관리자에 데이터를 저장 하 고 비활성화 있지만 되지 다시 활성화의 경우에서 해당 데이터를 필요한 tooclean 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="88096-164">hello [행위자 서비스](service-fabric-reliable-actors-platform.md) 원격 호출자에서 작업자를 삭제 하기 위한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="88096-165">작업자 삭제 효과 hello 행위자 현재 활성 인지 아닌지에 따라 다음 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88096-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="88096-166">**활성 행위자**</span><span class="sxs-lookup"><span data-stu-id="88096-166">**Active Actor**</span></span>
  * <span data-ttu-id="88096-167">행위자가 활성 행위자 목록에서 제거되고 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="88096-168">해당 상태가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="88096-169">**비활성 행위자**</span><span class="sxs-lookup"><span data-stu-id="88096-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="88096-170">해당 상태가 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="88096-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="88096-171">행위자를 호출할 수 없습니다는 런타임은 hello 행위자 호출 tooenforce 단일 스레드 액세스 잠금을 hello에서 확보 하는 행위자 호출 컨텍스트 내에서 실행 하는 동안 hello 행위자를 삭제할 수 없으므로 행위자 메서드 중 하나에서 자체에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="88096-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88096-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88096-172">Next steps</span></span>
* [<span data-ttu-id="88096-173">행위자 타이머 및 미리 알림</span><span class="sxs-lookup"><span data-stu-id="88096-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="88096-174">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="88096-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="88096-175">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="88096-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="88096-176">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="88096-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="88096-177">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="88096-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="88096-178">C# 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="88096-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="88096-179">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="88096-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
