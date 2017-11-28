---
title: "Reliable Actors 프레임워크의 다형성 | Microsoft Docs"
description: "Reliable Actors 프레임워크에서 .NET 인터페이스 및 형식의 계층 구조를 구축하여 기능 및 API 정의를 다시 사용합니다."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="68e06-103">Reliable Actors 프레임워크의 다형성</span><span class="sxs-lookup"><span data-stu-id="68e06-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="68e06-104">Reliable Actors 프레임워크를 사용하면 개체 지향 디자인에 사용하는 동일한 기술을 대부분 사용하여 행위자를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="68e06-105">이러한 다형성 기술 중 하나는 보다 일반화된 부모로부터 형식과 인터페이스를 상속하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="68e06-106">Reliable Actors 프레임워크의 상속은 일반적으로 몇 가지 추가적인 제약 조건과 함께 .NET 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="68e06-107">Java/Linux의 경우 Java 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="68e06-108">인터페이스</span><span class="sxs-lookup"><span data-stu-id="68e06-108">Interfaces</span></span>
<span data-ttu-id="68e06-109">Reliable Actors 프레임워크에서는 행위자 형식으로 구현될 인터페이스를 하나 이상 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="68e06-110">이 인터페이스는 클라이언트가 행위자와의 통신에 사용할 수 있는 프록시 클래스를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="68e06-111">모든 인터페이스가 행위자 형식에 의해 구현되고, 인터페이스의 모든 부모가 궁극적으로 IActor(C#) 또는 Actor(Java)로부터 파생되기만 한다면 인터페이스는 다른 인터페이스에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="68e06-112">IActor(C#) 및 Actor(Java)는 .NET 및 Java Framework에서 행위자에 대한 플랫폼 정의 기본 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="68e06-113">도형을 사용한 전형적인 다형성의 예는 다음과 유사한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![shape 행위자에 대한 인터페이스 계층 구조][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="68e06-115">형식</span><span class="sxs-lookup"><span data-stu-id="68e06-115">Types</span></span>
<span data-ttu-id="68e06-116">플랫폼에 제공되는 기본 Actor 클래스에서 파생되는 행위자 형식 계층 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="68e06-117">도형의 경우 상태 기본 `Shape`(C#) 또는 `ShapeImpl`(Java) 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="68e06-118">`Shape`(C#) 또는 `ShapeImpl`(Java)의 하위 형식은 기본부터 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="68e06-119">행위자 형식의 `ActorService` 특성에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="68e06-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="68e06-120">이 특성은 Reliable Actor 프레임워크가 이런 형식의 행위자를 호스팅하기 위해 서비스를 자동으로 생성하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="68e06-121">경우에 따라서 하위 형식과 기능을 공유하는 것만을 목적으로 기본 형식을 만들려고 하지만 구체적인 행위자를 인스턴스화하는 데 전혀 사용되지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="68e06-122">이런 경우에는 `abstract` 키워드를 사용하여 그런 형식을 기반으로 행위자를 만들지 않겠다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68e06-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68e06-123">Next steps</span></span>
* <span data-ttu-id="68e06-124">안정성, 확장성, 일관적인 상태를 제공하려면 [Reliable Actors 프레임워크에서 서비스 패브릭 플랫폼을 활용하는 방법](service-fabric-reliable-actors-platform.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68e06-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="68e06-125">[행위자 수명 주기](service-fabric-reliable-actors-lifecycle.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68e06-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
