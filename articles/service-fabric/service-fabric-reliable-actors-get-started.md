---
title: "C#에서 첫 번째 행위자 기반 Azure 마이크로 서비스 만들기 | Microsoft Docs"
description: "이 자습서에서는 서비스 패브릭 Reliable Actors를 사용하여 간단한 행위자 기반 서비스를 생성, 디버깅 및 배포하는 과정을 단계별로 안내합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="75cea-103">Reliable Actors 시작</span><span class="sxs-lookup"><span data-stu-id="75cea-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75cea-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="75cea-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="75cea-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="75cea-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="75cea-106">이 문서는 Azure 서비스 패브릭 Reliable Actors의 기본 개념을 설명하고 Visual Studio에서 간단한 Reliable Actor 응용 프로그램을 생성, 디버깅 및 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="75cea-107">설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="75cea-107">Installation and setup</span></span>
<span data-ttu-id="75cea-108">시작하기 전에 컴퓨터에 서비스 패브릭 개발 환경이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="75cea-109">이를 설정하려면 [개발 환경을 설정하는 방법](service-fabric-get-started.md)에 대한 자세한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75cea-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="75cea-110">기본 개념</span><span class="sxs-lookup"><span data-stu-id="75cea-110">Basic concepts</span></span>
<span data-ttu-id="75cea-111">Reliable Actors를 시작하려면 몇 가지 기본 개념만 이해하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="75cea-112">**행위자 서비스**.</span><span class="sxs-lookup"><span data-stu-id="75cea-112">**Actor service**.</span></span> <span data-ttu-id="75cea-113">Reliable Actors는 서비스 패브릭 인프라에 배포될 수 있는 Reliable Services에 패키징됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="75cea-114">행위자 인스턴스는 명명된 서비스 인스턴스에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="75cea-115">**행위자 등록**.</span><span class="sxs-lookup"><span data-stu-id="75cea-115">**Actor registration**.</span></span> <span data-ttu-id="75cea-116">Reliable Services와 마찬가지로 Reliable Actor 서비스를 Service Fabric 런타임에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="75cea-117">또한 행위자 형식을 행위자 런타임에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="75cea-118">**행위자 인터페이스**.</span><span class="sxs-lookup"><span data-stu-id="75cea-118">**Actor interface**.</span></span> <span data-ttu-id="75cea-119">행위자 인터페이스는 행위자에 대한 강력한 형식의 공용 인터페이스를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="75cea-120">Reliable Actor 모델 용어에서 행위자 인터페이스는 행위자가 이해하고 처리할 수 있는 메시지의 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="75cea-121">행위자 인터페이스는 다른 행위자 또는 클라이언트 응용 프로그램에서 메시지를 행위자에게 "보내는"(비동기) 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="75cea-122">Reliable Actors는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="75cea-123">**ActorProxy 클래스**.</span><span class="sxs-lookup"><span data-stu-id="75cea-123">**ActorProxy class**.</span></span> <span data-ttu-id="75cea-124">ActorProxy 클래스는 클라이언트 응용 프로그램에서 행위자 인터페이스를 통해 노출되는 메서드를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="75cea-125">ActorProxy 클래스는 다음 두 가지 중요한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="75cea-126">이름 확인: 클러스터에서 행위자를 찾을 수 있습니다(호스트되는 클러스터의 노드 찾기).</span><span class="sxs-lookup"><span data-stu-id="75cea-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="75cea-127">오류 처리: 메서드 호출을 다시 시도하고 행위자를 클러스터의 다른 노드로 재배치해야 하는 경우 등의 오류가 발생한 후 행위자의 위치를 다시 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="75cea-128">행위자 인터페이스와 관련된 다음 규칙을 확인하면 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="75cea-129">행위자 인터페이스 메서드는 오버로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="75cea-130">행위자 인터페이스 메서드에는 out, ref 또는 선택적 매개 변수가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="75cea-131">제네릭 인터페이스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="75cea-132">Visual Studio에서 새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="75cea-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="75cea-133">관리자 권한으로 Visual Studio 2015 또는 Visual Studio 2017을 시작하고 새로운 Service Fabric 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Visual Studio용 서비스 패브릭 도구 - 새 프로젝트][1]

