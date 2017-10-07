---
title: "사용자 지정 이벤트 및 메트릭을 대 한 인 사이트 API aaaApplication | Microsoft Docs"
description: "장치 또는 데스크톱 응용 프로그램, 웹 페이지 또는 서비스에 tootrack 사용량에 몇 줄의 코드를 삽입 하 고 문제를 진단 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="dcaa2-103">사용자 지정 이벤트 및 메트릭용 Application Insights API</span><span class="sxs-lookup"><span data-stu-id="dcaa2-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="dcaa2-104">프로그램 응용 프로그램 toofind, 사용자가 수행 하는 아웃에 몇 줄의 코드를 넣거나 toohelp 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="dcaa2-105">장치 및 데스크톱 앱, 웹 클라이언트, 웹 서버에서 원격 분석을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="dcaa2-106">사용 하 여 hello [Azure Application Insights](app-insights-overview.md) 원격 분석 API toosend 사용자 지정 이벤트 및 메트릭 및 사용자가 자체 버전 표준 원격 분석의 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="dcaa2-107">이 API는 동일한 API Application Insights 데이터 수집기를 사용 하 여 hello 표준에 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="dcaa2-108">API 요약</span><span class="sxs-lookup"><span data-stu-id="dcaa2-108">API summary</span></span>
<span data-ttu-id="dcaa2-109">hello API는 몇 가지 작은 변형 외에도 모든 플랫폼에 걸쳐 균일 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="dcaa2-110">메서드</span><span class="sxs-lookup"><span data-stu-id="dcaa2-110">Method</span></span> | <span data-ttu-id="dcaa2-111">용도</span><span class="sxs-lookup"><span data-stu-id="dcaa2-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="dcaa2-112">페이지, 화면, 블레이드 또는 양식.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="dcaa2-113">사용자 작업 및 기타 이벤트.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-113">User actions and other events.</span></span> <span data-ttu-id="dcaa2-114">Tootrack 사용자 동작 또는 toomonitor 성능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="dcaa2-115">큐 길이 같은 성능 측정 toospecific 이벤트와 무관 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="dcaa2-116">진단 예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="dcaa2-117">추적 관계 tooother 이벤트에서 발생 및 스택 추적을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="dcaa2-118">Hello 빈도 / 기간 서버 요청의 성능 분석에 대 한 로깅을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="dcaa2-119">진단 로그 메시지.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-119">Diagnostic log messages.</span></span> <span data-ttu-id="dcaa2-120">타사 로그도 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="dcaa2-121">Hello 기간 및 빈도 응용 프로그램에 의존 하는 호출 tooexternal 구성 요소의 로깅을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="dcaa2-122">할 수 있습니다 [연결 속성 및 메트릭을](#properties) toomost 이러한 원격 분석 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="dcaa2-123"><a name="prep"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="dcaa2-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="dcaa2-124">Application Insights SDK에 대한 참조가 아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="dcaa2-125">Hello Application Insights SDK tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="dcaa2-126">ASP.NET 프로젝트</span><span class="sxs-lookup"><span data-stu-id="dcaa2-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="dcaa2-127">Java 프로젝트</span><span class="sxs-lookup"><span data-stu-id="dcaa2-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="dcaa2-128">각 웹 페이지의 JavaScript</span><span class="sxs-lookup"><span data-stu-id="dcaa2-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="dcaa2-129">장치 또는 웹 서버 코드에 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="dcaa2-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="dcaa2-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="dcaa2-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="dcaa2-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="dcaa2-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="dcaa2-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="dcaa2-133">TelemetryClient 인스턴스 생성</span><span class="sxs-lookup"><span data-stu-id="dcaa2-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="dcaa2-134">`TelemetryClient`의 인스턴스를 생성합니다(웹 페이지의 JavaScript는 제외).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="dcaa2-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="dcaa2-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="dcaa2-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="dcaa2-138">TelemetryClient는 스레드로부터 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="dcaa2-139">앱의 각 모듈에 대해 TelemetryClient 인스턴스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="dcaa2-140">예를 들어, 웹 서비스 tooreport 들어오는 HTTP 요청을 받은 및 미들웨어 클래스 tooreport 비즈니스 논리 이벤트에서 다른 TelemetryClient 인스턴스 하나를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="dcaa2-141">와 같은 속성을 설정할 수 있습니다 `TelemetryClient.Context.User.Id` tootrack 사용자와 세션, 또는 `TelemetryClient.Context.Device.Id` tooidentify hello 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="dcaa2-142">이 정보는 hello 인스턴스 전송 하는 연결 된 tooall 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="dcaa2-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="dcaa2-143">TrackEvent</span></span>
<span data-ttu-id="dcaa2-144">Application Insights에서 *사용자 지정 이벤트*는 [메트릭 탐색기](app-insights-metrics-explorer.md)에 집계된 개수로 표시하고 [진단 검색](app-insights-diagnostic-search.md)에 개별 항목으로 표시할 수 있는 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="dcaa2-145">(관련된 tooMVC 또는 다른 프레임 워크 "이벤트입니다." 하지)</span><span class="sxs-lookup"><span data-stu-id="dcaa2-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="dcaa2-146">삽입 `TrackEvent` 코드 toocount의 다양 한 이벤트를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="dcaa2-147">사용자가 특정 기능을 얼마나 자주 선택하는지, 특정 목표를 얼마나 자주 달성하는지 또는 특정 유형의 실수를 얼마나 자주 하는지를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="dcaa2-148">예를 들어 게임 응용 프로그램에서 사용자 hello 승리는 이벤트를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="dcaa2-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="dcaa2-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="dcaa2-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="dcaa2-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="dcaa2-153">Hello Microsoft Azure 포털에서 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="dcaa2-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="dcaa2-154">사용자 이벤트의 개수 toosee 열고는 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드에서 새 차트를 추가 하 고 선택 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![사용자 지정 이벤트 수 보기](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="dcaa2-156">다른 이벤트의 toocompare hello 횟수 hello 차트 종류를 너무 설정**그리드**, 이벤트 이름으로 그룹화 하 고:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Hello 차트 종류와 그룹화를 설정 합니다.](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="dcaa2-158">Hello 표에서 이벤트 이름 toosee의 개별 항목에 해당 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="dcaa2-159">toosee는 hello 목록에서 임의의 발생 항목 클릭 자세히-자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-159">toosee more detail - click any occurrence in hello list.</span></span>

![Hello 이벤트 드릴스루](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="dcaa2-161">관심이 있는 집합 hello 블레이드 필터 toohello 이벤트 이름 검색 또는 메트릭 탐색기에서 특정 이벤트에 toofocus:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![필터를 열고 이벤트 이름을 확장한 다음 하나 이상의 값을 선택합니다.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="dcaa2-163">분석의 사용자 지정 이벤트</span><span class="sxs-lookup"><span data-stu-id="dcaa2-163">Custom events in Analytics</span></span>

<span data-ttu-id="dcaa2-164">hello 원격 분석은 hello에서 사용할 수 있는 `customEvents` 테이블에 [응용 프로그램 통찰력 분석](app-insights-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="dcaa2-165">각 행 너무 대 한 호출을 나타내는`trackEvent(..)` 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="dcaa2-166">경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="dcaa2-167">예제 itemCount는 10 개의 호출이 tootrackEvent()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="dcaa2-168">사용자 지정 이벤트의 정확한 개수 tooget 사용 해야 하므로와 같은 사용 가능한 코드 `customEvent | summarize sum(itemCount)`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="dcaa2-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="dcaa2-169">TrackMetric</span></span>

<span data-ttu-id="dcaa2-170">Application Insights에 연결 된 tooparticular 이벤트가 메트릭을 차트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="dcaa2-171">예를 들어 정기적으로 큐 길이를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="dcaa2-172">메트릭을 사용 하 여 hello 개별 측정 하는 hello 변형 및 추세를 보다 작음 관심 되며 따라서 통계 차트 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="dcaa2-173">toosend 메트릭 tooApplication Insights 순서, hello를 사용할 수 있습니다 `TrackMetric(..)` API입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="dcaa2-174">두 가지 방법으로 toosend 메트릭</span><span class="sxs-lookup"><span data-stu-id="dcaa2-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="dcaa2-175">단일 값.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-175">Single value.</span></span> <span data-ttu-id="dcaa2-176">응용 프로그램에서 측정 한 값을 수행할 때마다 해당 값 hello tooApplication Insights 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="dcaa2-177">예를 들어 hello 컨테이너의 항목 수를 설명 하는 메트릭이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="dcaa2-178">특정 기간 동안 hello 컨테이너에 처음 세 개의 품목을 넣은 하 고 그런 다음 두 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="dcaa2-179">호출 하는 것이 그에 따라, `TrackMetric` 두 번: hello 값을 전달 하는 먼저 `3` 다음 값을 hello 및 `-2`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="dcaa2-180">Application Insights는 두 값을 자동으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="dcaa2-181">집계.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-181">Aggregation.</span></span> <span data-ttu-id="dcaa2-182">메트릭을 사용하여 작업하는 경우 모든 단일 측정값은 거의 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="dcaa2-183">대신 특정 기간 동안 발생한 내용의 요약이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="dcaa2-184">이러한 요약을 _집계_라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="dcaa2-185">위 예제는 hello, hello 해당 기간에 대 한 집계 메트릭 합계는 `1` hello hello 메트릭 값 개수 이며 `2`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="dcaa2-186">Hello 집계 방법을 사용할 때는 호출 하면 `TrackMetric` 시간 기간 및 송신 hello 집계 값 마다 한 번씩입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="dcaa2-187">이 hello 권장 접근법 hello 비용을 크게 줄일 수 있고 성능 오버 헤드가 적은 데이터를 보내 여전히 모든 관련 정보를 수집 하는 동안 tooApplication 통찰력을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="dcaa2-188">예제:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="dcaa2-189">단일 값</span><span class="sxs-lookup"><span data-stu-id="dcaa2-189">Single values</span></span>

<span data-ttu-id="dcaa2-190">toosend 단일 메트릭 값:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-190">toosend a single metric value:</span></span>

<span data-ttu-id="dcaa2-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="dcaa2-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="dcaa2-193">메트릭 집계</span><span class="sxs-lookup"><span data-stu-id="dcaa2-193">Aggregating metrics</span></span>

<span data-ttu-id="dcaa2-194">응용 프로그램, tooreduce 대역폭, 비용 및 tooimprove 성능에서 보내기 전에 tooaggregate 메트릭을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="dcaa2-195">다음은 집계 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="dcaa2-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="dcaa2-197">메트릭 탐색기의 사용자 지정 메트릭</span><span class="sxs-lookup"><span data-stu-id="dcaa2-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="dcaa2-198">toosee hello 결과 메트릭 탐색기를 열고 새 차트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="dcaa2-199">프로그램 메트릭을 hello 차트 tooshow를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="dcaa2-200">사용자의 사용자 지정 메트릭을 사용 가능한 메트릭 hello 목록에서 몇 분 tooappear를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![새 차트를 추가하거나 차트를 선택하고, 사용자 지정 아래에서 메트릭을 선택합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="dcaa2-202">분석의 사용자 지정 메트릭</span><span class="sxs-lookup"><span data-stu-id="dcaa2-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="dcaa2-203">hello 원격 분석은 hello에서 사용할 수 있는 `customMetrics` 테이블에 [응용 프로그램 통찰력 분석](app-insights-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="dcaa2-204">각 행 너무 대 한 호출을 나타내는`trackMetric(..)` 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="dcaa2-205">`valueSum`-이 hello 측정 hello 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="dcaa2-206">tooget hello 평균 값으로 나누기 `valueCount`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="dcaa2-207">`valueCount`-이에 집계 된 단위 수를 hello `trackMetric(..)` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="dcaa2-208">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="dcaa2-208">Page views</span></span>
<span data-ttu-id="dcaa2-209">장치 또는 웹 페이지 앱에서 각 화면 또는 페이지가 로드되면 기본적으로 페이지 보기 원격 분석이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="dcaa2-210">하지만 또는 다른 시간에 해당 tootrack 페이지 뷰를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="dcaa2-211">예를 들어, 탭 또는 블레이드를 표시 하는 응용 프로그램에 수 tootrack 페이지 때마다 원하는 hello 사용자는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![개요 블레이드의 사용 현황 렌즈](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="dcaa2-213">사용자 및 세션 데이터는 페이지 보기와 함께 속성 페이지 보기 원격 분석 때 생기는 사용자 및 세션 차트를 따라서 hello으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="dcaa2-214">사용자 지정 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="dcaa2-214">Custom page views</span></span>
<span data-ttu-id="dcaa2-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="dcaa2-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="dcaa2-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="dcaa2-218">여러 HTML 페이지 내에서 여러 탭이 있는 경우 너무 hello URL을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="dcaa2-219">페이지 보기 시간</span><span class="sxs-lookup"><span data-stu-id="dcaa2-219">Timing page views</span></span>
<span data-ttu-id="dcaa2-220">기본적으로 hello 번으로 보고 **페이지 보기 로드 시간** hello 브라우저 hello 브라우저 페이지 로드 이벤트를 호출할 때까지 hello 요청을 보낼 때에서 측정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="dcaa2-221">대신, 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-221">Instead, you can either:</span></span>

* <span data-ttu-id="dcaa2-222">Hello에 명시적 기간 설정 [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) 호출: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="dcaa2-223">Hello 페이지 보기 타이밍 호출을 사용 하 여 `startTrackPage` 및 `stopTrackPage`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="dcaa2-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="dcaa2-225">...</span><span class="sxs-lookup"><span data-stu-id="dcaa2-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="dcaa2-226">hello hello 첫 번째 매개 변수 연결 hello 시작으로를 사용 하는 이름 및 호출을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="dcaa2-227">현재 페이지 이름 toohello 기본값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="dcaa2-228">메트릭 탐색기에 표시 된 기간 사이의 hello hello 간격에서 파생 된 hello 결과 페이지 로드 시작 및 호출을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="dcaa2-229">가 tooyou 실제로 시간 어떤 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="dcaa2-230">분석의 페이지 원격 분석</span><span class="sxs-lookup"><span data-stu-id="dcaa2-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="dcaa2-231">[분석](app-insights-analytics.md)에서 두 테이블이 브라우저 작업의 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="dcaa2-232">hello `pageViews` hello URL 및 페이지 제목에 대 한 데이터를 포함 하는 테이블</span><span class="sxs-lookup"><span data-stu-id="dcaa2-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="dcaa2-233">hello `browserTimings` hello에 걸린 시간 tooprocess hello 들어오는 데이터와 같은 클라이언트 성능에 대 한 데이터 테이블에 포함</span><span class="sxs-lookup"><span data-stu-id="dcaa2-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="dcaa2-234">toofind hello 브라우저 사용 시간이 얼마나 걸리는지 tooprocess 서로 다른 페이지:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="dcaa2-235">다양 한 브라우저의 toodiscover hello popularities:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="dcaa2-236">종속성이 있는 tooassociate 페이지 뷰 tooAJAX 호출에 가입 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="dcaa2-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="dcaa2-237">TrackRequest</span></span>
<span data-ttu-id="dcaa2-238">hello 서버 SDK TrackRequest toolog HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="dcaa2-239">호출할 수 있습니다도 직접 컨텍스트에서 요청을 toosimulate 없는 hello 웹 서비스 모듈이 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="dcaa2-240">그러나 hello 권장 방법은 toosend 요청 원격 분석은 hello 요청 역할도 <a href="#operation-context">작업 컨텍스트</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="dcaa2-241">작업 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="dcaa2-241">Operation context</span></span>
<span data-ttu-id="dcaa2-242">일반적인 Operationid toothem 연결 하 여 원격 분석 항목을 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="dcaa2-243">기본 요청 추적 모듈이 hello 예외 및 HTTP 요청을 처리 하는 동안 전송 된 다른 이벤트에 대해 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="dcaa2-244">[검색](app-insights-diagnostic-search.md) 및 [분석](app-insights-analytics.md), hello ID tooeasily 찾기 hello 요청과 관련 된 모든 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="dcaa2-245">이 패턴을 사용 하 여 tooset 작업 컨텍스트를가 하는 hello 가장 쉬운 방법은 tooset hello ID:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="dcaa2-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="dcaa2-247">작업 컨텍스트를 설정 하는 함께 `StartOperation` 지정 하는 hello 유형의 원격 분석 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="dcaa2-248">보내는 hello 원격 분석 항목 hello 작업을 삭제 하거나 명시적으로 호출 하는 경우 `StopOperation`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="dcaa2-249">사용 하는 경우 `RequestTelemetry` 지속 시간이 toohello 간격 시작 및 중지 hello 원격 분석 유형으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="dcaa2-250">작업 컨텍스트는 중첩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="dcaa2-251">컨텍스트가 이미 있는 작업, 경우 해당 ID는 연결 된 모든 hello 포함 된 항목을 사용 하 여 만든 hello 항목을 포함 하 여 `StartOperation`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="dcaa2-252">검색에서 hello 작업 컨텍스트는 사용 되는 toocreate hello **관련 항목** 목록:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![관련 항목](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="dcaa2-254">사용자 지정 작업 추적에 대한 자세한 내용은 [application-insights-custom-operations-tracking.md]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="dcaa2-255">분석의 요청</span><span class="sxs-lookup"><span data-stu-id="dcaa2-255">Requests in Analytics</span></span> 

<span data-ttu-id="dcaa2-256">[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 표시를 요청 `requests` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="dcaa2-257">경우 [샘플링](app-insights-sampling.md) 은 작업에서 hello itemCount 속성은 값이 표시는 1 보다 큰 경우.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="dcaa2-258">예제 itemCount는 10 개의 호출이 tootrackRequest()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="dcaa2-259">요청 이름별 tooget 요청 및 평균 기간 올바른 수 분할와 같은 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="dcaa2-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="dcaa2-260">TrackException</span></span>
<span data-ttu-id="dcaa2-261">예외 tooApplication Insights 보내기:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="dcaa2-262">너무[합계를 구하고](app-insights-metrics-explorer.md), 문제의 hello 빈도를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="dcaa2-263">너무[개별 발생 수가 검사](app-insights-diagnostic-search.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="dcaa2-264">hello 보고서 hello 스택 추적에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="dcaa2-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="dcaa2-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="dcaa2-267">hello Sdk 바랍니다 항상 toocall TrackException 명시적으로 자동으로 대부분의 예외를 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="dcaa2-268">ASP.NET: [toocatch 예외 코드를 작성](app-insights-asp-net-exceptions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="dcaa2-269">J2EE: [예외가 자동으로 catch됨](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="dcaa2-270">JavaScript: 예외가 자동으로 catch됨.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="dcaa2-271">Toodisable 자동 수집 하려는 경우 웹 페이지에서 삽입 하는 줄 toohello 코드 조각을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="dcaa2-272">분석의 예외</span><span class="sxs-lookup"><span data-stu-id="dcaa2-272">Exceptions in Analytics</span></span>

<span data-ttu-id="dcaa2-273">[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 예외가 표시 `exceptions` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="dcaa2-274">경우 [샘플링](app-insights-sampling.md) 작업에 포함 되어, hello `itemCount` 속성 값이 1 보다 큰 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="dcaa2-275">예제 itemCount는 10 개의 호출이 tootrackException()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="dcaa2-276">예외의 유형을 통해 tooget 올바른 수 없는 예외 수 분할와 같은 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="dcaa2-277">대부분의 중요 한 스택 정보는 개별 변수로 추출 이미 하지만 더 많이 떨어져 있는 hello를 끌어올 수 hello `details` 구조 tooget 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="dcaa2-278">이 구조는 동적 이므로 hello 결과 toohello 형식을 예상 캐스팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="dcaa2-279">예:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="dcaa2-280">조인을 사용 하 여 해당 관련된 요청을 사용 하 여 tooassociate 예외:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="dcaa2-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="dcaa2-281">TrackTrace</span></span>
<span data-ttu-id="dcaa2-282">사용 하 여 TrackTrace toohelp "이동 경로 트레일에서" tooApplication 통찰력을 전송 하 여 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="dcaa2-283">진단 데이터의 청크를 보내고 [진단 검색](app-insights-diagnostic-search.md)에서 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="dcaa2-284">[어댑터 로그](app-insights-asp-net-trace-logs.md) 이 API toosend 제 3 자 로그 toohello 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="dcaa2-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="dcaa2-286">메시지 내용을 검색할 수 있지만 속성 값과는 달리 필터링할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="dcaa2-287">hello 크기 제한에 `message` hello 속성에 대 한도 보다 훨씬 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="dcaa2-288">TrackTrace 경우의 이점은 hello 메시지에 상대적으로 긴 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="dcaa2-289">예를 들어, POST 데이터를 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="dcaa2-290">또한, 심각도 수준 tooyour 메시지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="dcaa2-291">와 같은 다른 원격 분석을 필터링 할 속성 값 toohelp 또는 다른 집합이 추적에 대 한 검색 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="dcaa2-292">예:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="dcaa2-293">[검색](app-insights-diagnostic-search.md), tooa 특정 데이터베이스와 관련 된 특정 심각도 수준의 모든 hello 메시지를 쉽게 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="dcaa2-294">분석의 추적</span><span class="sxs-lookup"><span data-stu-id="dcaa2-294">Traces in Analytics</span></span>

<span data-ttu-id="dcaa2-295">[응용 프로그램 통찰력 분석](app-insights-analytics.md)를 실행 tooTrackTrace 표시 hello에 `traces` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="dcaa2-296">경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="dcaa2-297">10의 호출 하는 너무 10 의미 = = 연산자 예제 itemCount`trackTrace()`, 그 중 하나는 hello 샘플링 프로세스만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="dcaa2-298">tooget 추적 호출의 올바른 수를 사용 해야 하므로 코드와 같은 `traces | summarize sum(itemCount)`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="dcaa2-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="dcaa2-299">TrackDependency</span></span>
<span data-ttu-id="dcaa2-300">Tootrack hello 응답 시간과 성공률 호출 tooan 외부 코드 조각에 사용 하 여 hello TrackDependency를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="dcaa2-301">hello 결과가 hello 포털 hello 종속성 차트에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="dcaa2-302">해당 hello 서버 Sdk 포함 된다는 점에 유의 [종속성 모듈](app-insights-asp-net-dependencies.md) 검색 하 고 특정 종속성 호출을 자동으로-예: toodatabases 및 REST Api에 대 한 추적입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="dcaa2-303">Tooinstall 서버 toomake hello 모듈에서 에이전트를 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="dcaa2-304">자동화 된 추적 hello tootrack 호출 catch 하지 않으려는 경우 나 tooinstall hello 에이전트를 표시 하지 않으려는 경우이 호출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="dcaa2-305">기본 종속성 추적 모듈 hello 오프 tooturn 편집 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 너무 hello 참조를 삭제 하 고`DependencyCollector.DependencyTrackingTelemetryModule`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="dcaa2-306">분석의 종속성</span><span class="sxs-lookup"><span data-stu-id="dcaa2-306">Dependencies in Analytics</span></span>

<span data-ttu-id="dcaa2-307">[응용 프로그램 통찰력 분석](app-insights-analytics.md), hello에 trackDependency 호출 표시 `dependencies` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="dcaa2-308">경우 [샘플링](app-insights-sampling.md) hello itemCount 속성 값이 1 보다 큰 표시, 작업에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="dcaa2-309">예제 itemCount는 10 개의 호출이 tootrackDependency()의 hello 샘플링 프로세스에만 전송 중 10 의미 = = 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="dcaa2-310">대상 구성 요소에 의해 tooget 종속성의 올바른 수 분할와 같은 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="dcaa2-311">조인을 사용 하 여 해당 관련된 요청이 포함 된 tooassociate 종속성:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="dcaa2-312">데이터 플러시</span><span class="sxs-lookup"><span data-stu-id="dcaa2-312">Flushing data</span></span>
<span data-ttu-id="dcaa2-313">일반적으로 SDK hello 때때로 hello 사용자에 미치는 영향을 toominimize hello를 선택 하는 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="dcaa2-314">하지만, 일부 경우에 필요할 수 있습니다 tooflush hello 버퍼-예를 들어 종료 하는 응용 프로그램에 hello SDK를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="dcaa2-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="dcaa2-316">Hello 함수 hello에 대 한 비동기는 [서버 원격 분석 채널](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="dcaa2-317">인증된 사용자</span><span class="sxs-lookup"><span data-stu-id="dcaa2-317">Authenticated users</span></span>
<span data-ttu-id="dcaa2-318">웹앱에서 사용자는 기본적으로 쿠키로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="dcaa2-319">사용자가 다른 컴퓨터 또는 브라우저에서 앱에 액세스하거나 쿠키를 삭제하는 경우 두 번 이상 계산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="dcaa2-320">사용자가 tooyour 앱에 로그인 하는 경우에 hello 브라우저 코드에서 hello 인증 된 사용자 ID를 설정 하 여 보다 정확한 수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="dcaa2-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="dcaa2-322">ASP.NET 웹 MVC 응용 프로그램에서의 예:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="dcaa2-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="dcaa2-324">필요한 toouse hello 사용자의 실제 로그인 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="dcaa2-325">Toobe id는 고유 toothat 사용자 ID만에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="dcaa2-326">공백이 나 hello 문자를 포함 하지 않아야 `,;=|`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="dcaa2-327">hello 사용자 ID도 세션 쿠키에 설정 되 고 toohello 서버에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="dcaa2-328">Hello 서버 SDK가 설치 되어 hello ID가 클라이언트와 서버 모두의 원격 분석의 hello 컨텍스트 속성의 일부로 전송 되는 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="dcaa2-329">필터링하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-329">You can then filter and search on it.</span></span>

<span data-ttu-id="dcaa2-330">사용자 계정으로 그룹화 하는 응용 프로그램, hello 계정에 대 한 식별자 전달할 수도 있습니다 (hello로 동일한 문자 제한).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="dcaa2-331">[메트릭 탐색기](app-insights-metrics-explorer.md)에서 **사용자, 인증** 및 **사용자 계정**을 계산하는 차트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="dcaa2-332">특정 사용자 이름과 계정으로 클라이언트 데이터 지점을 [검색](app-insights-diagnostic-search.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="dcaa2-333"><a name="properties"></a>속성을 사용하여 데이터를 필터링, 검색 및 세분화</span><span class="sxs-lookup"><span data-stu-id="dcaa2-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="dcaa2-334">속성 및 측정 tooyour 이벤트 (및 또한 toometrics, 페이지 보기, 예외 및 기타 원격 분석 데이터)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="dcaa2-335">*속성* 는 사용할 수 있는 toofilter 원격 분석 hello 사용 현황 보고서에는 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="dcaa2-336">예를 들어 여러 게임을 제공 하는 앱을 더 많이 사용 되는 게임을 볼 수 있도록 hello 게임 tooeach 이벤트의 hello 이름을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="dcaa2-337">Hello 문자열 길이 8192의 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="dcaa2-338">(Toosend 큰 데이터 청크의 경우의 hello 메시지 매개 변수를 사용할 [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="dcaa2-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="dcaa2-339">*메트릭* 은 그래픽으로 표시할 수 있는 숫자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="dcaa2-340">예를 들어 프로그램 게이머 달성 하는 hello 점수에 점진적으로 증가 하면 toosee를 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="dcaa2-341">hello 그래프 얻을 수 있도록 hello 이벤트와 함께 전송 되는 속성을 구분 하는 hello 나눌 수 있습니다 또는 다른 게임에 대 한 그래프를 누적 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="dcaa2-342">메트릭 값 toobe 올바로 표시에 대 한 보다 크거나 같은 too0 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="dcaa2-343">일부 [속성, 속성 값, 및 메트릭을 hello 수에 대 한 제한](#limits) 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="dcaa2-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="dcaa2-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="dcaa2-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="dcaa2-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="dcaa2-348">개인 식별이 가능한 정보 속성에서 toolog 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="dcaa2-349">*메트릭을 사용 하는 경우*메트릭 탐색기를 열고 hello에서 hello 메트릭을 선택 **사용자 지정** 그룹:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![메트릭 탐색기를 선택 하는 hello 차트를 열고 hello 메트릭을 선택 합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="dcaa2-351">프로그램 메트릭을 표시 되지 않으면 또는 경우 hello **사용자 지정** 제목 없는 선택 영역 블레이드 닫기 hello 및 나중에 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="dcaa2-352">한 시간 메트릭 오래 걸릴 수도 toobe hello 파이프라인을 통해 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="dcaa2-353">*속성 및 메트릭을 사용 하는 경우*, hello 속성을 기준으로 hello 메트릭을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![그룹화를 설정 하 고 그룹화 기준 hello 속성을 선택 합니다](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="dcaa2-355">*진단 검색*, hello 속성 및 이벤트의 개별 항목의 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![인스턴스를 선택한 다음 '...'를 선택합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="dcaa2-357">사용 하 여 hello **검색** 특정 속성 값을 가진 toosee 이벤트 항목만 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![검색에 용어를 입력합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="dcaa2-359">[검색 식에 대해 자세히 알아보세요](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="dcaa2-360">다른 방법으로 tooset 속성 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="dcaa2-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="dcaa2-361">더 편리 이면 hello 매개 변수는 별도 개체에 이벤트를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="dcaa2-362">Hello를 다시 사용 하지 마세요 동일한 원격 분석 항목 인스턴스 (`event` 이 예에서) toocall Track*() 여러 번입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="dcaa2-363">잘못 된 구성으로 전송 하는 원격 분석 toobe를 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="dcaa2-364">분석의 사용자 지정 측정 및 속성</span><span class="sxs-lookup"><span data-stu-id="dcaa2-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="dcaa2-365">[분석](app-insights-analytics.md), hello에 대 한 사용자 지정 메트릭 및 속성 표시 `customMeasurements` 및 `customDimensions` 각 원격 분석 레코드의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="dcaa2-366">예를 들어 "게임" tooyour 요청 원격 분석 라는 속성을 추가한 경우이 쿼리 hello 발생 "게임"의 서로 다른 값의 수를 세 않으며 hello의 hello 평균 점수"사용자 지정 메트릭"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="dcaa2-367">다음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-367">Notice that:</span></span>

* <span data-ttu-id="dcaa2-368">가 동적 형식이 고 캐스팅 해야 하므로 hello customDimensions 또는 customMeasurements JSON에서 값을 추출할 때 `tostring` 또는 `todouble`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="dcaa2-369">hello 가능성 tootake 계정 [샘플링](app-insights-sampling.md)를 사용 해야 `sum(itemCount)`이 아니라 `count()`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="dcaa2-370"><a name="timed"></a> 타이밍 이벤트</span><span class="sxs-lookup"><span data-stu-id="dcaa2-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="dcaa2-371">소요 tooperform 동작 toochart를 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="dcaa2-372">예를 들어 tooknow 경우가 사용자 게임에서 tooconsider 선택 항목을 사용 하는 기간.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="dcaa2-373">이 대 한 hello 측정 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="dcaa2-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="dcaa2-375"><a name="defaults"></a>사용자 지정 원격 분석에 대한 기본 속성</span><span class="sxs-lookup"><span data-stu-id="dcaa2-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="dcaa2-376">일부 사용자가 작성 하는 hello 사용자 지정 이벤트에 대 한 tooset 기본 속성 값을 원하는 경우 TelemetryClient 인스턴스에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="dcaa2-377">이들은 연결 된 tooevery 원격 분석 항목은 해당 클라이언트에서 전송 된입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="dcaa2-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="dcaa2-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="dcaa2-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="dcaa2-381">원격 분석 개별 호출 자신의 속성 사전에 hello 기본 값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="dcaa2-382">*JavaScript 웹 클라이언트의 경우*[JavaScript 원격 분석 이니셜라이저를 사용합니다](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="dcaa2-383">*tooadd 속성 tooall 원격 분석*, 표준 컬렉션 모듈 hello 데이터를 포함 하 여 [구현 `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="dcaa2-384">원격 분석 샘플링, 필터링 및 처리</span><span class="sxs-lookup"><span data-stu-id="dcaa2-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="dcaa2-385">Hello SDK에서에서 전송 하기 전에 원격 분석 코드 tooprocess을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="dcaa2-386">hello 처리와 같은 HTTP 요청 컬렉션과 종속성 컬렉션 hello 표준 원격 분석 모듈에서 전송 된 데이터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="dcaa2-387">[속성 추가](app-insights-api-filtering-sampling.md#add-properties) 구현 하 여 tootelemetry `ITelemetryInitializer`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="dcaa2-388">예를 들어 다른 속성에서 계산된 버전 번호 또는 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="dcaa2-389">[필터링](app-insights-api-filtering-sampling.md#filtering) 수정 하거나 구현 하 여 hello SDK에서에서 전송 하기 전에 원격 분석을 취소 `ITelemetryProcesor`합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="dcaa2-390">전송 되었거나 무시 된 항목을 제어 있는데 tooaccount 하면 메트릭이에 hello 영향에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="dcaa2-391">항목을 삭제 하는 방법에 따라 관련된 항목 간의 hello 기능 toonavigate를 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="dcaa2-392">[샘플링](app-insights-api-filtering-sampling.md) 앱 toohello 포털에서 전송 된 데이터를 패키지에 포함 된 솔루션 tooreduce hello 볼륨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="dcaa2-393">메트릭을 표시 하는 hello 영향을 주지 않고을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="dcaa2-394">한 예외, 요청 및 페이지 보기 등의 관련된 항목 간에 이동 하 여 기능 toodiagnose 문제 영향을 주지 않고 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="dcaa2-395">[자세히 알아봅니다](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="dcaa2-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="dcaa2-396">원격 분석 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="dcaa2-396">Disabling telemetry</span></span>
<span data-ttu-id="dcaa2-397">너무*동적으로 중지 하 고 시작* 수집 및 원격 분석 전송을 hello:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="dcaa2-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="dcaa2-399">너무*선택한 표준 수집기를 해제*-예를 들어 성능 카운터, HTTP 요청-종속성을 삭제 하거나 hello 관련 줄의 주석 처리 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)합니다. 이렇게 하려면, 예를 들어 toosend TrackRequest 자신만 데이터를 원하는 경우.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="dcaa2-400"><a name="debug"></a>개발자 모드</span><span class="sxs-lookup"><span data-stu-id="dcaa2-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="dcaa2-401">디버깅 하는 동안 원격 분석 결과 즉시 볼 수 있도록 hello 파이프라인을 통해 신속한 유용 toohave 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="dcaa2-402">된 hello 원격 분석 문제를 추적할도 get 추가 메시지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="dcaa2-403">앱이 느려질 수 있으므로 프로덕션 환경에서는 끄는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="dcaa2-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="dcaa2-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="dcaa2-406"><a name="ikey"></a>선택한 사용자 지정 원격 분석을 위한 hello 계측 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="dcaa2-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="dcaa2-408"><a name="dynamic-ikey"></a> 동적 계측 키</span><span class="sxs-lookup"><span data-stu-id="dcaa2-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="dcaa2-409">개발, 테스트 및 프로덕션 환경에서 원격 분석을 혼합 tooavoid 할 수 있습니다 [별도 Application Insights 리소스 만들기](app-insights-create-new-resource.md) hello 환경에 따라 해당 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="dcaa2-410">Hello 구성 파일에서 hello 계측 키를 가져오는 대신 코드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="dcaa2-411">초기화 메서드에서 global.aspx.cs ASP.NET 서비스에서 같은 hello 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="dcaa2-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="dcaa2-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="dcaa2-414">웹 페이지에 tooset 수도 hello 웹 서버의 상태를 보다는 hello 스크립트에 문자 그대로 코딩 옵니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="dcaa2-415">예를 들어 ASP.NET 앱에서 생성된 웹 페이지에서 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="dcaa2-416">*Razor에서 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="dcaa2-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="dcaa2-417">TelemetryContext</span></span>
<span data-ttu-id="dcaa2-418">TelemetryClient에는 컨텍스트 속성이 있고, 이 속성은 모든 원격 분석 데이터와 함께 전송되는 값을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="dcaa2-419">일반적으로 hello 표준 원격 분석 모듈에 의해 설정 하지만 또한 속성을 설정할 수 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="dcaa2-420">예:</span><span class="sxs-lookup"><span data-stu-id="dcaa2-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="dcaa2-421">직접 설정할 경우 다음이 값 중 하나를 고려 hello에서 관련 줄을 제거 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)값과 hello 표준 값의 혼동 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="dcaa2-422">**구성 요소**: hello 앱 및 해당 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="dcaa2-423">**장치**: hello 앱이 실행 되는 hello 장치에 대 한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="dcaa2-424">(웹 응용 프로그램에서이 hello 서버 또는 클라이언트 장치에서 보내는 hello 원격 분석.)</span><span class="sxs-lookup"><span data-stu-id="dcaa2-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="dcaa2-425">**InstrumentationKey**: hello Azure hello 원격 분석 표시 되는 위치에서 Application Insights 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="dcaa2-426">일반적으로 ApplicationInsights.config에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="dcaa2-427">**위치**: hello hello 장치의 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="dcaa2-428">**작업**: 웹 응용 프로그램에서 현재 HTTP 요청을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="dcaa2-429">다른 응용 프로그램 형식에서는이 toogroup 이벤트를 함께 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="dcaa2-430">**Id**: 진단 검색의 이벤트를 검사할 때 "항목 관련"을 찾을 수 있도록 여러 이벤트를 상호 연결하는 생성된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="dcaa2-431">**이름**: 일반적으로 hello 요청 URL의 HTTP hello 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="dcaa2-432">**SyntheticSource**: 경우 하지 null 이거나 비어 hello 요청의 hello 원본을 나타내는 문자열 확인 되었습니다 로봇 또는 웹 테스트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="dcaa2-433">기본적으로 메트릭 탐색기의 계산에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="dcaa2-434">**Properties**: 모든 원격 분석 데이터와 함께 전송되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="dcaa2-435">개별 Track* 호출에서 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="dcaa2-436">**세션**: hello 사용자의 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-436">**Session**: hello user's session.</span></span> <span data-ttu-id="dcaa2-437">hello ID hello 사용자가 하지 상태인 동안 때 변경 되는 tooa 생성 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="dcaa2-438">**User**: 사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="dcaa2-439">제한</span><span class="sxs-lookup"><span data-stu-id="dcaa2-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="dcaa2-440">사용 하 여 hello 데이터 속도 제한에 도달 tooavoid [샘플링](app-insights-sampling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="dcaa2-441">toodetermine 긴 데이터를 유지 하는 방법 참조 [데이터 보존 및 개인 정보 보호](app-insights-data-retention-privacy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="dcaa2-442">참조 문서</span><span class="sxs-lookup"><span data-stu-id="dcaa2-442">Reference docs</span></span>
* [<span data-ttu-id="dcaa2-443">ASP.NET 참조</span><span class="sxs-lookup"><span data-stu-id="dcaa2-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="dcaa2-444">Java 참조</span><span class="sxs-lookup"><span data-stu-id="dcaa2-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="dcaa2-445">JavaScript 참조</span><span class="sxs-lookup"><span data-stu-id="dcaa2-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="dcaa2-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="dcaa2-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="dcaa2-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="dcaa2-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="dcaa2-448">SDK 코드</span><span class="sxs-lookup"><span data-stu-id="dcaa2-448">SDK code</span></span>
* [<span data-ttu-id="dcaa2-449">ASP.NET 핵심 SDK</span><span class="sxs-lookup"><span data-stu-id="dcaa2-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="dcaa2-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="dcaa2-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="dcaa2-451">Windows Server 패키지</span><span class="sxs-lookup"><span data-stu-id="dcaa2-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="dcaa2-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="dcaa2-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="dcaa2-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="dcaa2-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="dcaa2-454">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="dcaa2-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="dcaa2-455">질문</span><span class="sxs-lookup"><span data-stu-id="dcaa2-455">Questions</span></span>
* <span data-ttu-id="dcaa2-456">*Track_() 호출에서 발생할 수 있는 예외는 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="dcaa2-457">없음.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-457">None.</span></span> <span data-ttu-id="dcaa2-458">Toowrap 않아도 try catch 절에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="dcaa2-459">Hello 디버그 콘솔 출력에서 메시지를 기록 합니다 hello SDK에서 문제가 발생 하는 경우 및--인 경우 hello 메시지 될-를 통해 진단 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="dcaa2-460">*Hello 포털에서 REST API tooget 데이터는 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="dcaa2-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="dcaa2-461">예, hello [데이터 액세스 API](https://dev.applicationinsights.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="dcaa2-462">다른 방법으로 tooextract 데이터 포함 [분석 tooPower BI에서에서 내보낼](app-insights-export-power-bi.md) 및 [연속 내보내기를](app-insights-export-telemetry.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcaa2-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="dcaa2-463"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="dcaa2-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="dcaa2-464">검색 이벤트 및 로그</span><span class="sxs-lookup"><span data-stu-id="dcaa2-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="dcaa2-465">문제 해결</span><span class="sxs-lookup"><span data-stu-id="dcaa2-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


