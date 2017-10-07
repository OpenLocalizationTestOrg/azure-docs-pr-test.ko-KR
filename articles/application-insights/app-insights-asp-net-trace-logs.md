---
title: "Application Insights에서 aaaExplore.NET 추적 로그"
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
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="5604e-103">Application Insights에서 .NET 추적 로그 탐색</span><span class="sxs-lookup"><span data-stu-id="5604e-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="5604e-104">전송 로그 점이 NLog, log4Net 또는 System.Diagnostics.Trace ASP.NET 응용 프로그램에서 진단 추적을 위해 사용 하는 경우[Azure Application Insights][start], 탐색 하 고 수 있는 검색 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="5604e-105">로그를 다른 hello로 병합 될 원격 분석을 식별할 수 있도록 응용 프로그램에서 들어오는 hello 각 사용자 요청을 서비스와 관련 된 추적 및 상관 관계 다른 이벤트와 예외 보고서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="5604e-106">Hello 로그 캡처 모듈 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="5604e-106">Do you need hello log capture module?</span></span> <span data-ttu-id="5604e-107">타사 로거에 대한 유용한 어댑터지만 NLog, log4Net 또는 System.Diagnostics.Trace를 사용하지 않는 경우 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 를 직접 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="5604e-108">앱에 대한 로깅 설치</span><span class="sxs-lookup"><span data-stu-id="5604e-108">Install logging on your app</span></span>
<span data-ttu-id="5604e-109">프로젝트에서 선택한 로깅 프레임워크를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="5604e-110">그러면 app.config 또는 web.config에 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="5604e-111">System.Diagnostics.Trace를 사용 하는 항목 tooweb.config tooadd가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="5604e-112">Application Insights toocollect 로그 구성</span><span class="sxs-lookup"><span data-stu-id="5604e-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="5604e-113">**[Application Insights tooyour 프로젝트 추가](app-insights-asp-net.md)**  하는 작업을 아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="5604e-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="5604e-114">옵션 tooinclude hello 로그 수집기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="5604e-115">또는 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하여 **Application Insights를 구성** 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="5604e-116">Hello 옵션을 너무 선택**추적 수집을 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="5604e-117">*Application Insights 메뉴 또는 로그 수집기 옵션이 없습니까?*</span><span class="sxs-lookup"><span data-stu-id="5604e-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="5604e-118">[문제 해결](#troubleshooting)을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5604e-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="5604e-119">수동 설치</span><span class="sxs-lookup"><span data-stu-id="5604e-119">Manual installation</span></span>
<span data-ttu-id="5604e-120">프로젝트 형식 hello Application Insights 설치 관리자 (예를 들어 Windows 데스크톱 프로젝트)에서 지원 되지 않는 경우이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="5604e-121">Toouse log4Net 또는 NLog를 하려는 경우 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="5604e-122">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="5604e-123">"Application Insights" 검색</span><span class="sxs-lookup"><span data-stu-id="5604e-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="5604e-124">중 적절 한 패키지-hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="5604e-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace 호출)</span><span class="sxs-lookup"><span data-stu-id="5604e-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="5604e-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource 이벤트)</span><span class="sxs-lookup"><span data-stu-id="5604e-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="5604e-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW 이벤트)</span><span class="sxs-lookup"><span data-stu-id="5604e-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="5604e-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="5604e-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="5604e-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="5604e-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="5604e-130">hello NuGet 패키지는 hello 필요한 어셈블리를 설치 하 고 web.config 또는 app.config도 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="5604e-131">진단 로그 호출 삽입</span><span class="sxs-lookup"><span data-stu-id="5604e-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="5604e-132">System.Diagnostics.Trace를 사용하는 경우 일반적인 호출 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="5604e-133">Log4net 또는 NLog를 원할 경우</span><span class="sxs-lookup"><span data-stu-id="5604e-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="5604e-134">EventSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="5604e-134">Using EventSource events</span></span>
<span data-ttu-id="5604e-135">구성할 수 있습니다 [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 이벤트 전송 toobe tooApplication Insights로 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="5604e-136">먼저, hello 설치 `Microsoft.ApplicationInsights.EventSourceListener` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="5604e-137">다음 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="5604e-138">각 원본에 대 한 매개 변수 뒤 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="5604e-139">`Name`hello EventSource toocollect hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="5604e-140">`Level`로깅 수준 toocollect hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="5604e-141">`Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="5604e-142">`Keywords`(선택 사항) 키워드 조합 toouse의 hello 정수 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="5604e-143">DiagnosticSource 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="5604e-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="5604e-144">구성할 수 있습니다 [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) 이벤트 전송 toobe tooApplication Insights로 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="5604e-145">먼저, hello 설치 [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="5604e-146">다음 hello 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="5604e-147">원하는 tootrace, 각 DiagnosticSource에 대 한 hello로 항목을 추가 `Name` 특성 프로그램 DiagnosticSource의 toohello 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="5604e-148">ETW 이벤트 사용</span><span class="sxs-lookup"><span data-stu-id="5604e-148">Using ETW events</span></span>
<span data-ttu-id="5604e-149">TooApplication Insights 추적으로 전송 하는 ETW 이벤트 toobe를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="5604e-150">먼저, hello 설치 `Microsoft.ApplicationInsights.EtwCollector` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="5604e-151">다음 편집 `TelemetryModules` hello 섹션 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="5604e-152">ETW 이벤트 hello 프로세스 호스팅 hello SDK "Performance Log Users" 또는 관리자의 구성원 인 id에서 실행 중인 경우에 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="5604e-153">각 원본에 대 한 매개 변수 뒤 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="5604e-154">`ProviderName`hello ETW 공급자 toocollect hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="5604e-155">`ProviderGuid`대신 사용할 수 hello hello ETW 공급자 toocollect의 GUID를 지정 `ProviderName`합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="5604e-156">`Level`로깅 수준 toocollect hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="5604e-157">`Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning` 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="5604e-158">`Keywords`(선택 사항) 집합 hello 키워드 조합 toouse의 정수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="5604e-159">Hello 추적 API를 직접 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5604e-159">Using hello Trace API directly</span></span>
<span data-ttu-id="5604e-160">Hello Application Insights 추적 API를 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="5604e-161">이 API를 사용 하는 hello 로깅 어댑터.</span><span class="sxs-lookup"><span data-stu-id="5604e-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="5604e-162">예:</span><span class="sxs-lookup"><span data-stu-id="5604e-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="5604e-163">TrackTrace 경우의 이점은 hello 메시지에 상대적으로 긴 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="5604e-164">예를 들어, POST 데이터를 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="5604e-165">또한, 심각도 수준 tooyour 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="5604e-166">와 같은 다른 원격 분석 toohelp 필터 또는 다른 집합이 추적에 대 한 검색 사용할 수 있는 속성 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="5604e-167">예:</span><span class="sxs-lookup"><span data-stu-id="5604e-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="5604e-168">이 사용 하면에서 [검색][diagnostic], tooeasily tooa 특정 데이터베이스와 관련 된 특정 심각도 수준의 모든 hello 메시지를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="5604e-169">로그 탐색</span><span class="sxs-lookup"><span data-stu-id="5604e-169">Explore your logs</span></span>
<span data-ttu-id="5604e-170">디버그 모드에서 앱을 실행하거나 실시간으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="5604e-171">응용 프로그램의 개요 블레이드에서 [hello Application Insights 포털][portal], 선택 [검색][diagnostic]합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Application Insights에서 검색 선택](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![검색](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="5604e-174">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-174">You can, for example:</span></span>

* <span data-ttu-id="5604e-175">특정 속성이 있는 로그 추적 또는 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="5604e-176">특정 항목을 자세히 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="5604e-177">Toohello와 관련 된 다른 원격 분석 찾기 같은 사용자 요청 (즉,와 동일한를 hello OperationId)</span><span class="sxs-lookup"><span data-stu-id="5604e-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="5604e-178">이 페이지의 hello 구성 즐겨찾기로 저장</span><span class="sxs-lookup"><span data-stu-id="5604e-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="5604e-179">**샘플링**</span><span class="sxs-lookup"><span data-stu-id="5604e-179">**Sampling.**</span></span> <span data-ttu-id="5604e-180">이상에 대 한 ASP.NET 버전 2.0.0-beta3 hello Application Insights SDK를 사용 하는 응용 프로그램에서 많은 양의 데이터를 hello 적응 샘플링 기능이 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="5604e-181">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="5604e-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5604e-182">Next steps</span></span>
<span data-ttu-id="5604e-183">[ASP.NET의 실패 및 예외 진단][exceptions]</span><span class="sxs-lookup"><span data-stu-id="5604e-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="5604e-184">[검색에 대한 자세한 정보][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="5604e-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5604e-185">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5604e-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="5604e-186">Java의 경우 이 작업을 어떻게 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="5604e-186">How do I do this for Java?</span></span>
<span data-ttu-id="5604e-187">사용 하 여 hello [Java 로그 어댑터](app-insights-java-trace-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="5604e-188">Hello 프로젝트 상황에 맞는 메뉴에서 Application Insights 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="5604e-189">Application Insights 도구가 이 개발 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="5604e-190">Visual Studio 메뉴 도구, 확장 및 업데이트에서 Application Insights 도구를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="5604e-191">Hello 설치 됨 탭에 없으면 온라인 hello 탭을 열고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="5604e-192">Application Insights 도구에서 지원되지 않는 프로젝트 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="5604e-193">[수동 설치](#manual-installation)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="5604e-194">Hello 구성 도구에서 로그 어댑터 옵션 없음</span><span class="sxs-lookup"><span data-stu-id="5604e-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="5604e-195">먼저 tooinstall hello 로깅 프레임 워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="5604e-196">System.Diagnostics.Trace를 사용하는 경우 [`web.config`에서 구성](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="5604e-197">Application Insights의 최신 버전 hello 있죠?</span><span class="sxs-lookup"><span data-stu-id="5604e-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="5604e-198">Visual Studio에서 **도구** 메뉴 선택 **확장명 및 업데이트**, 및 열기 hello **업데이트** 탭 합니다. 개발자 분석 도구 중지 되지 않은 경우, 클릭 tooupdate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="5604e-199"><a name="emptykey"></a>"계측 키는 비워 둘 수 없습니다." 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="5604e-200">Application Insights를 설치 하지 않고 어댑터 Nuget 패키지 로깅 hello 설치한 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="5604e-201">솔루션 탐색기에서 `ApplicationInsights.config` 를 마우스 오른쪽 단추로 클릭하고 **Application Insights 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="5604e-202">TooAzure 안에 toosign 초대 하는 대화 상자를 얻을 수 및 Application Insights 리소스를 만들거나 기존 집합을 다시 사용 하거나 합니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="5604e-203">이 경우 문제가 해결된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="5604e-204">추적을 진단 검색에서 확인할 수는 있지만 다른 이벤트를 hello 하지</span><span class="sxs-lookup"><span data-stu-id="5604e-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="5604e-205">경우에 따라 모든 hello 이벤트 및 요청 tooget hello 파이프라인을 통해 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="5604e-206"><a name="limits"></a>얼마나 많은 데이터가 보존되나요?</span><span class="sxs-lookup"><span data-stu-id="5604e-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="5604e-207">보관 되는 데이터 양을 hello 영향을 주는 몇 가지 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="5604e-208">Hello 참조 [제한](app-insights-api-custom-events-metrics.md#limits) hello 고객 이벤트 메트릭 페이지에 대 한 자세한 내용은의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="5604e-209">예상 hello 로그 항목 일부는 표시 되지 않는</span><span class="sxs-lookup"><span data-stu-id="5604e-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="5604e-210">이상에 대 한 ASP.NET 버전 2.0.0-beta3 hello Application Insights SDK를 사용 하는 응용 프로그램에서 많은 양의 데이터를 hello 적응 샘플링 기능이 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="5604e-211">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5604e-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="5604e-212"><a name="add"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="5604e-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="5604e-213">[가용성 및 응답성 테스트 설정][availability]</span><span class="sxs-lookup"><span data-stu-id="5604e-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="5604e-214">[문제 해결][qna]</span><span class="sxs-lookup"><span data-stu-id="5604e-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
