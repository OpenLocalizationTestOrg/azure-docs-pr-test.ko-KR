---
title: "hello Reliable Actors 프레임 워크에서 aaaPolymorphism | Microsoft Docs"
description: ".NET 인터페이스 및 hello Reliable Actors framework tooreuse 기능에에서는 형식 및 API 정의의 계층 구조를 작성 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>다형성 hello Reliable Actors 프레임 워크에서
프레임 워크 있습니다 toobuild 행위자를 사용 하 여 hello Reliable Actors hello 개체 지향 디자인에 사용 되는 방법과 같습니다. 이러한 기술 중 하나는 다형성 인터페이스 tooinherit 두 개에서 및 형식 수 부모를 일반화 합니다. 상속 hello Reliable Actors 프레임 워크에는 일반적으로 몇 가지 추가 제약 조건으로 hello.NET 모델을 따릅니다. Java/Linux의 경우 hello Java 모델을 따릅니다.

## <a name="interfaces"></a>인터페이스
hello Reliable Actors 프레임 워크 필요 toodefine 행위자 형식에서 구현 된 인터페이스를 하나 이상 toobe 합니다. 이 인터페이스는 사용 되는 toogenerate 클라이언트 toocommunicate 프로그램 작업자를 사용할 수 있는 프록시 클래스입니다. 모든 인터페이스가 행위자 형식에 의해 구현되고, 인터페이스의 모든 부모가 궁극적으로 IActor(C#) 또는 Actor(Java)로부터 파생되기만 한다면 인터페이스는 다른 인터페이스에서 상속할 수 있습니다. IActor(C#) 및 Actor(Java)는 hello 플랫폼 정의 된 기본 인터페이스 hello 프레임 워크는.NET 및 Java에 행위자를 위한 각각입니다. 따라서 다음과 같이 셰이프를 사용 하 여 hello 클래식 다형성 예제가 같습니다.

![shape 행위자에 대한 인터페이스 계층 구조][shapes-interface-hierarchy]

## <a name="types"></a>형식
Hello 플랫폼에서 제공 되는 hello 기본 행위자 클래스에서 파생 되는 행위자 형식 계층 구조를 만들 수 있습니다. 도형의 hello 경우, 기본 해야 할 수 있습니다 `Shape`(C#) 또는 `ShapeImpl`(Java) 형식:

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

하위 유형 `Shape`(C#) 또는 `ShapeImpl`(Java) hello 기본 메서드를 재정의할 수 있습니다.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

참고 hello `ActorService` hello 행위자 형식에는 특성입니다. 이 특성은이 유형의 행위자 호스트용 서비스를 자동으로 만들도록 hello Reliable Actor 프레임 워크를 알려 줍니다. 일부 경우에만 하위 종류와 기능을 공유 하는 데 사용 되는 기본 형식 toocreate 수도 및 될 수 없으므로 사용 하는 tooinstantiate 구체적인 행위자입니다. 이 경우 hello를 사용 해야 `abstract` 키워드 tooindicate 해당 형식에 기반 하는 행위자 만들 하지 않습니다.

## <a name="next-steps"></a>다음 단계
* 참조 [hello Reliable Actors 프레임 워크 hello 서비스 패브릭 플랫폼을 활용 하는 방법을](service-fabric-reliable-actors-platform.md) tooprovide 안정성, 확장성 및 일관 된 상태입니다.
* Hello에 대 한 자세한 내용은 [행위자 수명 주기](service-fabric-reliable-actors-lifecycle.md)합니다.

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
