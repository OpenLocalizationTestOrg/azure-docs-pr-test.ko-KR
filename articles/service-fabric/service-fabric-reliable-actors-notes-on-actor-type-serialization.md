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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="f8320-103">서비스 패브릭 신뢰할 수 있는 행위자 형식 직렬화에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="f8320-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="f8320-104">모든 메서드의 hello 인수는 행위자 인터페이스의 각 메서드에 의해 반환 된 hello 작업의 결과 형식 및 행위자의 상태 관리자에 저장 된 개체 여야 [데이터 계약 직렬화 가능](https://msdn.microsoft.com/library/ms731923.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="f8320-105">이 적용 됩니다. toohello 인수에 정의 된 hello 메서드의 [행위자 이벤트 인터페이스](service-fabric-reliable-actors-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="f8320-106">(행위자 이벤트 인터페이스 메서드는 항상 void를 반환합니다.)</span><span class="sxs-lookup"><span data-stu-id="f8320-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="f8320-107">사용자 지정 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="f8320-107">Custom data types</span></span>
<span data-ttu-id="f8320-108">이 예에서 행위자 인터페이스 뒤 hello 이라는 사용자 지정 데이터 형식을 반환 하는 메서드를 정의 합니다. `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="f8320-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="f8320-109">상태 관리자 toostore hello를 사용 하는 행위자가 hello 인터페이스를 구현는 `VoicemailBox` 개체:</span><span class="sxs-lookup"><span data-stu-id="f8320-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="f8320-110">이 예제에서는 hello `VoicemailBox` 개체가 serialize 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="f8320-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="f8320-111">hello 개체 행위자 인스턴스와 호출자 간에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="f8320-112">hello 개체는 지속형된 toodisk 하 고 복제 tooother 노드 hello 상태 관리자에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="f8320-113">hello Reliable Actor framework DataContract serialization을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="f8320-114">따라서 사용자 지정 데이터 개체를 hello 및 해당 멤버 hello로 주석을 달아야 **DataContract** 및 **DataMember** 특성에 각각 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8320-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f8320-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8320-115">Next steps</span></span>
* [<span data-ttu-id="f8320-116">행위자 수명 주기 및 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="f8320-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="f8320-117">행위자 타이머 및 미리 알림</span><span class="sxs-lookup"><span data-stu-id="f8320-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="f8320-118">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="f8320-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="f8320-119">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="f8320-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="f8320-120">행위자 다형성 및 개체 지향 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="f8320-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="f8320-121">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="f8320-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
