---
title: "Reliable Actors 타이머 및 미리 알림 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors의 타이머 및 미리 알림에 대해 소개합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="3e1b7-103">행위자 타이머 및 미리 알림</span><span class="sxs-lookup"><span data-stu-id="3e1b7-103">Actor timers and reminders</span></span>
<span data-ttu-id="3e1b7-104">행위자는 타이머 또는 미리 알림을 등록하여 정기적인 작업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="3e1b7-105">이 문서에서는 타이머와 미리 알림을 사용하는 방법을 보여 주고 둘 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="3e1b7-106">행위자 타이머</span><span class="sxs-lookup"><span data-stu-id="3e1b7-106">Actor timers</span></span>
<span data-ttu-id="3e1b7-107">행위자 타이머는 콜백 메서드가 행위자 런타임에서 제공하는 턴 기반 동시성 보증을 준수하는 .NET 또는 Java 타이머에 대한 간단한 래퍼를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="3e1b7-108">행위자는 기본 클래스에서 `RegisterTimer`(C#) 또는 `registerTimer`(Java) 및 `UnregisterTimer`(C#) 또는 `unregisterTimer`(Java) 메서드를 사용하여 해당 타이머를 등록 및 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="3e1b7-109">아래 예제에서는 타이머 API의 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="3e1b7-110">API는 .NET 타이머 또는 Java 타이머와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="3e1b7-111">이 예제의 경우 타이머가 만료되면 행위자 런타임에서는 `MoveObject`(C#) 또는 `moveObject`(Java) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="3e1b7-112">메서드는 턴 기반 동시성을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="3e1b7-113">즉, 다른 행위자 메서드나 타이머/미리 알림 콜백은 이 콜백의 실행이 완료될 때까지 진행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="3e1b7-114">다음 타이머 시간 간격은 콜백 실행이 완료된 후 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="3e1b7-115">이는 타이머 콜백이 실행되는 동안 타이머는 중지되고 콜백이 완료되면 시작된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="3e1b7-116">행위자 런타임은 콜백이 완료되면 행위자의 상태 관리자에 대한 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="3e1b7-117">상태를 저장하는 중에 오류가 발생하는 경우 해당 행위자 개체는 비활성화되고 새 인스턴스가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3e1b7-118">행위자가 가비지 수집의 일환으로 비활성화되면 모든 타이머가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="3e1b7-119">그다음 타이머 콜백이 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="3e1b7-120">또한 행위자 런타임은 비활성화 전에 실행 중이었던 타이머에 대한 정보를 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="3e1b7-121">나중에 다시 활성화될 때 필요한 모든 타이머를 등록하는 것은 행위자의 일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="3e1b7-122">자세한 내용은 [행위자 가비지 수집](service-fabric-reliable-actors-lifecycle.md)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="3e1b7-123">행위자 미리 알림</span><span class="sxs-lookup"><span data-stu-id="3e1b7-123">Actor reminders</span></span>
<span data-ttu-id="3e1b7-124">미리 알림은 행위자에서 지정된 시간에 영구 콜백을 트리거하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="3e1b7-125">기능은 타이머와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="3e1b7-126">하지만 타이머와 달리 미리 알림은 행위자가 명시적으로 등록을 취소하거나 행위자가 명시적으로 삭제할 때까지 모든 상황에서 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="3e1b7-127">구체적으로, 미리 알림은 행위자 런타임이 행위자의 미리 알림에 대한 정보를 유지하므로 행위자 비활성화 및 장애 조치를 통해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="3e1b7-128">미리 알림을 등록하기 위해서는 행위자가 기본 클래스에서 제공된 `RegisterReminderAsync` 메서드를 아래 예제와 같이 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="3e1b7-129">이 예제에서 `"Pay cell phone bill"` 은 미리 알림 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="3e1b7-130">행위자가 미리 알림을 고유하게 식별하는 데 사용하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="3e1b7-131">`BitConverter.GetBytes(amountInDollars)`(C#)는 해당 미리 알림에 연결되는 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="3e1b7-132">또한 이 값은 미리 알림 콜백의 인수(`IRemindable.ReceiveReminderAsync`(C#) 또는 `Remindable.receiveReminderAsync`(Java))로 행위자에게 다시 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="3e1b7-133">미리 알림을 사용하는 행위자는 아래 예제에 나온 대로 `IRemindable` 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="3e1b7-134">미리 알림이 트리거되면 Reliable Actors 런타임에서 행위자에 대해 `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="3e1b7-135">행위자는 미리 알림을 여러 개 등록할 수 있으며 `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 메서드는 이러한 미리 알림 중 하나가 트리거되면 언제든지 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="3e1b7-136">행위자는 `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 메서드로 전달되는 미리 알림 이름을 사용하여 미리 알림이 트리거되었는지 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="3e1b7-137">행위자 런타임은 `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 호출이 완료되면 행위자의 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="3e1b7-138">상태를 저장하는 중에 오류가 발생하는 경우 해당 행위자 개체는 비활성화되고 새 인스턴스가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3e1b7-139">미리 알림을 등록 취소하려면 행위자가 아래 예제에 나온 대로 `UnregisterReminderAsync`(C#) 또는 `unregisterReminderAsync`(Java) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="3e1b7-140">위의 그림과 같이 `UnregisterReminderAsync`(C#) 또는 `unregisterReminderAsync`(Java) 메서드는 `IActorReminder`(C#) 또는 `ActorReminder`(Java) 인터페이스를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="3e1b7-141">행위자 기본 클래스는 미리 알림 이름에 전달하여 `IActorReminder`(C#) 또는 `ActorReminder`(Java) 인터페이스를 검색하는 데 사용할 수 있는 `GetReminder`(C#) 또는 `getReminder`(Java) 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="3e1b7-142">이 방법은 행위자가 `RegisterReminder`(C#) 또는 `registerReminder`(Java) 메서드 호출에서 반환된 `IActorReminder`(C#) 또는 `ActorReminder`(Java) 인터페이스를 유지할 필요가 없기 때문에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e1b7-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e1b7-143">Next Steps</span></span>
<span data-ttu-id="3e1b7-144">Reliable Actor 이벤트 및 재진입에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e1b7-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="3e1b7-145">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="3e1b7-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="3e1b7-146">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="3e1b7-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
