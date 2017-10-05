---
title: "행위자 기반 Azure 마이크로 서비스의 이벤트 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors의 이벤트에 대해 소개합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="0390a-103">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="0390a-103">Actor events</span></span>
<span data-ttu-id="0390a-104">행위자 이벤트는 행위자에서 클라이언트로 최상의 알림을 보낼 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="0390a-105">행위자 이벤트는 행위자-클라이언트 간 통신을 위해 디자인되었으며 행위자-행위자 간 통신에는 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="0390a-106">다음 코드 조각에서는 응용 프로그램에서 행위자 이벤트를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="0390a-107">행위자가 게시한 이벤트를 설명하는 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="0390a-108">이 인터페이스는 `IActorEvents` 인터페이스에서 파생되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="0390a-109">메서드의 인수는 [데이터 계약 직렬화 가능](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="0390a-110">이벤트 알림은 단방향으로 최대한 제공되므로 메서드는 void를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="0390a-111">행위자 인터페이스에서 행위자에 의해 게시된 이벤트를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="0390a-112">클라이언트쪽에서는 이벤트 처리기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="0390a-113">클라이언트에서 이벤트를 게시하고 이벤트를 구독하는 행위자에 대한 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="0390a-114">장애 조치 발생 시 행위자는 서로 다른 프로세스 또는 노드로 장애 조치(failover)가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="0390a-115">행위자 프록시는 활성 구독을 관리하고 자동으로 재구독합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="0390a-116">`ActorProxyEventExtensions.SubscribeAsync<TEvent>` API를 통해 재구독 간격을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="0390a-117">구독을 취소하려면 `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="0390a-118">행위자에서 이벤트 발생 시 해당 이벤트를 게시하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="0390a-119">이벤트에 구독자가 여럿 있는 경우는 행위자 런타임에서 구독자들에게 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0390a-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="0390a-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0390a-120">Next steps</span></span>
* [<span data-ttu-id="0390a-121">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="0390a-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="0390a-122">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="0390a-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="0390a-123">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="0390a-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="0390a-124">C# 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="0390a-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0390a-125">C# .NET Core 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="0390a-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="0390a-126">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="0390a-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
