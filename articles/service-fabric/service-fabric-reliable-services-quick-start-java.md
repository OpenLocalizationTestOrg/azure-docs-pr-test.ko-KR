---
title: "Java에서 첫 번째 신뢰할 수 있는 Azure 마이크로 서비스 만들기 | Microsoft Docs"
description: "상태 비저장 및 상태 저장 서비스를 사용하여 Microsoft Azure 서비스 패브릭 응용 프로그램 만들기 소개"
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="c0878-103">Reliable Services로 시작하기</span><span class="sxs-lookup"><span data-stu-id="c0878-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0878-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="c0878-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="c0878-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="c0878-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="c0878-106">이 문서는 Azure Service Fabric Reliable Services의 기본 개념을 설명하고 Java로 작성된 Reliable Services 응용 프로그램을 생성 및 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="c0878-107">이 Microsoft Virtual Academy 비디오는 상태 비저장 신뢰할 수 있는 서비스를 만드는 방법을 보여줍니다.<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="c0878-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="c0878-108">설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="c0878-108">Installation and setup</span></span>
<span data-ttu-id="c0878-109">시작하기 전에 컴퓨터에 Service Fabric 개발 환경이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="c0878-110">설정해야 하는 경우 [Mac에서 시작](service-fabric-get-started-mac.md) 또는 [Linux에서 시작](service-fabric-get-started-linux.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="c0878-111">기본 개념</span><span class="sxs-lookup"><span data-stu-id="c0878-111">Basic concepts</span></span>
<span data-ttu-id="c0878-112">Reliable Services를 시작하려면 몇 가지 기본 개념만 이해하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="c0878-113">**서비스 유형**: 서비스 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="c0878-114">이름 및 버전 번호와 함께 `StatelessService` 및 기타 코드 또는 여기에 사용된 종속성을 확장하도록 사용자가 작성한 클래스에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="c0878-115">**명명된 서비스 인스턴스**: 서비스를 실행하려면 클래스 유형의 개체 인스턴스를 만드는 것처럼 서비스 유형의 명명된 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="c0878-116">서비스 인스턴스는 실제로 사용자가 작성한 서비스 클래스의 개체 인스턴스화입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="c0878-117">**서비스 호스트**: 호스트 내에서 실행해야 하는 사용자가 만든 명명된 서비스 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="c0878-118">서비스 호스트는 서비스의 인스턴스에서 실행할 수 있는 프로세스일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="c0878-119">**서비스 등록**: 등록은 모든 항목을 함께 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="c0878-120">Service Fabric에서 실행할 인스턴스를 만들 수 있도록 서비스 호스트의 Service Fabric 런타임에 서비스 유형을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="c0878-121">상태 비저장 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c0878-121">Create a stateless service</span></span>
<span data-ttu-id="c0878-122">Service Fabric 응용 프로그램을 만드는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="c0878-123">Linux용 Service Fabric SDK는 Service Fabric 응용 프로그램용 스캐폴딩에 상태 비저장 서비스를 제공하기 위해 Yeoman 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="c0878-124">다음 Yeoman 명령을 실행하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="c0878-125">지침에 따라 **신뢰할 수 있는 상태 비저장 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="c0878-126">이 자습서에서는 응용 프로그램을 "HelloWorldApplication", 행위자를 "HelloWorld"라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="c0878-127">결과에는 `HelloWorldApplication` 및 `HelloWorld`에 대한 디렉터리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-the-service"></a><span data-ttu-id="c0878-128">서비스 구현</span><span class="sxs-lookup"><span data-stu-id="c0878-128">Implement the service</span></span>
<span data-ttu-id="c0878-129">**HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="c0878-130">이 클래스는 서비스 유형을 정의하고 모든 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="c0878-131">서비스 API는 코드에 대한 두 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="c0878-132">장기 실행 계산 워크로드 등 모든 워크로드의 실행을 시작할 수 있는 `runAsync()`라는 개방형 진입점 메서드.</span><span class="sxs-lookup"><span data-stu-id="c0878-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="c0878-133">원하는 통신 스택을 연결할 수 있는 통신 진입점.</span><span class="sxs-lookup"><span data-stu-id="c0878-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="c0878-134">사용자 및 다른 서비스에서 요청을 수신하도록 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="c0878-135">이 자습서에서는 `runAsync()` 진입점 메서드에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="c0878-136">바로 코드를 실행하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="c0878-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="c0878-137">RunAsync</span></span>
<span data-ttu-id="c0878-138">서비스의 인스턴스가 배치되어 실행할 준비가 되면 플랫폼이 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="c0878-139">상태 비저장 서비스의 경우 이는 간단히 말해 서비스 인스턴스가 열릴 때를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="c0878-140">서비스 인스턴스를 종료해야 하는 경우 취소 토큰이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="c0878-141">서비스 패브릭에서 서비스 인스턴스의 열림-닫힘 주기는 서비스의 수명 동안 전체적으로 여러 번 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="c0878-142">다음을 포함하여 여러 가지 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="c0878-143">시스템은 리소스 분산을 위해 서비스 인스턴스를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="c0878-144">오류는 코드에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-144">Faults occur in your code.</span></span>
* <span data-ttu-id="c0878-145">응용 프로그램 또는 시스템 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="c0878-146">기본 하드웨어가 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="c0878-147">이러한 오케스트레이션은 서비스의 가용성을 높게 유지하고 제대로 균형을 유지하기 위해 Service Fabric에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="c0878-148">`runAsync()`는 동기적으로 차단하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="c0878-149">runAsync의 구현에서는 런타임을 지속할 수 있게 CompletableFuture를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="c0878-150">워크로드에서 실행 시간이 긴 작업을 구현해야 하는 경우 이 작업은 CompletableFuture에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="c0878-151">취소</span><span class="sxs-lookup"><span data-stu-id="c0878-151">Cancellation</span></span>
<span data-ttu-id="c0878-152">워크로드 취소는 제공된 취소 토큰에 의해 조정된 공동의 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="c0878-153">시스템은 계속하기 전에 태스크가 종료(성공적인 완료, 취소 또는 오류에 의해)될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="c0878-154">시스템이 취소를 요청할 때 가능한 한 빨리 취소 토큰을 받아들이고 작업을 마치며 `runAsync()` 를 종료하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="c0878-155">다음 예제에서는 취소 이벤트를 처리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="c0878-156">서비스 등록</span><span class="sxs-lookup"><span data-stu-id="c0878-156">Service registration</span></span>
<span data-ttu-id="c0878-157">서비스 유형은 Service Fabric 런타임에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="c0878-158">서비스 유형은 `ServiceManifest.xml`에서 정의되고 `StatelessService`를 구현하는 서비스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="c0878-159">서비스 등록은 프로세스 주 진입점에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="c0878-160">이 예제에서는 프로세스 주 진입점은 `HelloWorldServiceHost.java`입니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-the-application"></a><span data-ttu-id="c0878-161">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c0878-161">Run the application</span></span>

<span data-ttu-id="c0878-162">Yeoman 스캐폴딩은 응용 프로그램을 빌드하는 Gradle 스크립트와 응용 프로그램을 배포하고 제거하는 Bash 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="c0878-163">응용 프로그램을 실행하려면 먼저 다음과 같은 Gradle을 통해 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="c0878-164">그러면 Service Fabric CLI를 사용하여 배포할 수 있는 Service Fabric 응용 프로그램 패키지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="c0878-165">Service Fabric CLI를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="c0878-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="c0878-166">install.sh 스크립트는 응용 프로그램 패키지를 배포하는 데 필요한 Service Fabric CLI 명령을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="c0878-167">install.sh 스크립트를 실행하여 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c0878-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="c0878-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0878-168">Next steps</span></span>

* [<span data-ttu-id="c0878-169">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="c0878-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
