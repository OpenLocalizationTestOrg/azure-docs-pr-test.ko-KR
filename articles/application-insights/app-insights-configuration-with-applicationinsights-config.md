---
title: "ApplicationInsights.config 참조 - Azure | Microsoft Docs"
description: "데이터 수집 모듈을 사용하거나 사용하지 않도록 설정하고 성능 카운터 및 기타 매개 변수를 추가합니다."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="e0336-103">ApplicationInsights.config 또는 .xml로 Application Insights SDK 구성</span><span class="sxs-lookup"><span data-stu-id="e0336-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="e0336-104">Application Insights.NET SDK는  NuGet 패키지의 숫자로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="e0336-105">[코어 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights) Application Insights에 원격 분석을 보내는 경우에 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="e0336-106">[추가 패키지](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)는 해당 컨텍스트 및 응용 프로그램에서 원격 분석을 자동으로 추적하기 위해 원격 분석 *모듈* 및 *이니셜라이저*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="e0336-107">구성 파일을 조정하여 모듈을 활성화하거나 비활성화하고 이 중 일부 모듈의 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="e0336-108">구성 파일의 이름은 응용 프로그램 유형에 따라 `ApplicationInsights.config` 또는 `ApplicationInsights.xml`입니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="e0336-109">[대부분 버전의 SDK는 설치][start]할 때 프로젝트에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="e0336-110">또한 [IIS 서버의 상태 모니터][redfield]에 의해 또는 [Azure 웹사이트 또는 VM에 대한 Appplication Insights 확장](app-insights-azure-web-apps.md)을 선택하는 경우 웹앱에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="e0336-111">[웹 페이지에서 SDK][client]를 제어할 동급의 파일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="e0336-112">이 문서는 구성 파일에서 참조하는 섹션, SDK의 구성 요소를 제어하는 방법 및 해당 구성 요소를 로드하는 NuGet 패키지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="e0336-113">원격 분석 모듈(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0336-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="e0336-114">각 원격 분석 모듈은 특정 형식의 데이터를 수집하고 코어 API를 사용하여 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="e0336-115">모듈은 다른 NuGet 패키지에 의해 설치되며 이는 .config 파일에 필요한 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="e0336-116">각 모듈에 대해 구성 파일에 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="e0336-117">모듈을 사용하지 않으려면 노드를 삭제하거나 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="e0336-118">종속성 추적 </span><span class="sxs-lookup"><span data-stu-id="e0336-118">Dependency Tracking</span></span>
<span data-ttu-id="e0336-119">[종속성 추적](app-insights-asp-net-dependencies.md) 은 앱이 데이터베이스 및 외부 서비스와 데이터베이스에 수행하는 호출에 대한 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="e0336-120">이 모듈이 IIS 서버에서 작동하도록 하려면 [상태 모니터를 설치][redfield]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="e0336-121">Azure 웹앱 또는 VM에서 사용하려면 [Application Insights 확장을 선택](app-insights-azure-web-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="e0336-122">[TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)를 사용하여 종속성 추적 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="e0336-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="e0336-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="e0336-124">성능 수집기</span><span class="sxs-lookup"><span data-stu-id="e0336-124">Performance collector</span></span>
<span data-ttu-id="e0336-125">IIS 설치에서 CPU, 메모리 및 네트워크 부하와 같은 [시스템 성능 카운터를 수집](app-insights-performance-counters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="e0336-126">사용자가 직접 설정한 성능 카운터를 포함하여 어떤 카운터를 수집할지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="e0336-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="e0336-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="e0336-128">Application Insights 진단 원격 분석</span><span class="sxs-lookup"><span data-stu-id="e0336-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="e0336-129">`DiagnosticsTelemetryModule` 은 Application Insights instrumenation 코드 자체에 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="e0336-130">예를 들어 코드가 성능 카운터에 액세스할 수 없는 경우 또는 `ITelemetryInitializer` 를 throw하는 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="e0336-131">이 모듈에서 추적된 원격 분석 추적은 [진단 검색][diagnostic]에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="e0336-132">dc.services.vsallin.net에 진단 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="e0336-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="e0336-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="e0336-134">이 패키지를 설치하는 경우 ApplicationInsights.config 파일은 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="e0336-135">개발자 모드</span><span class="sxs-lookup"><span data-stu-id="e0336-135">Developer Mode</span></span>
<span data-ttu-id="e0336-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`이 Application Insights `TelemetryChannel`를 적용하여 디버거가 응용 프로그램 프로세스에 연결될 때 한번에 원격 분석 항목을 하나씩 즉시 보냅니다. </span><span class="sxs-lookup"><span data-stu-id="e0336-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="e0336-137">응용 프로그램이 원격 분석을 추적할 때와 Application insights 포털에 나타날 때의 간격의 시간차를 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="e0336-138">CPU 및 네트워크 대역폭에 상당한 오버 헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="e0336-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e0336-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="e0336-140">웹 요청 추적</span><span class="sxs-lookup"><span data-stu-id="e0336-140">Web Request Tracking</span></span>
<span data-ttu-id="e0336-141">HTTP 요청의 [응답 시간 및 결과 코드](app-insights-asp-net.md) 를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="e0336-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e0336-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="e0336-143">예외 추적</span><span class="sxs-lookup"><span data-stu-id="e0336-143">Exception tracking</span></span>
<span data-ttu-id="e0336-144">`ExceptionTrackingTelemetryModule` 는 웹앱에서 처리되지 않은 예외를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="e0336-145">[오류 및 예외][exceptions]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0336-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="e0336-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e0336-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="e0336-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - [관찰되지 않은 작업 예외](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="e0336-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 작업자 역할, Windows 서비스 및 콘솔 응용 프로그램에 대한 처리되지 않은 예외를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="e0336-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="e0336-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="e0336-150">EventSource 추적</span><span class="sxs-lookup"><span data-stu-id="e0336-150">EventSource Tracking</span></span>
<span data-ttu-id="e0336-151">`EventSourceTelemetryModule`을 사용하여 Application Insights에 전송될 EventSource 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0336-152">EventSource 이벤트 추적에 대한 자세한 내용은 [EventSource 이벤트 사용](app-insights-asp-net-trace-logs.md#using-eventsource-events)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0336-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="e0336-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="e0336-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="e0336-154">ETW 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="e0336-154">ETW Event Tracking</span></span>
<span data-ttu-id="e0336-155">`EtwCollectorTelemetryModule`을 사용하여 Application Insights에 추적으로 전송할 ETW 공급자의 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0336-156">ETW 이벤트 추적에 대한 자세한 내용은 [ETW 이벤트 사용](app-insights-asp-net-trace-logs.md#using-etw-events)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0336-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="e0336-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="e0336-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="e0336-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="e0336-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="e0336-159">Microsoft.ApplicationInsights 패키지는 SDK의 [코어 API](https://msdn.microsoft.com/library/mt420197.aspx) 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="e0336-160">다른 원격 분석 모듈은 이를 사용하고 사용자 또한 [사용자 고유의 원격 분석을 정의하는 데 사용](app-insights-api-custom-events-metrics.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="e0336-161">ApplicationInsights.config에 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="e0336-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="e0336-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="e0336-163">이 NuGet을 설치하면 .config 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="e0336-164">원격 분석 채널</span><span class="sxs-lookup"><span data-stu-id="e0336-164">Telemetry Channel</span></span>
<span data-ttu-id="e0336-165">원격 분석 채널은 Application Insights 서비스에 대한 원격 분석의 버퍼링 및 전송을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="e0336-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` 는 서비스에 대한 기본 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="e0336-167">메모리에 데이터를 버퍼링합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-167">It buffers data in memory.</span></span>
* <span data-ttu-id="e0336-168">`Microsoft.ApplicationInsights.PersistenceChannel` 는 콘솔 응용 프로그램에 대한 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="e0336-169">앱을 닫을 때 플러시되지 않은 데이터를 영구 저장소로 저장하고 앱이 다시 시작되면 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="e0336-170">원격 분석 이니셜라이저(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0336-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="e0336-171">원격 분석 이니셜라이저는 원격 분석의 모든 항목과 함께 전송되는 컨텍스트 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="e0336-172">[고유한 이니셜라이저를 작성](app-insights-api-filtering-sampling.md#add-properties) 하여 컨텍스트 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="e0336-173">표준 이니셜라이저는 웹 또는 Windows Server NuGet 패키지에서 모두 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="e0336-174">`AccountIdTelemetryInitializer` 는 AccountId 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="e0336-175">`AuthenticatedUserIdTelemetryInitializer`는 JavaScript SDK에서 설정한 AuthenticatedUserId 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="e0336-176">`AzureRoleEnvironmentTelemetryInitializer`은 `RoleName` 및 Azure 런타임 환경에서 추출된 정보를 사용하여 모든 원격 분석 항목에 대해 `Device` 컨텍스트에 대한 `RoleInstance` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="e0336-177">`BuildInfoConfigComponentVersionTelemetryInitializer`은 MS 빌드에 의해 생성된 `BuildInfo.config` 파일로부터 추출된 값을 사용하여 모든 원격 분석 항목에 대한 `Component` 컨텍스트의 `Version` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="e0336-178">`ClientIpHeaderTelemetryInitializer`은 `X-Forwarded-For` HTTP 헤더 기반의 모든 원격 분석 항목의 `Location` 컨텍스트의 `Ip` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="e0336-179">`DeviceTelemetryInitializer`은 모든 원격 분석 항목에 대한 `Device` 컨텍스트의 다음 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="e0336-180">`Type`은 "PC"로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="e0336-181">`Id`은 웹 응용 프로그램이 실행되고 있는 컴퓨터의 도메인 이름으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="e0336-182">`OemName`은 WMI를 사용하여 `Win32_ComputerSystem.Manufacturer` 필드에서 추출된 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="e0336-183">`Model`은 WMI를 사용하여 `Win32_ComputerSystem.Model` 필드에서 추출된 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="e0336-184">`NetworkType`은 `NetworkInterface`에서 추출된 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="e0336-185">`Language`은 `CurrentCulture`의 이름으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="e0336-186">`DomainNameRoleInstanceTelemetryInitializer`은 웹 응용 프로그램이 실행되는 컴퓨터의 도메인 이름을 사용하여 모든 원격 분석 항목에 대해 `Device` 컨텍스트의 `RoleInstance` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="e0336-187">`OperationNameTelemetryInitializer`은 `RequestTelemetry`의 `Name` 속성과 HTTP 메서드를 기반으로 한 모든 원격 분석 아이템의 `Operation` 컨텍스트의 `Name` 속성을 업데이트뿐만 아니라 ASP.NET MVC 컨트롤러와 요청을 처리하는 데 작업을 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="e0336-188">`OperationIdTelemetryInitializer` 또는 `OperationCorrelationTelemetryInitializer`는 자동으로 생성된 `RequestTelemetry.Id`를 사용하여 요청을 처리하는 동안 추적된 모든 원격 분석 항목의 `Operation.Id` 컨텍스트 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="e0336-189">`SessionTelemetryInitializer`은 사용자의 브라우저에서 실행되는 Application Insights JavaScript 계측 코드에 의해 제공된 `ai_session` 쿠키의 추출된 값을 사용하여 모든 원격 분석 항목에 대한 `Session` 컨텍스트의 `Id` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="e0336-190">`SyntheticTelemetryInitializer` 또는 `SyntheticUserAgentTelemetryInitializer`는 가용성 테스트 또는 검색 엔진 봇과 같은 가상 소스에서 요청을 처리하는 경우 모든 원격 분석 항목의 `User`, `Session` 및 `Operation` 컨텍스트 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="e0336-191">기본적으로 [메트릭 탐색기](app-insights-metrics-explorer.md) 는 가상 원격 분석을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="e0336-192">`<Filters>` 는 요청의 식별 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="e0336-193">`UserAgentTelemetryInitializer`은 `User-Agent` HTTP 헤더 기반의 모든 원격 분석 항목의 `User` 컨텍스트의 `UserAgent` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="e0336-194">`UserTelemetryInitializer`은 사용자의 브라우저에서 실행되는 Application insights JavaScript 계측 코드에 의해 제공된 `ai_user` 쿠키의 추출된 값을 사용하여 모든 원격 분석 항목에 대한 `User` 컨텍스트의 `Id` 및 `AcquisitionDate`속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="e0336-195">`WebTestTelemetryInitializer` 는 [가용성 테스트](app-insights-monitor-web-app-availability.md)의 HTTP 요청에 대한 사용자 ID, 세션 ID 및 가상 원본 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="e0336-196">`<Filters>` 는 요청의 식별 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="e0336-197">Service Fabric에서 실행되는 .NET 응용 프로그램에 대해 `Microsoft.ApplicationInsights.ServiceFabric` NuGet 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="e0336-198">이 패키지에는 Service Fabric 속성을 원격 분석 항목에 추가하는 `FabricTelemetryInitializer`가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="e0336-199">자세한 내용은 이 NuGet 패키지에 의해 추가된 속성에 대한 [GitHub 페이지](https://go.microsoft.com/fwlink/?linkid=848457)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0336-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="e0336-200">원격 분석 프로세서(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0336-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="e0336-201">원격 분석 프로세서는 각 원격 분석 항목을 SDK에서 포털에 보내기 전에 필터링하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="e0336-202">[고유한 원격 분석 프로세서를 작성](app-insights-api-filtering-sampling.md#filtering)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="e0336-203">적응 샘플링 원격 분석 프로세서(2.0.0-beta3부터)</span><span class="sxs-lookup"><span data-stu-id="e0336-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="e0336-204">이 옵션은 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-204">This is enabled by default.</span></span> <span data-ttu-id="e0336-205">앱에서 다양한 원격 분석을 보내는 경우 이 프로세서는 일부 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="e0336-206">매개 변수는 알고리즘을 달성하려고 하는 대상을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="e0336-207">SDK의 각 인스턴스가 독립적으로 작동하므로 서버가 여러 컴퓨터의 클러스터인 경우 원격 분석의 실제 볼륨을 적절하게 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="e0336-208">[샘플링에 대해 자세히 알아봅니다](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="e0336-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="e0336-209">고정 비율 샘플링 원격 분석 프로세서(2.0.0-beta1부터)</span><span class="sxs-lookup"><span data-stu-id="e0336-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="e0336-210">또한 표준 [샘플링 원격 분석 프로세서](app-insights-api-filtering-sampling.md) 도 있습니다(2.0.1부터).</span><span class="sxs-lookup"><span data-stu-id="e0336-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="e0336-211">채널 매개 변수(Java)</span><span class="sxs-lookup"><span data-stu-id="e0336-211">Channel parameters (Java)</span></span>
<span data-ttu-id="e0336-212">이러한 매개 변수는 Java SDK가 수집한 원격 분석 데이터를 저장하고 플러시하는 방법에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="e0336-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="e0336-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="e0336-214">SDK의 메모리 내 저장소에 저장할 수 있는 원격 분석 항목의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="e0336-215">이 수에 도달하면 원격 분석 버퍼가 플러시됩니다. 즉, 원격 분석 항목이 Application Insights 서버로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="e0336-216">최소: 1</span><span class="sxs-lookup"><span data-stu-id="e0336-216">Min: 1</span></span>
* <span data-ttu-id="e0336-217">최대: 1000</span><span class="sxs-lookup"><span data-stu-id="e0336-217">Max: 1000</span></span>
* <span data-ttu-id="e0336-218">기본값: 500</span><span class="sxs-lookup"><span data-stu-id="e0336-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="e0336-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="e0336-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="e0336-220">메모리 내 저장소에 저장된 데이터가 플러시될(Application Insights로 보내는) 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="e0336-221">최소: 1</span><span class="sxs-lookup"><span data-stu-id="e0336-221">Min: 1</span></span>
* <span data-ttu-id="e0336-222">최대: 300</span><span class="sxs-lookup"><span data-stu-id="e0336-222">Max: 300</span></span>
* <span data-ttu-id="e0336-223">기본값: 5</span><span class="sxs-lookup"><span data-stu-id="e0336-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="e0336-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="e0336-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="e0336-225">로컬 디스크에서 영구 저장소에 할당되는 최대 크기(MB)를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="e0336-226">이 저장소는 Application Insights 끝점으로 전송하지 못한 원격 분석 항목을 유지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="e0336-227">저장소 크기를 충족하면 새 원격 분석 항목이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="e0336-228">최소: 1</span><span class="sxs-lookup"><span data-stu-id="e0336-228">Min: 1</span></span>
* <span data-ttu-id="e0336-229">최대: 100</span><span class="sxs-lookup"><span data-stu-id="e0336-229">Max: 100</span></span>
* <span data-ttu-id="e0336-230">기본값: 10</span><span class="sxs-lookup"><span data-stu-id="e0336-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="e0336-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="e0336-231">InstrumentationKey</span></span>
<span data-ttu-id="e0336-232">데이터가 표시되는 Application Insights 리소스를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="e0336-233">일반적으로 각 응용 프로그램에 대해 별도 키를 사용하여 별도 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="e0336-234">키를 동적으로 설정하려는 경우, 예를 들어 응용 프로그램의 결과를 다른 리소스로 보내려는 경우 구성 파일에서 키를 생략하고 대신 코드에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="e0336-235">표준 원격 분석 모듈을 비롯한 TelemetryClient의 모든 인스턴스에 대한 키를 설정하려면 TelemetryConfiguration.Active에 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="e0336-236">ASP.NET 서비스의 global.aspx.cs와 같은 초기화 메서드에 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="e0336-237">특정 이벤트 집합을 다른 리소스로 보내려는 경우 특정 TelemetryClient에 대한 키를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0336-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="e0336-238">새 키를 얻으려면 [Application Insights 포털에서 새 리소스를 만듭니다][new].</span><span class="sxs-lookup"><span data-stu-id="e0336-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0336-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0336-239">Next steps</span></span>
<span data-ttu-id="e0336-240">[API에 대해 자세히 알아보세요][api].</span><span class="sxs-lookup"><span data-stu-id="e0336-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
