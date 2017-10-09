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
# <a name="actor-events"></a>행위자 이벤트
행위자 이벤트 hello 행위자 toohello 클라이언트로부터 방법을 toosend 최상의 알림을 제공합니다. 행위자 이벤트는 행위자-클라이언트 간 통신을 위해 디자인되었으며 행위자-행위자 간 통신에는 사용하지 않아야 합니다.

hello 다음 코드 조각 표시 방법을 응용 프로그램의 toouse 행위자 이벤트입니다.

Hello 행위자가 게시 하는 hello 이벤트에 설명 하는 인터페이스를 정의 합니다. 이 인터페이스는 hello에서 파생 되어야 합니다 `IActorEvents` 인터페이스입니다. hello 메서드의 hello 인수 여야 [데이터 계약 직렬화 가능](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)합니다. hello 메서드는 void를 반환 해야, 이벤트로 알림은 단방향 및 최상의 노력 합니다.

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
Hello 행위자 hello 행위자 인터페이스에 의해 게시 된 hello 이벤트를 선언 합니다.

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
Hello 클라이언트 쪽에서 hello 이벤트 처리기를 구현 합니다.

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

Hello 클라이언트 hello 이벤트를 게시 하는 프록시 toohello 행위자 만들고 tooits 이벤트를 구독 합니다.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

장애 조치의 hello 이벤트에서 hello 행위자 tooa 다른 프로세스 또는 노드를 통해 실패할 수 있습니다. hello 행위자 프록시 hello 활성 구독을 관리 하 고 자동으로 다시 구독 합니다. Hello 통해 hello 다시 구독 간격을 제어할 수 있습니다 `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API입니다. toounsubscribe를 사용 하 여 hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API입니다.

Hello 행위자에서 발생할 때마다 hello 이벤트를 게시 하기만 하면 됩니다. 구독자 toohello 이벤트 인 경우 hello 행위자 런타임은 해당 hello 알림을 보냅니다.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>다음 단계
* [행위자 다시 표시](service-fabric-reliable-actors-reentrancy.md)
* [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)
* [행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# 샘플 코드](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [C# .NET Core 샘플 코드](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Java 샘플 코드](http://github.com/Azure-Samples/service-fabric-java-getting-started)
