---
title: "Azure microservices 행위자 기반에서 aaaEvents | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors에 대 한 tooevents를 소개 합니다."
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="c11ff-103">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="c11ff-103">Actor events</span></span>
<span data-ttu-id="c11ff-104">행위자 이벤트 hello 행위자 toohello 클라이언트로부터 방법을 toosend 최상의 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="c11ff-105">행위자 이벤트는 행위자-클라이언트 간 통신을 위해 디자인되었으며 행위자-행위자 간 통신에는 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="c11ff-106">hello 다음 코드 조각 표시 방법을 응용 프로그램의 toouse 행위자 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="c11ff-107">Hello 행위자가 게시 하는 hello 이벤트에 설명 하는 인터페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="c11ff-108">이 인터페이스는 hello에서 파생 되어야 합니다 `IActorEvents` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="c11ff-109">hello 메서드의 hello 인수 여야 [데이터 계약 직렬화 가능](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="c11ff-110">hello 메서드는 void를 반환 해야, 이벤트로 알림은 단방향 및 최상의 노력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="c11ff-111">Hello 행위자 hello 행위자 인터페이스에 의해 게시 된 hello 이벤트를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="c11ff-112">Hello 클라이언트 쪽에서 hello 이벤트 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="c11ff-113">Hello 클라이언트 hello 이벤트를 게시 하는 프록시 toohello 행위자 만들고 tooits 이벤트를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="c11ff-114">장애 조치의 hello 이벤트에서 hello 행위자 tooa 다른 프로세스 또는 노드를 통해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="c11ff-115">hello 행위자 프록시 hello 활성 구독을 관리 하 고 자동으로 다시 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="c11ff-116">Hello 통해 hello 다시 구독 간격을 제어할 수 있습니다 `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API입니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="c11ff-117">toounsubscribe를 사용 하 여 hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API입니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="c11ff-118">Hello 행위자에서 발생할 때마다 hello 이벤트를 게시 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="c11ff-119">구독자 toohello 이벤트 인 경우 hello 행위자 런타임은 해당 hello 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c11ff-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="c11ff-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c11ff-120">Next steps</span></span>
* [<span data-ttu-id="c11ff-121">행위자 다시 표시</span><span class="sxs-lookup"><span data-stu-id="c11ff-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="c11ff-122">행위자 진단 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="c11ff-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="c11ff-123">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="c11ff-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="c11ff-124">C# 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="c11ff-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="c11ff-125">C# .NET Core 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="c11ff-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="c11ff-126">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="c11ff-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
