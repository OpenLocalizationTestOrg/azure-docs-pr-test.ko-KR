---
title: "Application Insights에서 .NET 추적 로그 탐색"
description: "추적, NLog 또는 Log4Net을 사용하여 생성된 로그를 검색합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="e0cf5-103">Application Insights에서 .NET 추적 로그 탐색</span><span class="sxs-lookup"><span data-stu-id="e0cf5-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="e0cf5-104">ASP.NET 응용 프로그램에서 진단 추적에 NLog, log4Net 또는 System.Diagnostics.Trace를 사용하는 경우 [Azure Application Insights][start]로 로그를 보내서 탐색 및 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="e0cf5-105">서비스를 제공하는 각 사용자 요청과 연결된 추적을 식별하고 다른 이벤트 및 예외 보고서와 상호 연결할 수 있도록 로그가 응용 프로그램에서 들어오는 다른 원격 분석과 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="e0cf5-106">로그 캡처 모듈이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="e0cf5-106">Do you need the log capture module?</span></span> <span data-ttu-id="e0cf5-107">타사 로거에 대한 유용한 어댑터지만 NLog, log4Net 또는 System.Diagnostics.Trace를 사용하지 않는 경우 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 를 직접 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="e0cf5-108">앱에 대한 로깅 설치</span><span class="sxs-lookup"><span data-stu-id="e0cf5-108">Install logging on your app</span></span>
<span data-ttu-id="e0cf5-109">프로젝트에서 선택한 로깅 프레임워크를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="e0cf5-110">그러면 app.config 또는 web.config에 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="e0cf5-111">System.Diagnostics.Trace를 사용하는 경우 web.config에 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="e0cf5-112">로그를 수집하도록 Application Insights 구성</span><span class="sxs-lookup"><span data-stu-id="e0cf5-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="e0cf5-113">**[프로젝트에 Application Insights를 추가](app-insights-asp-net.md)**하지 않은 경우 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="e0cf5-114">로그 수집기를 포함하는 옵션이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="e0cf5-115">또는 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하여 **Application Insights를 구성** 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="e0cf5-116">옵션을 **추적 컬렉션 구성**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="e0cf5-117">*Application Insights 메뉴 또는 로그 수집기 옵션이 없습니까?*</span><span class="sxs-lookup"><span data-stu-id="e0cf5-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="e0cf5-118">[문제 해결](#troubleshooting)을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="e0cf5-119">수동 설치</span><span class="sxs-lookup"><span data-stu-id="e0cf5-119">Manual installation</span></span>
<span data-ttu-id="e0cf5-120">프로젝트 형식이 Application Insights 설치 관리자에서 지원되지 않는 경우(예: Windows 데스크톱 프로젝트) 이 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="e0cf5-121">Log4Net 또는 NLog를 사용하려는 경우 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="e0cf5-122">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="e0cf5-123">"Application Insights" 검색</span><span class="sxs-lookup"><span data-stu-id="e0cf5-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="e0cf5-124">다음 패키지 중에서 적절한 패키지를 하나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="e0cf5-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span><span class="sxs-lookup"><span data-stu-id="e0cf5-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="e0cf5-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span><span class="sxs-lookup"><span data-stu-id="e0cf5-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="e0cf5-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span><span class="sxs-lookup"><span data-stu-id="e0cf5-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="e0cf5-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="e0cf5-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="e0cf5-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="e0cf5-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="e0cf5-130">NuGet 패키지는 필요한 어셈블리를 설치하고 web.config 또는 app.config를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="e0cf5-131">진단 로그 호출 삽입</span><span class="sxs-lookup"><span data-stu-id="e0cf5-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="e0cf5-132">System.Diagnostics.Trace를 사용하는 경우 일반적인 호출 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="e0cf5-133">Log4net 또는 NLog를 원할 경우</span><span class="sxs-lookup"><span data-stu-id="e0cf5-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="e0cf5-134">EventSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="e0cf5-134">Using EventSource events</span></span>
<span data-ttu-id="e0cf5-135">Application Insights에 추적으로 보낼 [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0cf5-136">먼저 `Microsoft.ApplicationInsights.EventSourceListener` NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="e0cf5-137">그런 후 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일의 `TelemetryModules` 섹션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="e0cf5-138">각 원본에 대해 다음 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="e0cf5-139">`Name`은 수집할 EventSource의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="e0cf5-140">`Level`은 수집할 로깅 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="e0cf5-141">`Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="e0cf5-142">`Keywords`(선택 사항)는 사용할 키워드 정수 값 조합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="e0cf5-143">DiagnosticSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="e0cf5-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="e0cf5-144">Application Insights에 추적으로 보낼 [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0cf5-145">먼저 [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="e0cf5-146">그런 다음 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일의 `TelemetryModules` 섹션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="e0cf5-147">추적하려는 각 DiagnosticSource에 대해 `Name` 특성 집합이 포함된 항목을 DiagnosticSource 이름에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="e0cf5-148">ETW 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="e0cf5-148">Using ETW events</span></span>
<span data-ttu-id="e0cf5-149">추적으로 Application Insights에 전송될 ETW 이벤트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0cf5-150">먼저 `Microsoft.ApplicationInsights.EtwCollector` NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="e0cf5-151">그런 후 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일의 `TelemetryModules` 섹션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="e0cf5-152">ETW 이벤트는 SDK를 호스트하는 프로세스가 "성능 로그 사용자" 또는 관리자의 구성원인 ID에서 실행되는 경우에만 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="e0cf5-153">각 원본에 대해 다음 매개 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="e0cf5-154">`ProviderName`은 수집할 ETW 공급자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="e0cf5-155">`ProviderGuid`는 `ProviderName` 대신 사용할 수 있는 수집할 ETW 공급자의 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="e0cf5-156">`Level`은 수집할 로깅 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="e0cf5-157">`Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="e0cf5-158">`Keywords`(선택 사항)는 사용할 키워드 정수 값 조합을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="e0cf5-159">직접 추적 API 사용</span><span class="sxs-lookup"><span data-stu-id="e0cf5-159">Using the Trace API directly</span></span>
<span data-ttu-id="e0cf5-160">Application Insights 추적 API를 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="e0cf5-161">로깅 어댑터는 이 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-161">The logging adapters use this API.</span></span>

<span data-ttu-id="e0cf5-162">예:</span><span class="sxs-lookup"><span data-stu-id="e0cf5-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="e0cf5-163">TrackTrace의 장점은 메시지에 상대적으로 긴 데이터를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="e0cf5-164">예를 들어, POST 데이터를 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="e0cf5-165">또한 메시지에 심각도 수준을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="e0cf5-166">또 다른 원격 분석처럼, 다른 추적 집합에 대한 필터링 또는 검색하는 데 사용할 수 있는 속성 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="e0cf5-167">예:</span><span class="sxs-lookup"><span data-stu-id="e0cf5-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="e0cf5-168">이를 통해 [Search][diagnostic]에서 특정 데이터베이스와 관련된 특정 심각도 수준의 모든 메시지를 쉽게 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="e0cf5-169">로그 탐색</span><span class="sxs-lookup"><span data-stu-id="e0cf5-169">Explore your logs</span></span>
<span data-ttu-id="e0cf5-170">디버그 모드에서 앱을 실행하거나 실시간으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="e0cf5-171">[Application Insights 포털][portal]의 앱 개요 블레이드에서 [검색][diagnostic]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Application Insights에서 검색 선택](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![검색](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="e0cf5-174">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-174">You can, for example:</span></span>

* <span data-ttu-id="e0cf5-175">특정 속성이 있는 로그 추적 또는 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="e0cf5-176">특정 항목을 자세히 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="e0cf5-177">동일한 사용자 요청에 관련된, 다시 말해서 OperationId가 같은 다른 원격 분석을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="e0cf5-178">이 페이지의 구성을 즐겨찾기로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="e0cf5-179">**샘플링**</span><span class="sxs-lookup"><span data-stu-id="e0cf5-179">**Sampling.**</span></span> <span data-ttu-id="e0cf5-180">응용 프로그램이 대량의 데이터를 전송하고 ASP.NET 버전 2.0.0-beta3 또는 그 이상에서의 Application Insights SDK를 사용하는 경우 적응 샘플링 기능이 작동하고 원격 분석의 백분율만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="e0cf5-181">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="e0cf5-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0cf5-182">Next steps</span></span>
<span data-ttu-id="e0cf5-183">[ASP.NET의 실패 및 예외 진단][exceptions]</span><span class="sxs-lookup"><span data-stu-id="e0cf5-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="e0cf5-184">[검색에 대한 자세한 정보][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e0cf5-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e0cf5-185">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e0cf5-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="e0cf5-186">Java의 경우 이 작업을 어떻게 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="e0cf5-186">How do I do this for Java?</span></span>
<span data-ttu-id="e0cf5-187">[Java 로그 어댑터](app-insights-java-trace-logs.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="e0cf5-188">프로젝트 상황에 맞는 메뉴에 Application Insights 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="e0cf5-189">Application Insights 도구가 이 개발 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="e0cf5-190">Visual Studio 메뉴 도구, 확장 및 업데이트에서 Application Insights 도구를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="e0cf5-191">설치됨 탭에 없는 경우 온라인 탭을 열고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="e0cf5-192">Application Insights 도구에서 지원되지 않는 프로젝트 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="e0cf5-193">[수동 설치](#manual-installation)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="e0cf5-194">구성 도구에 로그 어댑터 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="e0cf5-195">먼저 로깅 프레임워크를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="e0cf5-196">System.Diagnostics.Trace를 사용하는 경우 [`web.config`에서 구성](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="e0cf5-197">최신 버전의 Application Insights가 있으신가요?</span><span class="sxs-lookup"><span data-stu-id="e0cf5-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="e0cf5-198">Visual Studio **도구** 메뉴에서 **확장 및 업데이트**를 선택하고 **업데이트** 탭을 엽니다. 개발자 분석 도구가 있으면 클릭하여 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="e0cf5-199"><a name="emptykey"></a>"계측 키는 비워 둘 수 없습니다." 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="e0cf5-200">Application Insights를 설치하지 않고 로깅 어댑터 Nuget 패키지를 설치한 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="e0cf5-201">솔루션 탐색기에서 `ApplicationInsights.config` 를 마우스 오른쪽 단추로 클릭하고 **Application Insights 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="e0cf5-202">Azure에 로그인하고 Application Insights 리소스를 만들거나 기존 리소스를 다시 사용하도록 초대하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="e0cf5-203">이 경우 문제가 해결된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="e0cf5-204">진단 검색에 추적은 보이지만 다른 이벤트가 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="e0cf5-205">모든 이벤트와 요청이 파이프라인을 통과할 때까지 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="e0cf5-206"><a name="limits"></a>얼마나 많은 데이터가 보존되나요?</span><span class="sxs-lookup"><span data-stu-id="e0cf5-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="e0cf5-207">여러 가지 요인이 보관되는 데이터의 양에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="e0cf5-208">자세한 내용은 고객 이벤트 메트릭 페이지의 [제한](app-insights-api-custom-events-metrics.md#limits) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="e0cf5-209">예상되는 로그 항목의 일부가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="e0cf5-210">응용 프로그램이 대량의 데이터를 전송하고 ASP.NET 버전 2.0.0-beta3 또는 그 이상에서의 Application Insights SDK를 사용하는 경우 적응 샘플링 기능이 작동하고 원격 분석의 백분율만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="e0cf5-211">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0cf5-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="e0cf5-212"><a name="add"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0cf5-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="e0cf5-213">[가용성 및 응답성 테스트 설정][availability]</span><span class="sxs-lookup"><span data-stu-id="e0cf5-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="e0cf5-214">[문제 해결][qna]</span><span class="sxs-lookup"><span data-stu-id="e0cf5-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
