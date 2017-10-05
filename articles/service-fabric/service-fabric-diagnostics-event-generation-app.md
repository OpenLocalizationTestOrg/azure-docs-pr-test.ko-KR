---
title: "Azure Service Fabric 응용 프로그램 수준 모니터링 | Microsoft Docs"
description: "Azure Service Fabric 클러스터를 모니터링 및 진단하는 데 사용되는 응용 프로그램 및 서비스 수준 이벤트와 로그에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="1c1a3-103">응용 프로그램 및 서비스 수준 이벤트와 로그 생성</span><span class="sxs-lookup"><span data-stu-id="1c1a3-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="1c1a3-104">사용자 지정 이벤트를 사용하여 코드 계측</span><span class="sxs-lookup"><span data-stu-id="1c1a3-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="1c1a3-105">코드를 계측하는 것은 다른 측면 대부분의 서비스 모니터링에 대한 기반이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="1c1a3-106">계측은 무언가가 잘못되었다는 것을 알 수 있는 유일한 방법이며, 수정해야 할 것을 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="1c1a3-107">기술적으로 디버거를 프로덕션 서비스에 연결할 수도 있지만 일반적인 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="1c1a3-108">따라서 자세한 계측 데이터를 갖는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="1c1a3-109">일부 제품은 자동으로 코드를 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="1c1a3-110">이러한 솔루션이 잘 작동할 수 있지만 수동 계측이 거의 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="1c1a3-111">결국 응용 프로그램을 과학 수사 방식으로 디버그하는 데 필요한 정보가 충분히 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="1c1a3-112">이 문서에서는 코드를 계측하는 여러 가지 방법, 그리고 다른 방법 대신 특정 방법을 선택해야 하는 경우에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="1c1a3-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="1c1a3-113">EventSource</span></span>
<span data-ttu-id="1c1a3-114">Visual Studio의 템플릿에서 Service Fabric 솔루션을 만들면 **EventSource** 파생 클래스(**ServiceEventSource** 또는 **ActorEventSource**)가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="1c1a3-115">응용 프로그램 또는 서비스에 대한 이벤트를 추가할 수 있는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="1c1a3-116">**EventSource** 이름은 **고유해야** 하며 MyCompany-&lt;solution&gt;-&lt;project&gt; 기본 템플릿 문자열에서 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="1c1a3-117">동일한 이름을 사용하는 **EventSource** 정의가 여러 개 있으면 런타임에서 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="1c1a3-118">정의된 각 이벤트에는 고유 식별자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="1c1a3-119">식별자가 고유하지 않으면 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="1c1a3-120">일부 조직에서는 별도의 개발 팀 간에 충돌을 피하기 위해 식별자에 대한 값의 범위가 미리 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="1c1a3-121">자세한 내용은 [Vance의 블로그](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) 또는 [MSDN 설명서](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="1c1a3-122">구조적 EventSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="1c1a3-122">Using structured EventSource events</span></span>

<span data-ttu-id="1c1a3-123">이 섹션의 코드 예제에 있는 이벤트 각각은 특정 사례(예: 서비스 유형이 등록된 경우)에 대해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="1c1a3-124">사용 사례별로 메시지를 정의할 때 오류 텍스트와 함께 데이터를 패키지할 수 있으며, 지정된 속성의 이름이나 값을 기반으로 하여 보다 쉽게 검색하고 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="1c1a3-125">계측 출력을 구조화하면 더 쉽게 사용할 수 있지만 각 사용 사례마다 새 이벤트를 정의하는 데 더 많은 생각과 시간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="1c1a3-126">일부 이벤트 정의는 전체 응용 프로그램에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="1c1a3-127">예를 들어 메서드 시작 또는 중지 이벤트는 응용 프로그램 내의 많은 서비스에서 다시 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="1c1a3-128">주문 시스템과 같은 도메인 관련 서비스에는 자체의 고유 이벤트를 포함하는 **CreateOrder** 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="1c1a3-129">이 방법은 많은 이벤트를 생성하고 잠재적으로 프로젝트 팀 전체에서 식별자를 조정할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="1c1a3-130">일반적 EventSource 사용</span><span class="sxs-lookup"><span data-stu-id="1c1a3-130">Using EventSource generically</span></span>

<span data-ttu-id="1c1a3-131">특정 이벤트를 정의하는 것이 어려울 수 있기 때문에 많은 사람들이 일반적으로 정보를 문자열로 출력하는 공통 매개 변수 집합을 포함하는 몇 가지 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="1c1a3-132">구조적 측면 대부분이 손실되어 결과를 검색하고 필터링하는 것이 더욱 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="1c1a3-133">이 방법에서는 일반적으로 로깅 수준에 해당하는 몇 가지 이벤트가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="1c1a3-134">다음 코드 조각에서는 디버그 및 오류 메시지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="1c1a3-135">또한 구조적 계측과 일반 계측의 하이브리드를 사용하면 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="1c1a3-136">구조적 계측은 오류 및 메트릭 보고에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="1c1a3-137">일반 이벤트는 문제 해결을 위해 엔지니어가 사용하는 자세한 로깅에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="1c1a3-138">ASP.NET Core 로깅</span><span class="sxs-lookup"><span data-stu-id="1c1a3-138">ASP.NET Core logging</span></span>

<span data-ttu-id="1c1a3-139">코드를 계측하는 방법을 신중하게 계획해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="1c1a3-140">올바른 계측 계획을 사용하면 잠재적인 코드 기반의 불안정을 피한 다음 코드를 다시 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="1c1a3-141">위험을 줄이기 위해 Microsoft ASP.NET Core의 일부인 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)과 같은 계측 라이브러리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="1c1a3-142">ASP.NET Core에는 기존 코드에 미치는 영향을 최소화하면서 선택한 공급자와 함께 사용할 수 있는 [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="1c1a3-143">Windows 및 Linux의 ASP.NET Core 및 전체 .NET Framework의 코드를 사용하여 계측 코드를 표준화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="1c1a3-144">아래에서 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="1c1a3-145">Service Fabric에서 Microsoft.Extensions.Logging 사용</span><span class="sxs-lookup"><span data-stu-id="1c1a3-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="1c1a3-146">Microsoft.Extensions.Logging NuGet 패키지를 계측하려는 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="1c1a3-147">또한 모든 공급자 패키지도 추가합니다(타사 패키지의 경우 다음 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="1c1a3-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="1c1a3-148">자세한 내용은 [ASP.NET Core 로그인](https://docs.microsoft.com/aspnet/core/fundamentals/logging)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="1c1a3-149">'Microsoft.Extensions.Logging'에 대한 **using** 지시문을 서비스 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="1c1a3-150">서비스 클래스 내에 private 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="1c1a3-151">서비스 클래스의 생성자에서 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="1c1a3-152">메서드에서 코드 계측을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="1c1a3-153">다음은 몇 가지 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="1c1a3-154">다른 로깅 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="1c1a3-154">Using other logging providers</span></span>

<span data-ttu-id="1c1a3-155">타사 공급자 중 일부는 [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/) 및 [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)를 포함하여 이전 섹션에서 설명한 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="1c1a3-156">이들 각각을 ASP.NET Core 로깅에 연결하거나 개별적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="1c1a3-157">Serilog에는 로거에서 보낸 모든 메시지를 보강하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="1c1a3-158">이 기능은 서비스 이름, 유형 및 파티션 정보를 출력하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="1c1a3-159">ASP.NET Core 인프라에서 이 기능을 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="1c1a3-160">Serilog, Serilog.Extensions.Logging 및 Serilog.Sinks.Observable NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="1c1a3-161">다음 예제에서는 Serilog.Sinks.Literate도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="1c1a3-162">더 나은 방법은 이 문서의 뒷부분에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="1c1a3-163">Serilog에서 LoggerConfiguration 및 Logger 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="1c1a3-164">Serilog.ILogger 인수를 서비스 생성자에 추가하고 새로 만들어진 로거를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="1c1a3-165">서비스 생성자에서 다음 코드를 추가합니다. 이 예제에서는 서비스의 **ServiceTypeName**, **ServiceName**, **PartitionId** 및 **InstanceId** 속성에 대한 속성 보강자(property enricher)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="1c1a3-166">또한 ASP.NET Core 로깅 팩터리에 속성 보강자를 추가하여 코드에 Microsoft.Extensions.Logging.ILogger를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="1c1a3-167">Serilog 없이 ASP.NET Core를 사용하는 경우와 동일한 코드를 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="1c1a3-168">앞의 예제와 함께 정적 Log.Logger를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="1c1a3-169">Service Fabric은 단일 프로세스 내에서 동일한 서비스 유형의 여러 인스턴스를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="1c1a3-170">정적 Log.Logger를 사용하는 경우 속성 보강자의 마지막 기록기는 실행 중인 모든 인스턴스의 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="1c1a3-171">_logger 변수가 서비스 클래스의 private 멤버 변수가 되는 한 가지 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="1c1a3-172">또한 서비스 전체에서 사용할 수 있는 일반 코드에서 _logger를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="1c1a3-173">로깅 공급자 선택</span><span class="sxs-lookup"><span data-stu-id="1c1a3-173">Choosing a logging provider</span></span>

<span data-ttu-id="1c1a3-174">응용 프로그램이 높은 성능에 의존하는 경우 일반적으로 **EventSource**를 사용하는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="1c1a3-175">**EventSource**는 *일반적으로* ASP.NET Core 로깅이나 사용 가능한 타사 솔루션보다 더 적은 리소스를 사용하는 한편 더 효율적으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="1c1a3-176">이는 대부분의 서비스에서 문제가 되지 않지만, 성능 지향적인 서비스인 경우 **EventSource**를 사용하는 것이 더 나은 선택일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="1c1a3-177">그러나 구조적 로깅과 동일한 이점을 얻으려면 엔지니어링 팀에서 **EventSource**에 많이 투자해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="1c1a3-178">가능하다면 신속하게 몇 가지 로깅 옵션의 프로토타입을 제작하여 요구 사항에 가장 부합하는 것을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c1a3-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c1a3-179">Next steps</span></span>

<span data-ttu-id="1c1a3-180">응용 프로그램 및 서비스를 계측할 로깅 공급자를 선택한 후에는 분석 플랫폼으로 보낼 수 있도록 로그 및 이벤트를 집계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="1c1a3-181">권장 옵션을 더 잘 이해하려면 [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) 및 [WAD](service-fabric-diagnostics-event-aggregation-wad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c1a3-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
