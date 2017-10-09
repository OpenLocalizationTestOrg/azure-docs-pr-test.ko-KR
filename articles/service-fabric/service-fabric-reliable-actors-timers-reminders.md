---
title: "행위자 aaaReliable 타이머 및 미리 알림을 | Microsoft Docs"
description: "소개 tootimers 및 서비스 패브릭 Reliable Actors에 대 한 미리 알림입니다."
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
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a>행위자 타이머 및 미리 알림
행위자는 타이머 또는 미리 알림을 등록하여 정기적인 작업을 예약할 수 있습니다. 이 문서에서는 어떻게 toouse 타이머 및 미리 알림을 hello 그 차이 설명 합니다.

## <a name="actor-timers"></a>행위자 타이머
행위자 타이머 hello 콜백 메서드 런타임에서 제공 하는 행위자 hello hello 턴 기반 동시성 보장을 준수 한 간단한.NET 또는 Java 타이머 tooensure 래퍼를 제공 합니다.

행위자 hello צ ְ ײ `RegisterTimer`(C#) 또는 `registerTimer`(Java) 및 `UnregisterTimer`(C#) 또는 `unregisterTimer`(Java) 기반에 tooregister 클래스 메서드와 타이머가 등록을 취소 합니다. 다음 예제에서는 hello 타이머 Api hello 사용을 보여 줍니다. hello Api는 매우 유사한 toohello.NET 타이머 또는 Java 타이머입니다. 이 예제에서는 hello 타이머 원인인 hello 행위자 런타임 됩니다 호출 hello `MoveObject`(C#) 또는 `moveObject`메서드 (Java 참조). hello 메서드 toorespect hello 턴 기반 동시성을 보장 됩니다. 즉, 다른 행위자 메서드나 타이머/미리 알림 콜백은 이 콜백의 실행이 완료될 때까지 진행되어야 합니다.

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
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

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
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
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

hello는 hello 타이머의 다음 기간 hello 콜백 실행이 완료 한 후 시작 합니다. 이 hello 콜백이 실행 되 고 hello 콜백이 완료 될 때 시작 되는 동안 해당 hello 타이머가 중지 된 것을 의미 합니다.

hello 행위자 런타임 hello 콜백이 완료 될 때 변경 toohello 행위자 상태 관리자를 저장 합니다. Hello 상태를 저장 하는 중 오류가 발생 하는 경우 해당 행위자 개체가 비활성화 하 고 새 인스턴스를 활성화 됩니다.

가비지 수집의 일환으로 hello 행위자 비활성화 될 때 모든 타이머가 중지 됩니다. 그다음 타이머 콜백이 호출되지 않습니다. 또한 hello 행위자 런타임 비활성화 하기 전에 실행 중이 던 hello 타이머에 대 한 정보를 유지 하지 않습니다. 가 toohello 행위자 tooregister hello 나중에 다시 활성화 될 때 필요한 모든 타이머 합니다. 자세한 내용은 hello 섹션을 참조 [행위자 가비지 수집](service-fabric-reliable-actors-lifecycle.md)합니다.

## <a name="actor-reminders"></a>행위자 미리 알림
미리 알림은 메커니즘 tootrigger 영구 콜백을에 행위자에 지정 된 시간입니다. 메서드에 비슷한 tootimers 합니다. 하지만 타이머와는 달리 알림 트리거되는 모든 상황에서 hello 행위자에서 명시적으로 등록 취소 하거나 hello 행위자 명시적으로 삭제 될 때까지 합니다. 특히, hello 행위자 런타임 hello 행위자 미리 알림 방법에 대 한 정보를 유지 합니다. 미리 알림 행위자 deactivations 및 장애 조치에서 유발 됩니다.

미리 알림 tooregister 행위자 호출 hello `RegisterReminderAsync` hello 다음 예제와 같이 hello 기본 클래스에서 제공 하는 메서드:

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
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

이 예제에서는 `"Pay cell phone bill"` hello 미리 알림 이름입니다. 이 hello 행위자 사용 하는 문자열 toouniquely 미리 알림을 식별 합니다. `BitConverter.GetBytes(amountInDollars)`(C#)는 hello 미리 알림 연관 된 hello 컨텍스트입니다. 전달 됩니다 백 toohello 행위자 인수 toohello 미리 알림 콜백을으로, 즉 `IRemindable.ReceiveReminderAsync`(C#) 또는 `Remindable.receiveReminderAsync`(Java 참조).

미리 알림을 사용 하는 행위자 hello를 구현 해야 `IRemindable` 아래 hello 예에 나와 있는 것 처럼 인터페이스입니다.

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

Hello Reliable Actors 런타임에서 hello는 호출 하 고, 미리 알림이 트리거될 때 `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`hello 행위자 메서드 (Java 참조). 행위자 미리 알림을 여러 개를 등록 하 고 hello `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 메서드를 호출 중 이러한 미리 알림 트리거될 때. hello 행위자 toohello에 전달 되는 hello 미리 알림 이름은 צ ְ ײ `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 메서드 toofigure는 미리 알림 트리거 되었습니다.

hello 행위자 런타임 상태를 저장 hello 행위자 때 hello `ReceiveReminderAsync`(C#) 또는 `receiveReminderAsync`(Java) 호출을 완료 합니다. Hello 상태를 저장 하는 중 오류가 발생 하는 경우 해당 행위자 개체가 비활성화 하 고 새 인스턴스를 활성화 됩니다.

미리 알림 toounregister 행위자 호출 hello `UnregisterReminderAsync`(C#) 또는 `unregisterReminderAsync`(Java) 메서드를 다음 hello 예에 나와 있는 것 처럼 합니다.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

위와 같이 hello `UnregisterReminderAsync`(C#) 또는 `unregisterReminderAsync`(Java) 메서드에 `IActorReminder`(C#) 또는 `ActorReminder`(Java) 인터페이스입니다. 작업 자가 기본 클래스에서는 hello는 `GetReminder`(C#) 또는 `getReminder`(Java) 메서드 사용된 tooretrieve hello 일 수 있는 `IActorReminder`(C#) 또는 `ActorReminder`hello 미리 알림 이름 전달 하 여 (Java) 인터페이스입니다. Hello 행위자 toopersist hello 않아도 때문에이 방법은 편리 `IActorReminder`(C#) 또는 `ActorReminder`hello에서 반환 된 (Java) 인터페이스 `RegisterReminder`(C#) 또는 `registerReminder`(Java) 메서드를 호출 합니다.

## <a name="next-steps"></a>다음 단계
Reliable Actor 이벤트 및 재진입에 대해 알아봅니다.
* [행위자 이벤트](service-fabric-reliable-actors-events.md)
* [행위자 다시 표시](service-fabric-reliable-actors-reentrancy.md)