<span data-ttu-id="75cea-135">다음 대화 상자에서 만들려는 프로젝트의 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![서비스 패브릭 프로젝트 템플릿][5]

<span data-ttu-id="75cea-137">HelloWorld 프로젝트의 경우 서비스 패브릭 Reliable Actors 서비스를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="75cea-138">솔루션을 만들고 나면 다음과 같은 구조로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-138">After you have created the solution, you should see the following structure:</span></span>

![서비스 패브릭 프로젝트 구조][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="75cea-140">신뢰할 수 있는 행위자 기본 구성 요소</span><span class="sxs-lookup"><span data-stu-id="75cea-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="75cea-141">일반적으로 Reliable Actors 솔루션은 다음 3개 프로젝트로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="75cea-142">**응용 프로그램 프로젝트(MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="75cea-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="75cea-143">배포를 위해 모든 서비스를 함께 패키지하는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="75cea-144">응용 프로그램을 관리하기 위한 *ApplicationManifest.xml* 및 PowerShell 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="75cea-145">**인터페이스 프로젝트(MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="75cea-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="75cea-146">행위자에 대한 인터페이스 정의가 포함된 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="75cea-147">MyActor.Interfaces 프로젝트에서 솔루션의 행위자에 의해 사용될 인터페이스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="75cea-148">행위자 인터페이스는 모든 프로젝트에서 어떤 이름으로든 정의될 수 있지만 인터페이스는 행위자 구현과 행위자를 호출하는 클라이언트에서 공유되는 행위자 계약을 정의하므로 일반적으로 행위자 구현과 별개이고 다른 여러 프로젝트에서 공유될 수 있는 어셈블리에서 정의하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="75cea-149">**행위자 서비스 프로젝트(MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="75cea-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="75cea-150">행위자를 호스트할 서비스 패브릭 서비스를 정의하는 데 사용되는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="75cea-151">행위자의 구현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="75cea-152">행위자 구현은 기본 형식( `Actor` )에서 파생되는 클래스로서, MyActor.Interfaces 프로젝트에 정의된 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="75cea-153">또한 행위자 클래스는 `ActorService` 인스턴스 및 `ActorId`를 허용하고 이를 기본 `Actor` 클래스에 전달하는 생성자를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="75cea-154">그러면 플랫폼 종속성의 생성자 종속성 주입이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="75cea-155">행위자 서비스는 서비스 패브릭 런타임에서 서비스 유형에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="75cea-156">행위자 서비스에서 행위자 인스턴스를 실행하려면 행위자 서비스에 행위자 유형이 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="75cea-157">`ActorRuntime` 등록 메서드가 행위자에 대한 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="75cea-158">Visual Studio에서 새 프로젝트를 시작하고 하나의 행위자 정의만 있는 경우, 등록은 기본적으로 Visual Studio에서 생성하는 코드에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="75cea-159">서비스에서 다른 행위자를 정의하는 경우 다음을 사용하여 행위자 등록을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="75cea-160">서비스 패브릭 행위자 런타임에서는 일부 [행위자 메서드와 관련된 이벤트 및 성능 카운터](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters)를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="75cea-161">진단 및 성능 모니터링에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="75cea-162">디버그</span><span class="sxs-lookup"><span data-stu-id="75cea-162">Debugging</span></span>
<span data-ttu-id="75cea-163">Visual Studio용 서비스 패브릭 도구는 로컬 컴퓨터에서 디버깅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="75cea-164">F5 키를 눌러서 디버깅 세션을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="75cea-165">Visual Studio는 (필요한 경우) 패키지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="75cea-166">또한 로컬 서비스 패브릭 클러스터에 응용 프로그램을 배포하고 디버거를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="75cea-167">배포 프로세스가 진행되는 동안 **출력** 창에서 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![서비스 패브릭 디버깅 출력 창][3]

## <a name="next-steps"></a><span data-ttu-id="75cea-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75cea-169">Next steps</span></span>
<span data-ttu-id="75cea-170">[Reliable Actors가 Service Fabric 플랫폼을 사용하는 방법](service-fabric-reliable-actors-platform.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75cea-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
