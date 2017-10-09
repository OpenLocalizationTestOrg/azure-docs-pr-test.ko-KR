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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="6b9a6-103">다형성 hello Reliable Actors 프레임 워크에서</span><span class="sxs-lookup"><span data-stu-id="6b9a6-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="6b9a6-104">프레임 워크 있습니다 toobuild 행위자를 사용 하 여 hello Reliable Actors hello 개체 지향 디자인에 사용 되는 방법과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="6b9a6-105">이러한 기술 중 하나는 다형성 인터페이스 tooinherit 두 개에서 및 형식 수 부모를 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="6b9a6-106">상속 hello Reliable Actors 프레임 워크에는 일반적으로 몇 가지 추가 제약 조건으로 hello.NET 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="6b9a6-107">Java/Linux의 경우 hello Java 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="6b9a6-108">인터페이스</span><span class="sxs-lookup"><span data-stu-id="6b9a6-108">Interfaces</span></span>
<span data-ttu-id="6b9a6-109">hello Reliable Actors 프레임 워크 필요 toodefine 행위자 형식에서 구현 된 인터페이스를 하나 이상 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="6b9a6-110">이 인터페이스는 사용 되는 toogenerate 클라이언트 toocommunicate 프로그램 작업자를 사용할 수 있는 프록시 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="6b9a6-111">모든 인터페이스가 행위자 형식에 의해 구현되고, 인터페이스의 모든 부모가 궁극적으로 IActor(C#) 또는 Actor(Java)로부터 파생되기만 한다면 인터페이스는 다른 인터페이스에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="6b9a6-112">IActor(C#) 및 Actor(Java)는 hello 플랫폼 정의 된 기본 인터페이스 hello 프레임 워크는.NET 및 Java에 행위자를 위한 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="6b9a6-113">따라서 다음과 같이 셰이프를 사용 하 여 hello 클래식 다형성 예제가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![shape 행위자에 대한 인터페이스 계층 구조][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="6b9a6-115">형식</span><span class="sxs-lookup"><span data-stu-id="6b9a6-115">Types</span></span>
<span data-ttu-id="6b9a6-116">Hello 플랫폼에서 제공 되는 hello 기본 행위자 클래스에서 파생 되는 행위자 형식 계층 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="6b9a6-117">도형의 hello 경우, 기본 해야 할 수 있습니다 `Shape`(C#) 또는 `ShapeImpl`(Java) 형식:</span><span class="sxs-lookup"><span data-stu-id="6b9a6-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="6b9a6-118">하위 유형 `Shape`(C#) 또는 `ShapeImpl`(Java) hello 기본 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="6b9a6-119">참고 hello `ActorService` hello 행위자 형식에는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="6b9a6-120">이 특성은이 유형의 행위자 호스트용 서비스를 자동으로 만들도록 hello Reliable Actor 프레임 워크를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="6b9a6-121">일부 경우에만 하위 종류와 기능을 공유 하는 데 사용 되는 기본 형식 toocreate 수도 및 될 수 없으므로 사용 하는 tooinstantiate 구체적인 행위자입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="6b9a6-122">이 경우 hello를 사용 해야 `abstract` 키워드 tooindicate 해당 형식에 기반 하는 행위자 만들 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b9a6-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b9a6-123">Next steps</span></span>
* <span data-ttu-id="6b9a6-124">참조 [hello Reliable Actors 프레임 워크 hello 서비스 패브릭 플랫폼을 활용 하는 방법을](service-fabric-reliable-actors-platform.md) tooprovide 안정성, 확장성 및 일관 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="6b9a6-125">Hello에 대 한 자세한 내용은 [행위자 수명 주기](service-fabric-reliable-actors-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9a6-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
