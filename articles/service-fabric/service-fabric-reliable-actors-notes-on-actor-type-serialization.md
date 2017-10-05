---
title: "행위자 형식 직렬화에 대한 Reliable Actors 참고 사항 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors 상태 및 인터페이스를 정의하는 데 사용될 수 있는 직렬화가 가능 클래스를 정의하기 위한 기본 요구 사항을 설명합니다."
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
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="223cd-103">서비스 패브릭 신뢰할 수 있는 행위자 형식 직렬화에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="223cd-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="223cd-104">모든 메서드의 인수인 행위자 인터페이스의 각 메서드에 의해 반환되는 태스크의 결과 형식 및 행위자의 상태 관리자에 저장된 개체는 [데이터 계약 직렬화가 가능](https://msdn.microsoft.com/library/ms731923.aspx)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="223cd-105">또한 [행위자 이벤트 인터페이스](service-fabric-reliable-actors-events.md)에 정의된 메서드의 인수에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="223cd-106">(행위자 이벤트 인터페이스 메서드는 항상 void를 반환합니다.)</span><span class="sxs-lookup"><span data-stu-id="223cd-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="223cd-107">사용자 지정 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="223cd-107">Custom data types</span></span>
<span data-ttu-id="223cd-108">이 예제에서 다음과 같은 행위자 인터페이스는 `VoicemailBox`이라는 사용자 지정 데이터 형식을 반환하는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="223cd-109">이 인터페이스는 행위자에서 구현되며 이는 상태 관리자를 사용하여 `VoicemailBox` 개체를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="223cd-110">이 예제에서는 다음의 경우 `VoicemailBox` 개체를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="223cd-111">개체는 행위자 인스턴스와 호출자 간에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="223cd-112">개체는 디스크에 유지되고 다른 노드에 복제되는 상태 관리자에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="223cd-113">Reliable Actor 프레임워크는 DataContract 직렬화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="223cd-114">따라서 사용자 지정 데이터 개체와 해당 멤버는 각각 **DataContract** 및 **DataMember** 특성을 사용하여 주석으로 첨부되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="223cd-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="223cd-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="223cd-115">Next steps</span></span>
* [<span data-ttu-id="223cd-116">행위자 수명 주기 및 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="223cd-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="223cd-117">행위자 타이머 및 미리 알림</span><span class="sxs-lookup"><span data-stu-id="223cd-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="223cd-118">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="223cd-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="223cd-119">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="223cd-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="223cd-120">행위자 다형성 및 개체 지향 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="223cd-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="223cd-121">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="223cd-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
