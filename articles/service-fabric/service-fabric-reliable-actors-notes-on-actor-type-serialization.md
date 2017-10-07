---
title: "작업자에 대 한 aaaReliable 행위자 메모 입력 serialization | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors 상태 사용된 toodefine 일 수 있는 직렬화 가능 클래스 및 인터페이스를 정의 하기 위한 기본적인 요구 사항 설명"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>서비스 패브릭 신뢰할 수 있는 행위자 형식 직렬화에 대한 참고 사항
모든 메서드의 hello 인수는 행위자 인터페이스의 각 메서드에 의해 반환 된 hello 작업의 결과 형식 및 행위자의 상태 관리자에 저장 된 개체 여야 [데이터 계약 직렬화 가능](https://msdn.microsoft.com/library/ms731923.aspx)합니다. 이 적용 됩니다. toohello 인수에 정의 된 hello 메서드의 [행위자 이벤트 인터페이스](service-fabric-reliable-actors-events.md)합니다. (행위자 이벤트 인터페이스 메서드는 항상 void를 반환합니다.)

## <a name="custom-data-types"></a>사용자 지정 데이터 형식
이 예에서 행위자 인터페이스 뒤 hello 이라는 사용자 지정 데이터 형식을 반환 하는 메서드를 정의 합니다. `VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

상태 관리자 toostore hello를 사용 하는 행위자가 hello 인터페이스를 구현는 `VoicemailBox` 개체:

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

이 예제에서는 hello `VoicemailBox` 개체가 serialize 되는 경우:

* hello 개체 행위자 인스턴스와 호출자 간에 전송 됩니다.
* hello 개체는 지속형된 toodisk 하 고 복제 tooother 노드 hello 상태 관리자에 저장 됩니다.

hello Reliable Actor framework DataContract serialization을 사용합니다. 따라서 사용자 지정 데이터 개체를 hello 및 해당 멤버 hello로 주석을 달아야 **DataContract** 및 **DataMember** 특성에 각각 있습니다.

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>다음 단계
* [행위자 수명 주기 및 가비지 수집](service-fabric-reliable-actors-lifecycle.md)
* [행위자 타이머 및 미리 알림](service-fabric-reliable-actors-timers-reminders.md)
* [행위자 이벤트](service-fabric-reliable-actors-events.md)
* [행위자 다시 표시](service-fabric-reliable-actors-reentrancy.md)
* [행위자 다형성 및 개체 지향 디자인 패턴](service-fabric-reliable-actors-polymorphism.md)
* [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)
