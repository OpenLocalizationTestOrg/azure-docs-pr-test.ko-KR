---
title: "Java에서 첫 번째 행위자 기반 Azure 마이크로 서비스 만들기 | Microsoft Docs"
description: "이 자습서에서는 서비스 패브릭 Reliable Actors를 사용하여 간단한 행위자 기반 서비스를 생성, 디버깅 및 배포하는 과정을 단계별로 안내합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="90e45-103">Reliable Actors 시작</span><span class="sxs-lookup"><span data-stu-id="90e45-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90e45-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="90e45-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="90e45-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="90e45-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="90e45-106">이 문서는 Azure Service Fabric Reliable Actors의 기본 개념을 설명하고 Java에서 간단한 Reliable Actor 응용 프로그램을 생성 및 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="90e45-107">설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="90e45-107">Installation and setup</span></span>
<span data-ttu-id="90e45-108">시작하기 전에 컴퓨터에 Service Fabric 개발 환경이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="90e45-109">설정해야 하는 경우 [Mac에서 시작](service-fabric-get-started-mac.md) 또는 [Linux에서 시작](service-fabric-get-started-linux.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="90e45-110">기본 개념</span><span class="sxs-lookup"><span data-stu-id="90e45-110">Basic concepts</span></span>
<span data-ttu-id="90e45-111">Reliable Actors를 시작하려면 몇 가지 기본 개념만 이해하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="90e45-112">**행위자 서비스**.</span><span class="sxs-lookup"><span data-stu-id="90e45-112">**Actor service**.</span></span> <span data-ttu-id="90e45-113">Reliable Actors는 서비스 패브릭 인프라에 배포될 수 있는 Reliable Services에 패키징됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="90e45-114">행위자 인스턴스는 명명된 서비스 인스턴스에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="90e45-115">**행위자 등록**.</span><span class="sxs-lookup"><span data-stu-id="90e45-115">**Actor registration**.</span></span> <span data-ttu-id="90e45-116">Reliable Services와 마찬가지로 Reliable Actor 서비스를 Service Fabric 런타임에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="90e45-117">또한 행위자 형식을 행위자 런타임에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="90e45-118">**행위자 인터페이스**.</span><span class="sxs-lookup"><span data-stu-id="90e45-118">**Actor interface**.</span></span> <span data-ttu-id="90e45-119">행위자 인터페이스는 행위자에 대한 강력한 형식의 공용 인터페이스를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="90e45-120">Reliable Actor 모델 용어에서 행위자 인터페이스는 행위자가 이해하고 처리할 수 있는 메시지의 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="90e45-121">행위자 인터페이스는 다른 행위자 또는 클라이언트 응용 프로그램에서 메시지를 행위자에게 "보내는"(비동기) 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="90e45-122">Reliable Actors는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="90e45-123">**ActorProxy 클래스**.</span><span class="sxs-lookup"><span data-stu-id="90e45-123">**ActorProxy class**.</span></span> <span data-ttu-id="90e45-124">ActorProxy 클래스는 클라이언트 응용 프로그램에서 행위자 인터페이스를 통해 노출되는 메서드를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="90e45-125">ActorProxy 클래스는 다음 두 가지 중요한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="90e45-126">이름 확인: 클러스터에서 행위자를 찾을 수 있습니다(호스트되는 클러스터의 노드 찾기).</span><span class="sxs-lookup"><span data-stu-id="90e45-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="90e45-127">오류 처리: 메서드 호출을 다시 시도하고 행위자를 클러스터의 다른 노드로 재배치해야 하는 경우 등의 오류가 발생한 후 행위자의 위치를 다시 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="90e45-128">행위자 인터페이스와 관련된 다음 규칙을 확인하면 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="90e45-129">행위자 인터페이스 메서드는 오버로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="90e45-130">행위자 인터페이스 메서드에는 out, ref 또는 선택적 매개 변수가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="90e45-131">제네릭 인터페이스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="90e45-132">행위자 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="90e45-132">Create an actor service</span></span>
<span data-ttu-id="90e45-133">새 Service Fabric 응용 프로그램을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="90e45-134">Linux용 Service Fabric SDK는 Service Fabric 응용 프로그램용 스캐폴딩에 상태 비저장 서비스를 제공하기 위해 Yeoman 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="90e45-135">다음 Yeoman 명령을 실행하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="90e45-136">지침에 따라 **신뢰할 수 있는 행위자 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="90e45-137">이 자습서에서는 응용 프로그램을 "HelloWorldActorApplication", 행위자를 "HelloWorldActor"라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="90e45-138">다음 스캐폴딩이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-138">The following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="90e45-139">신뢰할 수 있는 행위자 기본 구성 요소</span><span class="sxs-lookup"><span data-stu-id="90e45-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="90e45-140">앞에서 설명한 기본 개념은 신뢰할 수 있는 행위자 서비스의 기본 구성 요소로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="90e45-141">행위자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="90e45-141">Actor interface</span></span>
<span data-ttu-id="90e45-142">여기에는 행위자에 대한 인터페이스 정의가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="90e45-143">이 인터페이스는 행위자 구현과 행위자를 호출하는 클라이언트에 의해 공유되는 행위자 계약을 정의하므로 일반적으로 행위자 구현과는 별개이고 다른 여러 서비스 또는 클라이언트 응용 프로그램이 공유할 수 있는 장소에서 정의하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="90e45-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="90e45-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="90e45-145">행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="90e45-145">Actor service</span></span>
<span data-ttu-id="90e45-146">여기에는 행위자 구현 및 행위자 등록 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="90e45-147">행위자 클래스는 행위자 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="90e45-148">사용자 행위자가 작업을 수행하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-148">This is where your actor does its work.</span></span>

<span data-ttu-id="90e45-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="90e45-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="90e45-150">행위자 등록</span><span class="sxs-lookup"><span data-stu-id="90e45-150">Actor registration</span></span>
<span data-ttu-id="90e45-151">행위자 서비스는 서비스 패브릭 런타임에서 서비스 유형에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="90e45-152">행위자 서비스에서 행위자 인스턴스를 실행하려면 행위자 서비스에 행위자 유형이 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="90e45-153">`ActorRuntime` 등록 메서드가 행위자에 대한 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="90e45-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="90e45-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="90e45-155">테스트 클라이언트</span><span class="sxs-lookup"><span data-stu-id="90e45-155">Test client</span></span>
<span data-ttu-id="90e45-156">이는 행위자 서비스를 테스트하기 위해 Service Fabric 응용 프로그램과 별개로 실행할 수 있는 간단한 테스트 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="90e45-157">이는 행위자 인스턴스를 활성화하고 통신하기 위해 ActorProxy를 사용할 수 있는 위치의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="90e45-158">사용자의 서비스와 함께 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="90e45-159">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="90e45-159">The application</span></span>
<span data-ttu-id="90e45-160">마지막으로, 응용 프로그램은 배포를 위해 나중에 추가할 수 있는 행위자 서비스와 기타 모든 서비스를 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="90e45-161">여기에는 *ApplicationManifest.xml*와 행위자 서비스 패키지를 위한 자리 표시자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="90e45-162">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="90e45-162">Run the application</span></span>

<span data-ttu-id="90e45-163">Yeoman 스캐폴딩은 응용 프로그램을 빌드하는 Gradle 스크립트와 응용 프로그램을 배포하고 제거하는 Bash 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="90e45-164">응용 프로그램을 배포하려면 먼저 다음과 같은 Gradle을 통해 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="90e45-165">그러면 Service Fabric CLI 도구를 사용하여 배포할 수 있는 Service Fabric 응용 프로그램 패키지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="90e45-166">Service Fabric CLI 배포</span><span class="sxs-lookup"><span data-stu-id="90e45-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="90e45-167">install.sh 스크립트는 응용 프로그램 패키지를 배포하는 데 필요한 Service Fabric CLI(sfctl) 명령을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="90e45-168">install.sh 스크립트를 실행하여 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="90e45-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="90e45-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90e45-169">Next steps</span></span>

* [<span data-ttu-id="90e45-170">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="90e45-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
