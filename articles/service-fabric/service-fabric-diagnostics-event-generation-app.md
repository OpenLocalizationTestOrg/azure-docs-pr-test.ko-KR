---
title: "서비스 패브릭 응용 프로그램 수준 모니터링 aaaAzure | Microsoft Docs"
description: "응용 프로그램에 대 한 자세한 내용은 및 서비스 수준 이벤트 및 로그 toomonitor를 사용 하 고 Azure 서비스 패브릭 클러스터를 진단 합니다."
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
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="a29df-103">응용 프로그램 및 서비스 수준 이벤트와 로그 생성</span><span class="sxs-lookup"><span data-stu-id="a29df-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="a29df-104">사용자 지정 이벤트를 사용 하 여 hello 코드 계측</span><span class="sxs-lookup"><span data-stu-id="a29df-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="a29df-105">Hello 코드를 계측는 hello 기반 서비스 모니터링의 대부분의 다른 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="a29df-106">계측 hello 유일한 방법은 인가 잘못 및 고정 toobe 필요한 toodiagnose 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="a29df-107">기술적으로 것은 가능한 tooconnect 디버거 tooa 프로덕션 서비스를 일반적으로 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="a29df-108">따라서 자세한 계측 데이터를 갖는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="a29df-109">일부 제품은 자동으로 코드를 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="a29df-110">이러한 솔루션이 잘 작동할 수 있지만 수동 계측이 거의 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="a29df-111">Hello 끝 hello 응용 프로그램을 디버깅할 충분 한 정보 tooforensically가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="a29df-112">이 문서에서는 두 가지 방법을 tooinstrumenting 사용자 코드와 다른 toochoose 하나 방식 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a29df-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="a29df-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="a29df-113">EventSource</span></span>
<span data-ttu-id="a29df-114">Visual Studio의 템플릿에서 Service Fabric 솔루션을 만들면 **EventSource** 파생 클래스(**ServiceEventSource** 또는 **ActorEventSource**)가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="a29df-115">응용 프로그램 또는 서비스에 대한 이벤트를 추가할 수 있는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="a29df-116">hello **EventSource** 이름 **해야** , 고유 하 고 기본 템플릿 문자열 hello MyCompany-에서 이름을 바꿀 수 해야&lt;솔루션&gt; - &lt; 프로젝트&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="a29df-117">여러 개 있으면 **EventSource** 정의 사용 하는 hello에서 문제 런타임에 동일한 이름 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="a29df-118">정의된 각 이벤트에는 고유 식별자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="a29df-119">식별자가 고유하지 않으면 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="a29df-120">일부 조직에서는 preassign 범위의 값에 대 한 별도 개발 팀 간의 식별자 tooavoid 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="a29df-121">자세한 내용은 참조 [Vance의 블로그](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) 또는 hello [MSDN 설명서](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="a29df-122">구조적 EventSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="a29df-122">Using structured EventSource events</span></span>

<span data-ttu-id="a29df-123">각이 섹션의 hello 코드 예제에서 hello 이벤트에 대해 정의 된 특정 대/소문자, 예를 들어 서비스 종류를 등록 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a29df-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="a29df-124">사용 사례에서 메시지를 정의 하 고 hello 오류의 hello 텍스트와 데이터를 패키지할 수 할 수 있습니다 더 쉽게 검색 하 고 hello 이름 또는 hello의 값을 기준으로 필터 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="a29df-125">Hello 계측 출력 구조 쉽게 tooconsume 있지만 보다 깊은 주의가 필요 있고 toodefine을 각 사용 사례에 대 한 새 이벤트 시간 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="a29df-126">이벤트 정의 만들었다고 hello 전체 응용 프로그램에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="a29df-127">예를 들어 메서드 시작 또는 중지 이벤트는 응용 프로그램 내의 많은 서비스에서 다시 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="a29df-128">주문 시스템과 같은 도메인 관련 서비스에는 자체의 고유 이벤트를 포함하는 **CreateOrder** 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="a29df-129">이 방법은 많은 이벤트를 생성하고 잠재적으로 프로젝트 팀 전체에서 식별자를 조정할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="a29df-130">일반적 EventSource 사용</span><span class="sxs-lookup"><span data-stu-id="a29df-130">Using EventSource generically</span></span>

<span data-ttu-id="a29df-131">특정 이벤트를 정의하는 것이 어려울 수 있기 때문에 많은 사람들이 일반적으로 정보를 문자열로 출력하는 공통 매개 변수 집합을 포함하는 몇 가지 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="a29df-132">대부분 hello 구조적 측면의 손실 된 며 toosearch 및 필터 hello 결과 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="a29df-133">이 방법에서는 일반적으로 toohello 로깅 수준에 해당 하는 몇 가지 이벤트 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="a29df-134">다음 코드 조각 hello 디버그 및 오류 메시지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
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

<span data-ttu-id="a29df-135">또한 구조적 계측과 일반 계측의 하이브리드를 사용하면 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="a29df-136">구조적 계측은 오류 및 메트릭 보고에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="a29df-137">제네릭 이벤트를 자세히 설명 하는 hello에 사용할 수 문제 해결을 위한 엔지니어가 사용 즉 로깅.</span><span class="sxs-lookup"><span data-stu-id="a29df-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="a29df-138">ASP.NET Core 로깅</span><span class="sxs-lookup"><span data-stu-id="a29df-138">ASP.NET Core logging</span></span>

<span data-ttu-id="a29df-139">중요 한 toocarefully 코드를 계측 합니다 방법을 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="a29df-140">hello 오른쪽 계측 계획 코드 베이스를 잠재적으로 불안정 하 고 다음 tooreinstrument hello 코드 필요를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="a29df-141">tooreduce 위험 같은 계측 라이브러리는 선택할 수 있습니다 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), Microsoft ASP.NET Core의 일부인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="a29df-142">ASP.NET Core에는 [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) hello 기존 코드에는 영향을 최소화 하면서 사용자가 선택한 hello 공급자와 함께 사용할 수 있는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="a29df-143">Windows 및 Linux에서 ASP.NET Core hello 코드를 사용할 수 있으며 계측 코드가 표준화 되 되므로 전체.NET Framework hello에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="a29df-144">아래에서 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="a29df-145">Service Fabric에서 Microsoft.Extensions.Logging 사용</span><span class="sxs-lookup"><span data-stu-id="a29df-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="a29df-146">Hello tooinstrument 원하는 Microsoft.Extensions.Logging NuGet 패키지 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="a29df-147">또한 모든 공급자 패키지 추가 (타사 패키지에 대 한 hello 다음 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="a29df-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="a29df-148">자세한 내용은 [ASP.NET Core 로그인](https://docs.microsoft.com/aspnet/core/fundamentals/logging)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a29df-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="a29df-149">추가 **를 사용 하 여** Microsoft.Extensions.Logging tooyour 서비스 파일에 대 한 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="a29df-150">서비스 클래스 내에 private 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="a29df-151">Hello 서비스 클래스의 생성자에서이 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="a29df-152">메서드에서 코드 계측을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="a29df-153">다음은 몇 가지 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="a29df-154">다른 로깅 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="a29df-154">Using other logging providers</span></span>

<span data-ttu-id="a29df-155">일부 타사 공급자 사용 hello 앞 섹션에서에서 설명 하는 hello 방식은 포함 하 여 [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), 및 [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="a29df-156">이들 각각을 ASP.NET Core 로깅에 연결하거나 개별적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="a29df-157">Serilog에는 로거에서 보낸 모든 메시지를 보강하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="a29df-158">이 기능은 유용 toooutput hello 서비스 이름, 형식 및 파티션 정보 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="a29df-159">toouse hello ASP.NET Core 인프라에서에서이 기능은 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="a29df-160">Serilog, Serilog.Extensions.Logging, hello 및 Serilog.Sinks.Observable t toohello 프로젝트 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="a29df-161">Hello 다음 예제에서는 Serilog.Sinks.Literate를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="a29df-162">더 나은 방법은 이 문서의 뒷부분에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="a29df-163">Serilog, LoggerConfiguration 및 hello로 거 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="a29df-164">Serilog.ILogger 인수 toohello 서비스 생성자를 추가 하 고 새로 생성 된로 거 hello를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="a29df-165">Hello 서비스 생성자에서 코드를 만드는 hello hello에 대 한 속성 enrichers 다음 hello 추가 **ServiceTypeName**, **ServiceName**, **PartitionId**, 및  **InstanceId** hello 서비스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="a29df-166">또한 Microsoft.Extensions.Logging.ILogger 코드에서 사용할 수 있도록 속성 enricher toohello ASP.NET Core 로깅 팩터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="a29df-167">계측 hello 코드 hello Serilog 하지 않고 ASP.NET Core를 사용 하는 경우에 따라 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="a29df-168">정적 hello를 사용 하지 않는 것이 좋습니다 Log.Logger 앞 예제는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="a29df-169">서비스 패브릭에서 여러 인스턴스를 호스팅할 수 hello의 단일 프로세스 내에서 형식을 서비스 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="a29df-170">사용 하는 경우 정적 Log.Logger hello, hello 속성 enrichers의 hello 마지막 작성자를 실행 하는 모든 인스턴스에 대 한 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="a29df-171">이것이 이유 hello _logger 변수는 hello 서비스 클래스의 전용 멤버 변수는 한 가지 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="a29df-172">또한 서비스에서 사용할 수 있는 hello _logger toocommon 사용할 수 있는 코드를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="a29df-173">로깅 공급자 선택</span><span class="sxs-lookup"><span data-stu-id="a29df-173">Choosing a logging provider</span></span>

<span data-ttu-id="a29df-174">응용 프로그램이 높은 성능에 의존하는 경우 일반적으로 **EventSource**를 사용하는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="a29df-175">**EventSource** *일반적으로* 더 적은 리소스를 사용 하 고 ASP.NET Core 로깅 또는 hello 사용 가능한 다른 공급 업체 솔루션 보다 더 나은 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="a29df-176">이는 대부분의 서비스에서 문제가 되지 않지만, 성능 지향적인 서비스인 경우 **EventSource**를 사용하는 것이 더 나은 선택일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="a29df-177">그러나 tooget의 이러한 이점을 구조화 된 로깅, **EventSource** 엔지니어링 팀에서 더 큰 투자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="a29df-178">가능 하면 몇 가지 로깅 옵션의 빠른 프로토타입을 수행 하 고 hello 요구에 가장 부합 하는 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a29df-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a29df-179">Next steps</span></span>

<span data-ttu-id="a29df-180">응용 프로그램 및 서비스 로깅 공급자 tooinstrument을 선택 했으면, 로그 및 이벤트 필요 toobe 집계 전에 tooany 분석 플랫폼 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="a29df-181">에 대 한 읽기 [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) 및 [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter hello 권장 옵션 중 일부를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="a29df-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
