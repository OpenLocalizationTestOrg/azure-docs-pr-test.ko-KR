---
title: "aaaCreate 프로그램 첫 번째 행위자 기반 Azure 마이크로 서비스 java에서 | Microsoft Docs"
description: "이 자습서의 만들기, 디버깅 및 서비스 패브릭 Reliable Actors를 사용 하 여 간단한 행위자 기반 서비스를 배포 hello 단계를 안내 합니다."
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
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="2765a-103">Reliable Actors 시작</span><span class="sxs-lookup"><span data-stu-id="2765a-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2765a-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="2765a-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="2765a-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="2765a-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="2765a-106">이 문서는 Azure 서비스 패브릭 Reliable Actors의 hello 기본 사항에 설명 하 고 만들기 및 java에서 간단한 Reliable Actor 응용 프로그램을 배포 하는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="2765a-107">설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="2765a-107">Installation and setup</span></span>
<span data-ttu-id="2765a-108">시작 하기 전에 hello 서비스 패브릭 개발 환경 컴퓨터에 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="2765a-109">Tooset 해야 할 경우, 상태로 업데이트 너무 않을[Mac에서 시작](service-fabric-get-started-mac.md) 또는 [linux 시작](service-fabric-get-started-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="2765a-110">기본 개념</span><span class="sxs-lookup"><span data-stu-id="2765a-110">Basic concepts</span></span>
<span data-ttu-id="2765a-111">Reliable Actors만 시작 tooget toounderstand 몇 가지 기본 개념을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="2765a-112">**행위자 서비스**.</span><span class="sxs-lookup"><span data-stu-id="2765a-112">**Actor service**.</span></span> <span data-ttu-id="2765a-113">Reliable Actors hello 서비스 패브릭 인프라에 배포할 수 있는 신뢰할 수 있는 서비스에 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="2765a-114">행위자 인스턴스는 명명된 서비스 인스턴스에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="2765a-115">**행위자 등록**.</span><span class="sxs-lookup"><span data-stu-id="2765a-115">**Actor registration**.</span></span> <span data-ttu-id="2765a-116">신뢰할 수 있는 서비스와 함께 하 Reliable Actor 서비스에 등록 된 hello 서비스 패브릭 런타임을 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="2765a-117">또한 hello 행위자 형식에 등록 된 hello 행위자 런타임 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="2765a-118">**행위자 인터페이스**.</span><span class="sxs-lookup"><span data-stu-id="2765a-118">**Actor interface**.</span></span> <span data-ttu-id="2765a-119">hello 행위자 인터페이스는 사용 되는 toodefine 행위자의 강력한 형식의 공용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="2765a-120">Reliable Actor 모델 용어 hello hello 행위자 인터페이스 hello 행위자 hello 메시지 유형을 이해 하 고 처리할 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="2765a-121">클라이언트 응용 프로그램 너무 "send" (비동기) 메시지 toohello 행위자 및 hello 행위자 인터페이스 다른 행위자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="2765a-122">Reliable Actors는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="2765a-123">**ActorProxy 클래스**.</span><span class="sxs-lookup"><span data-stu-id="2765a-123">**ActorProxy class**.</span></span> <span data-ttu-id="2765a-124">hello ActorProxy 클래스 클라이언트 응용 프로그램 tooinvoke에서 사용 하는 hello hello 행위자 인터페이스를 통해 노출 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="2765a-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="2765a-125">hello ActorProxy 클래스는 두 가지 중요 한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="2765a-126">이름 확인: hello 클러스터 (찾기 그 데이터베이스가 호스팅될 hello 클러스터의 노드 hello)에서 수 toolocate hello 작업자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="2765a-127">오류 처리: hello 행위자 toobe를 필요로 하는 오류 hello 클러스터의 노드 tooanother 재배치 하는 예를 들어,이 메서드 호출을 다시 시도 하 고 다시 후 hello 행위자 위치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="2765a-128">hello tooactor 인터페이스와 관련 된 규칙 설명이 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="2765a-129">행위자 인터페이스 메서드는 오버로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="2765a-130">행위자 인터페이스 메서드에는 out, ref 또는 선택적 매개 변수가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="2765a-131">제네릭 인터페이스는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="2765a-132">행위자 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2765a-132">Create an actor service</span></span>
<span data-ttu-id="2765a-133">새 Service Fabric 응용 프로그램을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="2765a-134">Linux 용 서비스 패브릭 SDK hello 포함 한 Yeoman 생성기 tooprovide hello 스 캐 폴딩 상태 비저장 서비스와 서비스 패브릭 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="2765a-135">Hello를 실행 하 여 시작 Yeoman 다음 명령:</span><span class="sxs-lookup"><span data-stu-id="2765a-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="2765a-136">Hello 지침 toocreate에 따라 한 **Reliable Actor 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="2765a-137">이 자습서에서는 이름을 hello 응용 프로그램 "HelloWorldActorApplication" 및 hello 행위자 "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="2765a-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="2765a-138">스 캐 폴딩 다음 hello는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-138">hello following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="2765a-139">신뢰할 수 있는 행위자 기본 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2765a-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="2765a-140">앞에서 설명한 hello 기본 개념 hello Reliable Actor 서비스의 기본 빌딩 블록으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="2765a-141">행위자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="2765a-141">Actor interface</span></span>
<span data-ttu-id="2765a-142">이 hello 작업자에 대해 hello 인터페이스 정의 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="2765a-143">Hello 행위자 구현과 hello 행위자를 호출 하 여 일반적으로 의미 toodefine hello 행위자 구현과에서 분리 하 고 다른 여러에서 공유할 수 있는 위치에 있으므로 hello 클라이언트가에서 공유 하는 hello 행위자 계약을 정의 하는이 인터페이스 서비스 또는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="2765a-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="2765a-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="2765a-145">행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="2765a-145">Actor service</span></span>
<span data-ttu-id="2765a-146">여기에는 행위자 구현 및 행위자 등록 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="2765a-147">hello 행위자 클래스 hello 행위자 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="2765a-148">사용자 행위자가 작업을 수행하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-148">This is where your actor does its work.</span></span>

<span data-ttu-id="2765a-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="2765a-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="2765a-150">행위자 등록</span><span class="sxs-lookup"><span data-stu-id="2765a-150">Actor registration</span></span>
<span data-ttu-id="2765a-151">hello 행위자 서비스는 hello 서비스 패브릭 런타임에서 서비스 유형으로 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="2765a-152">주문 hello 행위자 서비스 toorun 행위자 인스턴스, 행위자 형식 hello 행위자 서비스에도 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="2765a-153">hello `ActorRuntime` 등록 메서드는 행위자를 위한이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="2765a-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="2765a-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="2765a-155">테스트 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2765a-155">Test client</span></span>
<span data-ttu-id="2765a-156">간단한 테스트 클라이언트 응용 프로그램에서 실행할 수 있습니다 별도로 hello 서비스 패브릭 응용 프로그램 tootest 행위자 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="2765a-157">이 예제는 hello ActorProxy 사용된 tooactivate 수 및 행위자 인스턴스와 통신할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="2765a-158">사용자의 서비스와 함께 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="2765a-159">hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2765a-159">hello application</span></span>
<span data-ttu-id="2765a-160">마지막으로, 응용 프로그램 패키지 hello hello 행위자 서비스 및 기타 서비스 배포에 대 한 향후 hello에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="2765a-161">Hello 포함 되어 *ApplicationManifest.xml* 및 hello 행위자 서비스 패키지에 대 한 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="2765a-162">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2765a-162">Run hello application</span></span>

<span data-ttu-id="2765a-163">hello Yeoman 스 캐 폴딩 gradle 스크립트 toobuild hello 응용 프로그램 및 bash 스크립트 toodeploy 및 응용 프로그램 제거를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="2765a-164">toodeploy hello 응용 프로그램, gradle 하는 첫 번째 빌드 hello 적용:</span><span class="sxs-lookup"><span data-stu-id="2765a-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="2765a-165">그러면 Service Fabric CLI 도구를 사용하여 배포할 수 있는 Service Fabric 응용 프로그램 패키지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="2765a-166">Service Fabric CLI 배포</span><span class="sxs-lookup"><span data-stu-id="2765a-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="2765a-167">hello install.sh 스크립트 hello 필요한 서비스 패브릭 CLI (sfctl) 명령을 toodeploy hello 응용 프로그램 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="2765a-168">Hello install.sh 스크립트 toodeploy hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2765a-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="2765a-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2765a-169">Next steps</span></span>

* [<span data-ttu-id="2765a-170">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="2765a-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
