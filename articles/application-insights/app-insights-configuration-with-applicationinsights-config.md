---
title: "aaaApplicationInsights.config 참조-Azure | Microsoft Docs"
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
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="7b8b7-103">ApplicationInsights.config 또는.xml을 사용 하 여 hello Application Insights SDK를 구성</span><span class="sxs-lookup"><span data-stu-id="7b8b7-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="7b8b7-104">Application Insights.NET SDK hello NuGet 패키지의 번호로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="7b8b7-105">[코어 패키지](http://www.nuget.org/packages/Microsoft.ApplicationInsights) hello Application Insights 원격 분석 보내기 위한 hello API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="7b8b7-106">[추가 패키지](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)는 해당 컨텍스트 및 응용 프로그램에서 원격 분석을 자동으로 추적하기 위해 원격 분석 *모듈* 및 *이니셜라이저*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="7b8b7-107">Hello 구성 파일을 조정 하 여 또는 원격 분석 모듈 및 이니셜라이저를 사용 하지 않도록 설정를 그 중 일부에 대 한 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="7b8b7-108">hello 구성 파일의 이름은 `ApplicationInsights.config` 또는 `ApplicationInsights.xml`hello 유형의 응용 프로그램에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="7b8b7-109">Tooyour는 자동으로 추가 때 프로젝트 있습니다 [대부분 hello SDK의 버전을 설치][start]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="7b8b7-110">Tooa 웹 앱으로도 추가 됩니다 [상태 모니터는 IIS 서버에][redfield], hello Appplication 통찰력을 선택 하면 [Azure 웹 사이트 또는 VM에 대 한 확장](app-insights-azure-web-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="7b8b7-111">해당 하는 파일 toocontrol hello 하지 않으므로 [웹 페이지에는 SDK][client]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="7b8b7-112">이 문서에서는 hello 섹션에에서 나와 있는 hello 구성 파일, SDK, hello의 hello 구성 요소를 제어 하는 방법 및 해당 구성 요소를 로드 하는 NuGet 패키지에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="7b8b7-113">원격 분석 모듈(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="7b8b7-114">각 원격 분석 모듈 특정 형식의 데이터를 수집 하 고 hello 코어 API toosend hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="7b8b7-115">hello 모듈 hello 필요한 선을 toohello.config 파일에 추가 하 여 다른 NuGet 패키지를으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="7b8b7-116">각 모듈에 대 한 hello 구성 파일에는 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="7b8b7-117">모듈의 경우, toodisable hello 노드를 삭제 하거나 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="7b8b7-118">종속성 추적 </span><span class="sxs-lookup"><span data-stu-id="7b8b7-118">Dependency Tracking</span></span>
<span data-ttu-id="7b8b7-119">[종속성 추적](app-insights-asp-net-dependencies.md) toodatabases 및 외부 서비스 및 데이터베이스 응용 프로그램가 호출 하는 방법에 대 한 원격 분석 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="7b8b7-120">tooallow IIS 서버에서이 모듈 toowork, 필요한 너무[상태 모니터 설치][redfield]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="7b8b7-121">toouse Azure 웹 앱 또는 Vm에서 [hello Application Insights 확장 선택](app-insights-azure-web-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="7b8b7-122">사용자 고유의 종속성 hello를 사용 하 여 코드 추적을 작성할 수도 있습니다 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="7b8b7-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="7b8b7-124">성능 수집기</span><span class="sxs-lookup"><span data-stu-id="7b8b7-124">Performance collector</span></span>
<span data-ttu-id="7b8b7-125">IIS 설치에서 CPU, 메모리 및 네트워크 부하와 같은 [시스템 성능 카운터를 수집](app-insights-performance-counters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="7b8b7-126">사용자가 직접 설정한 성능 카운터를 포함 하는 카운터 toocollect를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="7b8b7-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="7b8b7-128">Application Insights 진단 원격 분석</span><span class="sxs-lookup"><span data-stu-id="7b8b7-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="7b8b7-129">hello `DiagnosticsTelemetryModule` hello Application Insights 계측 코드 자체에서 오류를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="7b8b7-130">예를 들어 hello 코드 성능 카운터에 액세스할 수 없는 경우 또는 경우는 `ITelemetryInitializer` 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="7b8b7-131">Hello에이 모듈에서 추적 하는 추적 원격 분석 표시 [진단 검색][diagnostic]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="7b8b7-132">진단 데이터 toodc.services.vsallin.net을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="7b8b7-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="7b8b7-134">만이 패키지를 설치한 경우 hello ApplicationInsights.config 파일이 자동으로 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="7b8b7-135">개발자 모드</span><span class="sxs-lookup"><span data-stu-id="7b8b7-135">Developer Mode</span></span>
<span data-ttu-id="7b8b7-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`강제로 hello Application Insights `TelemetryChannel` toosend 데이터에 즉시 사용 경우 디버거는 한 번에 하나의 원격 분석 항목 toohello 응용 프로그램 프로세스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="7b8b7-137">이렇게 하면 응용 프로그램 원격 분석을 추적 하는 경우 및 hello Application Insights 포털에 표시 되 면 hello hello 순간 사이의 시간 크기를 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="7b8b7-138">CPU 및 네트워크 대역폭에 상당한 오버 헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="7b8b7-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="7b8b7-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="7b8b7-140">웹 요청 추적</span><span class="sxs-lookup"><span data-stu-id="7b8b7-140">Web Request Tracking</span></span>
<span data-ttu-id="7b8b7-141">보고서 hello [응답 시간 및 결과 코드](app-insights-asp-net.md) 의 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="7b8b7-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="7b8b7-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="7b8b7-143">예외 추적</span><span class="sxs-lookup"><span data-stu-id="7b8b7-143">Exception tracking</span></span>
<span data-ttu-id="7b8b7-144">`ExceptionTrackingTelemetryModule` 는 웹앱에서 처리되지 않은 예외를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="7b8b7-145">[오류 및 예외][exceptions]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="7b8b7-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="7b8b7-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="7b8b7-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - [관찰되지 않은 작업 예외](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="7b8b7-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 작업자 역할, Windows 서비스 및 콘솔 응용 프로그램에 대한 처리되지 않은 예외를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="7b8b7-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="7b8b7-150">EventSource 추적</span><span class="sxs-lookup"><span data-stu-id="7b8b7-150">EventSource Tracking</span></span>
<span data-ttu-id="7b8b7-151">`EventSourceTelemetryModule`tooconfigure를 EventSource 이벤트 toobe tooApplication Insights 추적 파일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="7b8b7-152">EventSource 이벤트 추적에 대한 자세한 내용은 [EventSource 이벤트 사용](app-insights-asp-net-trace-logs.md#using-eventsource-events)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="7b8b7-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="7b8b7-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="7b8b7-154">ETW 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="7b8b7-154">ETW Event Tracking</span></span>
<span data-ttu-id="7b8b7-155">`EtwCollectorTelemetryModule`ETW 공급자 toobe tooApplication Insights 추적 파일로 전송에서 tooconfigure 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="7b8b7-156">ETW 이벤트 추적에 대한 자세한 내용은 [ETW 이벤트 사용](app-insights-asp-net-trace-logs.md#using-etw-events)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="7b8b7-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="7b8b7-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="7b8b7-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="7b8b7-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="7b8b7-159">hello Microsoft.ApplicationInsights 패키지 제공 hello [API 핵심](https://msdn.microsoft.com/library/mt420197.aspx) hello SDK의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="7b8b7-160">hello 다른 원격 분석 모듈을 사용 하 여이 및 수도 있습니다 [toodefine를 사용 하 여 사용자 고유의 원격 분석](app-insights-api-custom-events-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="7b8b7-161">ApplicationInsights.config에 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="7b8b7-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="7b8b7-163">이 NuGet을 설치하면 .config 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="7b8b7-164">원격 분석 채널</span><span class="sxs-lookup"><span data-stu-id="7b8b7-164">Telemetry Channel</span></span>
<span data-ttu-id="7b8b7-165">hello 원격 분석 채널에는 버퍼링 및 원격 분석 toohello Application Insights 서비스의 전송을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="7b8b7-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`서비스에 대 한 hello 기본 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="7b8b7-167">메모리에 데이터를 버퍼링합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-167">It buffers data in memory.</span></span>
* <span data-ttu-id="7b8b7-168">`Microsoft.ApplicationInsights.PersistenceChannel` 는 콘솔 응용 프로그램에 대한 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="7b8b7-169">앱을 다운 닫고 hello 앱이 다시 시작 될 때 전송 합니다 어떤 unflushed 데이터 toopersistent 저장소를 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="7b8b7-170">원격 분석 이니셜라이저(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="7b8b7-171">원격 분석 이니셜라이저는 원격 분석의 모든 항목과 함께 전송되는 컨텍스트 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="7b8b7-172">할 수 있습니다 [직접 이니셜라이저 작성](app-insights-api-filtering-sampling.md#add-properties) tooset 컨텍스트 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="7b8b7-173">hello 표준 이니셜라이저 모두 설정 되었습니다. 하거나 hello 웹 또는 windows Server NuGet 패키지:</span><span class="sxs-lookup"><span data-stu-id="7b8b7-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="7b8b7-174">`AccountIdTelemetryInitializer`hello AccountId 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="7b8b7-175">`AuthenticatedUserIdTelemetryInitializer`JavaScript SDK hello 여 세트로 hello AuthenticatedUserId 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="7b8b7-176">`AzureRoleEnvironmentTelemetryInitializer`업데이트 hello `RoleName` 및 `RoleInstance` hello의 속성 `Device` hello Azure 런타임 환경에서 추출한 정보로 모든 원격 분석 항목에 대 한 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="7b8b7-177">`BuildInfoConfigComponentVersionTelemetryInitializer`업데이트 hello `Version` hello 속성 `Component` hello에서 추출한 hello 값으로 모든 원격 분석 항목에 대 한 컨텍스트 `BuildInfo.config` 파일이 하기 위해 Msbuild에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="7b8b7-178">`ClientIpHeaderTelemetryInitializer`업데이트 `Ip` hello 속성 `Location` hello에 따라 모든 원격 분석 항목의 상황에 맞는 `X-Forwarded-For` hello 요청의 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="7b8b7-179">`DeviceTelemetryInitializer`다음과 같은 hello의 속성 업데이트 hello `Device` 모든 원격 분석 항목에 대 한 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="7b8b7-180">`Type`너무 설정 된 "PC"</span><span class="sxs-lookup"><span data-stu-id="7b8b7-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="7b8b7-181">`Id`hello 웹 응용 프로그램이 실행 되 고 있는 hello 컴퓨터의 toohello 도메인 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="7b8b7-182">`OemName`hello에서 추출 된 toohello 값으로 설정 되어 `Win32_ComputerSystem.Manufacturer` WMI를 사용 하 여 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="7b8b7-183">`Model`hello에서 추출 된 toohello 값으로 설정 되어 `Win32_ComputerSystem.Model` WMI를 사용 하 여 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="7b8b7-184">`NetworkType`hello에서 추출 된 toohello 값으로 설정 되어 `NetworkInterface`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="7b8b7-185">`Language`hello toohello 이름이 설정 되어 `CurrentCulture`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="7b8b7-186">`DomainNameRoleInstanceTelemetryInitializer`업데이트 hello `RoleInstance` hello 속성 `Device` hello 웹 응용 프로그램을 실행 중인 hello 컴퓨터의 hello 도메인 이름의 모든 원격 분석 항목에 대 한 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="7b8b7-187">`OperationNameTelemetryInitializer`업데이트 hello `Name` hello 속성 `RequestTelemetry` 및 hello `Name` hello 속성 `Operation` hello HTTP 메서드: ASP.NET MVC 컨트롤러 및 작업 호출 된 tooprocess hello의 이름에 따라 모든 원격 분석 항목의 컨텍스트 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="7b8b7-188">`OperationIdTelemetryInitializer`또는 `OperationCorrelationTelemetryInitializer` 업데이트 hello `Operation.Id` 모든 원격 분석 항목의 컨텍스트 속성이 자동으로 생성 하는 hello로 요청을 처리 하는 동안 추적 `RequestTelemetry.Id`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="7b8b7-189">`SessionTelemetryInitializer`업데이트 hello `Id` hello 속성 `Session` hello에서 추출 된 값을 가진 모든 원격 분석 항목에 대 한 컨텍스트 `ai_session` hello 사용자의 브라우저에서 실행 되는 ApplicationInsights JavaScript 계측 코드 hello 하 여 생성 된 쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="7b8b7-190">`SyntheticTelemetryInitializer`또는 `SyntheticUserAgentTelemetryInitializer` 업데이트 hello `User`, `Session` 및 `Operation` 가용성 테스트 또는 엔진 bot 검색 같은 통합 소스에서 요청을 처리 하는 경우 모든 원격 분석 항목의 컨텍스트 속성을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="7b8b7-191">기본적으로 [메트릭 탐색기](app-insights-metrics-explorer.md) 는 가상 원격 분석을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="7b8b7-192">hello `<Filters>` 설정 hello 요청의 속성을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="7b8b7-193">`UserAgentTelemetryInitializer`업데이트 hello `UserAgent` hello 속성 `User` hello에 따라 모든 원격 분석 항목의 상황에 맞는 `User-Agent` hello 요청의 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="7b8b7-194">`UserTelemetryInitializer`업데이트 hello `Id` 및 `AcquisitionDate` 의 속성 `User` hello에서 추출 된 값이 포함 된 모든 원격 분석 항목에 대 한 컨텍스트 `ai_user` hello hello 실행 되는 Application Insights JavaScript 계측 코드에 의해 생성 된 쿠키 사용자의 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="7b8b7-195">`WebTestTelemetryInitializer`HTTP 요청에서 제공 하는 대 한 사용자 id, 세션 id 및 가상 원본 속성 설정 hello [가용성 테스트](app-insights-monitor-web-app-availability.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="7b8b7-196">hello `<Filters>` 설정 hello 요청의 속성을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="7b8b7-197">서비스 패브릭에서 실행 되는.NET 응용 프로그램에 대 한 hello를 포함할 수 있습니다 `Microsoft.ApplicationInsights.ServiceFabric` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="7b8b7-198">이 패키지에는 `FabricTelemetryInitializer`, 서비스 패브릭 속성 tootelemetry 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="7b8b7-199">자세한 내용은 참조 hello [GitHub 페이지](https://go.microsoft.com/fwlink/?linkid=848457) 이 NuGet 패키지에서 추가 된 hello 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="7b8b7-200">원격 분석 프로세서(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="7b8b7-201">원격 분석 프로세서 필터링 하 고 hello SDK toohello 포털에서 보내기 바로 전에 각 원격 분석 항목을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="7b8b7-202">[고유한 원격 분석 프로세서를 작성](app-insights-api-filtering-sampling.md#filtering)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="7b8b7-203">적응 샘플링 원격 분석 프로세서(2.0.0-beta3부터)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="7b8b7-204">이 옵션은 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-204">This is enabled by default.</span></span> <span data-ttu-id="7b8b7-205">앱에서 다양한 원격 분석을 보내는 경우 이 프로세서는 일부 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="7b8b7-206">알고리즘 hello hello 대상 시도 tooachieve hello 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="7b8b7-207">각 인스턴스의 hello SDK 작업 하지 독립적으로 하므로 hello 실제 양의 원격 분석을 적절 하 게 곱합니다 서버가 여러 대의 컴퓨터의 클러스터 이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="7b8b7-208">[샘플링에 대해 자세히 알아봅니다](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7b8b7-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="7b8b7-209">고정 비율 샘플링 원격 분석 프로세서(2.0.0-beta1부터)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="7b8b7-210">또한 표준 [샘플링 원격 분석 프로세서](app-insights-api-filtering-sampling.md) 도 있습니다(2.0.1부터).</span><span class="sxs-lookup"><span data-stu-id="7b8b7-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="7b8b7-211">채널 매개 변수(Java)</span><span class="sxs-lookup"><span data-stu-id="7b8b7-211">Channel parameters (Java)</span></span>
<span data-ttu-id="7b8b7-212">이러한 매개 변수는 hello Java SDK 해야 저장 방법과 플러시 hello 원격 분석 데이터를 수집 하는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="7b8b7-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="7b8b7-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="7b8b7-214">hello hello SDK의 메모리 내 저장소에 저장 될 수 있는 원격 분석 항목 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="7b8b7-215">이 수에 도달 하면 hello 원격 분석 버퍼 플러시-즉, 원격 분석 항목 hello toohello Application Insights 서버 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="7b8b7-216">최소: 1</span><span class="sxs-lookup"><span data-stu-id="7b8b7-216">Min: 1</span></span>
* <span data-ttu-id="7b8b7-217">최대: 1000</span><span class="sxs-lookup"><span data-stu-id="7b8b7-217">Max: 1000</span></span>
* <span data-ttu-id="7b8b7-218">기본값: 500</span><span class="sxs-lookup"><span data-stu-id="7b8b7-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="7b8b7-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="7b8b7-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="7b8b7-220">얼마나 자주 hello hello 메모리 내 저장소에 저장 된 데이터는 결정 플러시된 (보낸된 tooApplication Insights) 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="7b8b7-221">최소: 1</span><span class="sxs-lookup"><span data-stu-id="7b8b7-221">Min: 1</span></span>
* <span data-ttu-id="7b8b7-222">최대: 300</span><span class="sxs-lookup"><span data-stu-id="7b8b7-222">Max: 300</span></span>
* <span data-ttu-id="7b8b7-223">기본값: 5</span><span class="sxs-lookup"><span data-stu-id="7b8b7-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="7b8b7-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="7b8b7-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="7b8b7-225">Hello mb toohello 영구 저장소 hello 로컬 디스크에 할당 된 최대 크기를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="7b8b7-226">이 저장소에 실패 한 클라이언트 전송 toobe toohello Application Insights 끝점 유지 원격 분석 항목에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="7b8b7-227">Hello 저장소 크기를 충족 하는 경우 새 원격 분석 항목 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="7b8b7-228">최소: 1</span><span class="sxs-lookup"><span data-stu-id="7b8b7-228">Min: 1</span></span>
* <span data-ttu-id="7b8b7-229">최대: 100</span><span class="sxs-lookup"><span data-stu-id="7b8b7-229">Max: 100</span></span>
* <span data-ttu-id="7b8b7-230">기본값: 10</span><span class="sxs-lookup"><span data-stu-id="7b8b7-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="7b8b7-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="7b8b7-231">InstrumentationKey</span></span>
<span data-ttu-id="7b8b7-232">데이터를 표시 하는 hello Application Insights 리소스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="7b8b7-233">일반적으로 각 응용 프로그램에 대해 별도 키를 사용하여 별도 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="7b8b7-234">하려면 tooset hello 키 동적으로-예를 들어 응용 프로그램 toodifferent 리소스-에서 toosend 결과 찾으려는 경우 hello 구성 파일에서 hello 키를 생략 하 고 대신 코드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="7b8b7-235">TelemetryConfiguration.Active hello 키를 설정 하는 표준 원격 분석 모듈을 포함 하 여 TelemetryClient의 모든 인스턴스에 대해 tooset hello 키.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="7b8b7-236">ASP.NET 서비스의 global.aspx.cs와 같은 초기화 메서드에 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="7b8b7-237">Toosend 원하는 이벤트 tooa 다른 리소스의 특정 집합이 이벤트를 특정 TelemetryClient에 대 한 hello 키를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="7b8b7-238">새 키를 tooget [hello Application Insights 포털에서 새 리소스 만들기][new]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b8b7-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b8b7-239">Next steps</span></span>
<span data-ttu-id="7b8b7-240">[Hello API에 대 한 자세한][api]합니다.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
