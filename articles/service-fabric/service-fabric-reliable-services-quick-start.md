---
title: "C#에서 첫 번째 Service Fabric 응용 프로그램 만들기 | Microsoft Docs"
description: "상태 비저장 및 상태 저장 서비스를 사용하여 Microsoft Azure 서비스 패브릭 응용 프로그램 만들기 소개"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="f069a-103">Reliable Services로 시작하기</span><span class="sxs-lookup"><span data-stu-id="f069a-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f069a-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="f069a-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="f069a-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="f069a-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="f069a-106">Azure 서비스 패브릭 응용 프로그램에는 코드를 실행하는 하나 이상의 서비스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="f069a-107">이 가이드에서는 [Reliable Services](service-fabric-reliable-services-introduction.md)를 사용하여 상태 비저장 및 상태 저장 서비스 패브릭 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="f069a-108">이 Microsoft Virtual Academy 비디오는 상태 비저장 신뢰할 수 있는 서비스를 만드는 방법을 보여줍니다.<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="f069a-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="f069a-109">기본 개념</span><span class="sxs-lookup"><span data-stu-id="f069a-109">Basic concepts</span></span>
<span data-ttu-id="f069a-110">Reliable Services를 시작하려면 몇 가지 기본 개념만 이해하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="f069a-111">**서비스 유형**: 서비스 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="f069a-112">이름 및 버전 번호와 함께 `StatelessService` 및 기타 코드 또는 여기에 사용된 종속성을 확장하도록 사용자가 작성한 클래스에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="f069a-113">**명명된 서비스 인스턴스**: 서비스를 실행하려면 클래스 유형의 개체 인스턴스를 만드는 것처럼 서비스 유형의 명명된 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="f069a-114">서비스 인스턴스는 "fabric:/MyApp/MyService"와 같은 "fabric:/" 체계를 사용하는 URI 형식의 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="f069a-115">**서비스 호스트**: 호스트 프로세스 내에서 실행해야 하는 사용자가 만든 명명된 서비스 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="f069a-116">서비스 호스트는 서비스의 인스턴스에서 실행할 수 있는 프로세스일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="f069a-117">**서비스 등록**: 등록은 모든 항목을 함께 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="f069a-118">Service Fabric에서 실행할 인스턴스를 만들 수 있도록 서비스 호스트의 Service Fabric 런타임에 서비스 유형을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="f069a-119">상태 비저장 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="f069a-119">Create a stateless service</span></span>
<span data-ttu-id="f069a-120">상태 비저장 서비스는 현재 클라우드 응용 프로그램에서 정상인 서비스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="f069a-121">서비스 자체가 안정적으로 저장되거나 항상 사용 가능해야 하는 데이터를 포함하기 때문에 상태 비저장으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="f069a-122">상태 비저장 서비스의 인스턴스가 종료되면 모든 내부 상태가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="f069a-123">이러한 서비스 유형에서는 Azure 테이블 또는 SQL 데이터베이스와 같은 외부 저장소에 상태를 항상 유지하고 이를 위해 높은 가용성과 안정성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="f069a-124">관리자 권한으로 Visual Studio 2015 또는 Visual Studio 2017을 시작하고 *HelloWorld*라는 새로운 서비스 패브릭 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![새 프로젝트 대화 상자를 사용하여 새 서비스 패브릭 응용 프로그램 만들기](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="f069a-126">그런 다음 *HelloWorldStateless*라는 상태 비저장 서비스 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![두 번째 대화 상자에서 상태 비저장 서비스 프로젝트 만들기](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="f069a-128">이제 솔루션에는 2개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="f069a-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="f069a-129">*HelloWorld*.</span></span> <span data-ttu-id="f069a-130">*서비스*가 포함된 *응용 프로그램* 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="f069a-131">또한 응용 프로그램을 배포하는 데 도움이 되는 다양한 PowerShell 스크립트 뿐만 아니라 응용 프로그램을 설명하는 응용 프로그램 매니페스트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="f069a-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="f069a-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="f069a-133">서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-133">This is the service project.</span></span> <span data-ttu-id="f069a-134">상태 비저장 서비스 구현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="f069a-135">서비스 구현</span><span class="sxs-lookup"><span data-stu-id="f069a-135">Implement the service</span></span>
<span data-ttu-id="f069a-136">서비스 프로젝트에서 **HelloWorldStateless.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="f069a-137">서비스 패브릭에서 서비스는 모든 비즈니스 논리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="f069a-138">서비스 API는 코드에 대한 두 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="f069a-139">장기 실행 계산 워크로드 등 모든 워크로드의 실행을 시작할 수 있는 *RunAsync*라는 개방형 진입점 메서드.</span><span class="sxs-lookup"><span data-stu-id="f069a-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="f069a-140">ASP.NET Core와 같이 원하는 통신 스택을 연결할 수 있는 통신 진입점.</span><span class="sxs-lookup"><span data-stu-id="f069a-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="f069a-141">사용자 및 다른 서비스에서 요청을 수신하도록 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="f069a-142">이 자습서에서는 `RunAsync()` 진입점 메서드에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="f069a-143">바로 코드를 실행하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="f069a-144">프로젝트 템플릿에는 롤링 횟수를 증분하는 `RunAsync()` 의 샘플 구현이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="f069a-145">통신 스택을 사용하는 방법에 대한 자세한 내용은 [OWIN 자체 호스팅으로 서비스 패브릭 Web API 서비스](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="f069a-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="f069a-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="f069a-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="f069a-147">서비스의 인스턴스가 배치되어 실행할 준비가 되면 플랫폼이 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="f069a-148">상태 비저장 서비스의 경우 이는 간단히 말해 서비스 인스턴스가 열릴 때를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="f069a-149">서비스 인스턴스를 종료해야 하는 경우 취소 토큰이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="f069a-150">서비스 패브릭에서 서비스 인스턴스의 열림-닫힘 주기는 서비스의 수명 동안 전체적으로 여러 번 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="f069a-151">다음을 포함하여 여러 가지 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="f069a-152">시스템은 리소스 분산을 위해 서비스 인스턴스를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="f069a-153">오류는 코드에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-153">Faults occur in your code.</span></span>
* <span data-ttu-id="f069a-154">응용 프로그램 또는 시스템 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="f069a-155">기본 하드웨어가 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="f069a-156">이러한 오케스트레이션은 서비스의 가용성을 높게 유지하고 제대로 균형을 유지하기 위해 시스템에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="f069a-157">`RunAsync()`는 동기적으로 차단하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="f069a-158">RunAsync 구현은 런타임이 지속되도록 작업을 반환하거나 장기 실행 또는 차단 작업을 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="f069a-159">이전 예제의 `while(true)` 루프에는 작업 반환 `await Task.Delay()`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="f069a-160">워크로드가 동기적으로 차단해야 하는 경우 `RunAsync` 구현에서 `Task.Run()`을 사용하여 새 작업을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="f069a-161">워크로드 취소는 제공된 취소 토큰에 의해 조정된 공동의 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="f069a-162">시스템은 계속하기 전에 태스크가 종료(성공적인 완료, 취소 또는 오류에 의해)될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="f069a-163">시스템이 취소를 요청할 때 가능한 한 빨리 취소 토큰을 받아들이고 작업을 마치며 `RunAsync()` 를 종료하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="f069a-164">이 상태 비저장 서비스 예에서는 개수가 로컬 변수에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="f069a-165">하지만 이는 상태 비저장 서비스이므로 저장되는 값은 해당 서비스 인스턴스의 현재 주기에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="f069a-166">서비스가 이동하거나 다시 시작되면 값이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="f069a-167">상태 저장 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="f069a-167">Create a stateful service</span></span>
<span data-ttu-id="f069a-168">서비스 패브릭은 상태 저장하는 서비스의 새로운 종류를 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="f069a-169">상태 저장 서비스는 서비스를 사용하는 코드와 함께 위치한 서비스 자체 내에서 안정적으로 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="f069a-170">외부 저장소에 상태를 유지하지 않고도 서비스 패브릭에서 상태는 높은 가용성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="f069a-171">서비스가 이동하거나 다시 시작하는 경우에도 카운터 값을 상태 비저장에서 항상 사용 가능하고 지속되게 만들려면 상태 저장 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="f069a-172">동일한 *HelloWorld* 응용 프로그램에서 응용 프로그램 프로젝트의 서비스 참조를 마우스 오른쪽 단추로 클릭하고 **추가 -> 새 Service Fabric 서비스**를 선택하여 새 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![서비스 패브릭 응용 프로그램에 서비스 추가](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="f069a-174">**상태 저장 서비스** 를 선택하고 *HelloWorldStateful*이라는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="f069a-175">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-175">Click **OK**.</span></span>

![새 프로젝트 대화 상자를 사용하여 새 서비스 패브릭 상태 저장 서비스 만들기](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="f069a-177">응용 프로그램에 이제 상태 비저장 서비스 *HelloWorldStateless* 및 상태 저장 서비스 *HelloWorldStateful*의 두 서비스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="f069a-178">상태 저장 서비스에는 상태 비저장 서비스와 동일한 진입점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="f069a-179">주요 차이점은 상태를 안정적으로 저장할 수 있는 *상태 제공자* 의 가용성입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="f069a-180">서비스 패브릭은 신뢰할 수 있는 상태 관리자를 통해 복제된 데이터 구조를 만들 수 있는 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md)이라는 상태 제공자 구현과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="f069a-181">상태 저장 Reliable Service는 기본적으로 이 상태 제공자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="f069a-182">다음 RunAsync 메서드를 포함하는 **HelloWorldStateful** 에서 *HelloWorldStateful.cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="f069a-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="f069a-183">RunAsync</span></span>
<span data-ttu-id="f069a-184">`RunAsync()` 은 상태 저장 및 상태 비저장 서비스에서 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="f069a-185">그러나 상태 저장 서비스에서 플랫폼은 `RunAsync()`을 실행하기 전에 사용자 대신 추가 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="f069a-186">이 작업은 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션을 사용할 준비가 되도록 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="f069a-187">신뢰할 수 있는 컬렉션 및 신뢰할 수 있는 상태 관리자</span><span class="sxs-lookup"><span data-stu-id="f069a-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="f069a-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) 는 서비스에서 상태를 안정적으로 저장하는데 사용할 수 있는 사전 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="f069a-189">서비스 패브릭 및 신뢰할 수 있는 컬렉션을 사용하면 외부 영구 저장소 없이도 서비스에 데이터를 직접 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="f069a-190">신뢰할 수 있는 컬렉션은 데이터를 항상 사용할 수 있게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="f069a-191">서비스 패브릭은 서비스의 여러 *복제본* 을 만들고 관리하여 이를 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="f069a-192">또한 해당 복제본 및 해당 상태 전환을 관리하는 복잡성을 추상화하는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="f069a-193">신뢰할 수 있는 컬렉션은 사용자 지정 형식을 포함하여 모든 .NET 유형을 저장할 수 있습니다. 단, 몇 가지 주의 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="f069a-194">서비스 패브릭은 노드의 상태를 *복제* 하고 신뢰할 수 있는 컬렉션은 데이터를 각 복제본의 로컬 디스크에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="f069a-195">즉, 신뢰할 수 있는 컬렉션에 저장된 모든 항목이 *직렬화 가능*상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="f069a-196">신뢰할 수 있는 컬렉션은 기본적으로 [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx)를 사용하여 직렬화를 수행하므로 기본 직렬 변환기를 사용할 때 해당 유형이 [데이터 계약 직렬 변환기에서 지원되는지](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) 확인하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="f069a-197">신뢰할 수 있는 컬렉션의 트랜잭션을 커밋하면 고가용성을 위해 개체가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="f069a-198">신뢰할 수 있는 컬렉션에 저장된 개체는 서비스의 로컬 메모리에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="f069a-199">즉, 개체에 대한 로컬 참조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="f069a-200">트랜잭션의 신뢰할 수 있는 컬렉션에서 업데이트 작업을 수행하지 않고 해당 개체의 로컬 인스턴스를 변환하지 않는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="f069a-201">개체의 로컬 인스턴스에 대한 변경 내용은 자동으로 복제되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="f069a-202">개체를 디렉터리에 다시 삽입하거나 디렉터리의 *update* 메서드 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="f069a-203">신뢰할 수 있는 상태 관리자는 사용자에 대한 신뢰할 수 있는 컬렉션을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="f069a-204">언제든지 서비스의 어느 위치에서든 신뢰할 수 있는 컬렉션에 대한 신뢰할 수 있는 상태 관리자를 단순히 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="f069a-205">신뢰할 수 있는 상태 관리자는 참조를 다시 가져오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="f069a-206">클래스 멤버 변수 또는 속성에서 신뢰할 수 있는 컬렉션 인스턴스에 대한 참조를 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="f069a-207">서비스 수명 주기에서 항상 참조가 인스턴스로 설정되어 있도록 특별히 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="f069a-208">신뢰할 수 있는 상태 관리자는 사용자를 위해 이 작업을 처리하고 반복 방문에 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="f069a-209">트랜잭션 및 비동기 작업</span><span class="sxs-lookup"><span data-stu-id="f069a-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="f069a-210">신뢰할 수 있는 컬렉션에는 LINQ를 제외하고 해당 `System.Collections.Generic` 및 `System.Collections.Concurrent` 항목이 수행하는 동일한 작업이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="f069a-211">신뢰할 수 있는 컬렉션의 작업은 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="f069a-212">신뢰할 수 있는 컬렉션을 사용한 쓰기 작업에서는 I/O 작업을 수행하여 데이터를 복제하고 디스크에 보존하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="f069a-213">신뢰할 수 있는 컬렉션 작업은 *트랜잭션*이므로 여러 신뢰할 수 있는 컬렉션 및 작업에서 상태를 일관성 있게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="f069a-214">예를 들어 신뢰할 수 있는 큐에서 작업 항목을 제거하고, 작업을 수행하고, 신뢰할 수 있는 사전의 결과를 모두 단일 트랜잭션 내에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="f069a-215">이는 원자성 작업으로 처리되며, 전체 작업이 성공하거나 롤백되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="f069a-216">항목을 큐에서 제거한 다음이지만 결과를 저장하기 전에 오류가 발생하면 전체 트랜잭션이 롤백되고 항목이 처리를 위해 큐에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f069a-217">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f069a-217">Run the application</span></span>
<span data-ttu-id="f069a-218">*HelloWorld* 응용 프로그램으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="f069a-219">이제 서비스를 빌드하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-219">You can now build and deploy your services.</span></span> <span data-ttu-id="f069a-220">**F5**키를 누르면 응용 프로그램이 빌드되고 로컬 클러스터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="f069a-221">서비스가 실행되기 시작한 후에 **진단 이벤트** 창에서 생성된 ETW(Windows용 이벤트 추적) 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="f069a-222">응용 프로그램의 상태 비저장 서비스 및 상태 저장 서비스 모두에서 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="f069a-223">**일시 중지** 단추를 클릭하여 스트림을 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="f069a-224">그런 다음 해당 메시지를 확장하여 메시지의 세부 정보를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="f069a-225">응용 프로그램을 실행하기 전에 로컬 개발 클러스터가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="f069a-226">로컬 환경 설정의 자세한 내용은 [시작 가이드](service-fabric-get-started.md) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f069a-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Visual Studio에서 진단 이벤트 보기](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="f069a-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f069a-228">Next steps</span></span>
[<span data-ttu-id="f069a-229">Visual Studio에서 서비스 패브릭 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="f069a-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="f069a-230">시작: OWIN 자체 호스팅을 사용하는 서비스 패브릭 Web API 서비스</span><span class="sxs-lookup"><span data-stu-id="f069a-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="f069a-231">신뢰할 수 있는 컬렉션에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f069a-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="f069a-232">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f069a-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="f069a-233">응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="f069a-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="f069a-234">신뢰할 수 있는 서비스에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="f069a-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

