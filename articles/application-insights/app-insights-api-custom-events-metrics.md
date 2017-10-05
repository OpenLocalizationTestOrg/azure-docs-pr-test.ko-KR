---
title: "사용자 지정 이벤트 및 메트릭용 Application Insights API | Microsoft Docs"
description: "장치 또는 데스크톱 앱, 웹 페이지, 서비스에 코드를 몇 줄 삽입하여 사용 및 진단 문제를 추적할 수 있습니다."
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
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="d6cb7-103">사용자 지정 이벤트 및 메트릭용 Application Insights API</span><span class="sxs-lookup"><span data-stu-id="d6cb7-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="d6cb7-104">응용 프로그램에 몇 줄의 코드를 삽입하여 사용자가 해당 응용 프로그램으로 어떤 작업을 하는지 살펴보거나 진단 문제를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="d6cb7-105">장치 및 데스크톱 앱, 웹 클라이언트, 웹 서버에서 원격 분석을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="d6cb7-106">[Azure Application Insights](app-insights-overview.md) 코어 원격 분석 API를 사용하여 사용자 지정 이벤트 및 메트릭 그리고 고유한 버전의 표준 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="d6cb7-107">이 API는 표준 Application Insights 데이터 수집기에서 사용하는 동일한 API입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="d6cb7-108">API 요약</span><span class="sxs-lookup"><span data-stu-id="d6cb7-108">API summary</span></span>
<span data-ttu-id="d6cb7-109">API는 사소한 차이를 제외하고 모든 플랫폼에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="d6cb7-110">메서드</span><span class="sxs-lookup"><span data-stu-id="d6cb7-110">Method</span></span> | <span data-ttu-id="d6cb7-111">용도</span><span class="sxs-lookup"><span data-stu-id="d6cb7-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="d6cb7-112">페이지, 화면, 블레이드 또는 양식.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="d6cb7-113">사용자 작업 및 기타 이벤트.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-113">User actions and other events.</span></span> <span data-ttu-id="d6cb7-114">사용자 동작을 추적하거나 성능을 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="d6cb7-115">특정 이벤트와 관련이 없는 큐 길이와 같은 성능 측정.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="d6cb7-116">진단 예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="d6cb7-117">다른 이벤트와 관련하여 발생 위치를 추적하고 스택 추적을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="d6cb7-118">성능 분석에 대한 서버 요청 빈도 및 기간을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="d6cb7-119">진단 로그 메시지.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-119">Diagnostic log messages.</span></span> <span data-ttu-id="d6cb7-120">타사 로그도 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="d6cb7-121">기간 및 빈도 앱이 종속된 외부 구성 요소에 대한 호출을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="d6cb7-122">이러한 대부분의 원격 분석 호출에 [속성 및 메트릭을 연결](#properties) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="d6cb7-123"><a name="prep"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d6cb7-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="d6cb7-124">Application Insights SDK에 대한 참조가 아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="d6cb7-125">프로젝트에 Application Insights SDK 추가:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="d6cb7-126">ASP.NET 프로젝트</span><span class="sxs-lookup"><span data-stu-id="d6cb7-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="d6cb7-127">Java 프로젝트</span><span class="sxs-lookup"><span data-stu-id="d6cb7-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="d6cb7-128">각 웹 페이지의 JavaScript</span><span class="sxs-lookup"><span data-stu-id="d6cb7-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="d6cb7-129">장치 또는 웹 서버 코드에 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="d6cb7-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="d6cb7-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="d6cb7-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="d6cb7-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="d6cb7-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="d6cb7-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="d6cb7-133">TelemetryClient 인스턴스 생성</span><span class="sxs-lookup"><span data-stu-id="d6cb7-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="d6cb7-134">`TelemetryClient`의 인스턴스를 생성합니다(웹 페이지의 JavaScript는 제외).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="d6cb7-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="d6cb7-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="d6cb7-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="d6cb7-138">TelemetryClient는 스레드로부터 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="d6cb7-139">앱의 각 모듈에 대해 TelemetryClient 인스턴스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="d6cb7-140">예를 들어 웹 서비스에 들어오는 HTTP 요청을 보고하는 TelemetryClient 인스턴스 하나가 있고 미들웨어 클래스에 비즈니스 논리 이벤트를 보고하는 다른 하나가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="d6cb7-141">`TelemetryClient.Context.User.Id`와 같은 속성을 설정하여 사용자 및 세션을 추적하거나 `TelemetryClient.Context.Device.Id`를 설정하여 컴퓨터를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="d6cb7-142">이 정보는 인스턴스에서 보내는 모든 이벤트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="d6cb7-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="d6cb7-143">TrackEvent</span></span>
<span data-ttu-id="d6cb7-144">Application Insights에서 *사용자 지정 이벤트*는 [메트릭 탐색기](app-insights-metrics-explorer.md)에 집계된 개수로 표시하고 [진단 검색](app-insights-diagnostic-search.md)에 개별 항목으로 표시할 수 있는 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="d6cb7-145">MVC 또는 다른 프레임워크 "이벤트"와 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="d6cb7-146">다양한 이벤트를 계산하기 위해 코드에 `TrackEvent`를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="d6cb7-147">사용자가 특정 기능을 얼마나 자주 선택하는지, 특정 목표를 얼마나 자주 달성하는지 또는 특정 유형의 실수를 얼마나 자주 하는지를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="d6cb7-148">예를 들어 게임 앱은 사용자가 이길 때마다 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="d6cb7-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="d6cb7-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="d6cb7-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="d6cb7-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="d6cb7-153">Microsoft Azure Portal에서 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="d6cb7-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="d6cb7-154">이벤트의 수를 보려면 [메트릭 탐색기](app-insights-metrics-explorer.md) 블레이드를 열고 새 차트를 추가한 다음 **이벤트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![사용자 지정 이벤트 수 보기](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="d6cb7-156">여러 이벤트의 수를 비교하려면 차트 유형을 **그리드**로 설정하고 이벤트 이름으로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![차트 종류 및 그룹화 설정](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="d6cb7-158">그리드에서 이벤트 이름을 클릭하여 해당 이벤트의 개별 항목을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="d6cb7-159">목록에서 해당 항목을 클릭하여 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-159">To see more detail - click any occurrence in the list.</span></span>

![이벤트를 드릴스루합니다.](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="d6cb7-161">검색 또는 메트릭 탐색기에서 특정 이벤트를 자세히 살펴보려면 관심 있는 이벤트 이름으로 블레이드 필터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![필터를 열고 이벤트 이름을 확장한 다음 하나 이상의 값을 선택합니다.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="d6cb7-163">분석의 사용자 지정 이벤트</span><span class="sxs-lookup"><span data-stu-id="d6cb7-163">Custom events in Analytics</span></span>

<span data-ttu-id="d6cb7-164">[Application Insights 분석](app-insights-analytics.md)의 `customEvents` 테이블에서 원격 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="d6cb7-165">각 행은 앱의 `trackEvent(..)` 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="d6cb7-166">[샘플링](app-insights-sampling.md)이 작동 중이면 itemCount 속성에 1보다 큰 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="d6cb7-167">예를 들어 itemCount==10은 trackEvent()에 대한 10개 호출의 샘플링을 의미하며 샘플링 프로세스는 이 중 하나만 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="d6cb7-168">따라서 정확한 사용자 지정 이벤트 수를 가져오려면 `customEvent | summarize sum(itemCount)`와 같은 코드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="d6cb7-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="d6cb7-169">TrackMetric</span></span>

<span data-ttu-id="d6cb7-170">Application Insights에서는 특정 이벤트에 연결되지 않은 메트릭을 차트로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="d6cb7-171">예를 들어 정기적으로 큐 길이를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="d6cb7-172">메트릭을 사용할 경우 개별 측정값보다 변형 및 추세에 좀 더 관심을 갖게 되며 통계 차트가 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="d6cb7-173">Application Insights로 메트릭을 보내려면 `TrackMetric(..)` API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="d6cb7-174">메트릭을 전송하는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="d6cb7-175">단일 값.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-175">Single value.</span></span> <span data-ttu-id="d6cb7-176">응용 프로그램에서 측정을 수행할 때마다 Application Insights에 해당 값을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="d6cb7-177">예를 들어 컨테이너의 항목 수를 설명하는 메트릭이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="d6cb7-178">특정 기간 동안 먼저 컨테이너에 3개 항목을 추가한 다음 2개 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="d6cb7-179">따라서 `TrackMetric`을 두 번 호출합니다. 처음에는 값 `3`을 전달하고 그 다음에는 값 `-2`를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="d6cb7-180">Application Insights는 두 값을 자동으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="d6cb7-181">집계.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-181">Aggregation.</span></span> <span data-ttu-id="d6cb7-182">메트릭을 사용하여 작업하는 경우 모든 단일 측정값은 거의 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="d6cb7-183">대신 특정 기간 동안 발생한 내용의 요약이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="d6cb7-184">이러한 요약을 _집계_라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="d6cb7-185">위의 예에서는 해당 기간에 대한 집계 메트릭 합계는 `1`이고 메트릭 값의 개수는 `2`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="d6cb7-186">집계 방법을 사용할 때는 `TrackMetric`을 기간당 한 번만 호출하고 집계 값을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="d6cb7-187">이렇게 하면 모든 관련 정보를 수집하는 동안 더 적은 데이터 요소를 Application Insights로 보냄으로써 비용 및 성능 오버헤드를 상당히 줄일 수 있기 때문에 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="d6cb7-188">예제:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="d6cb7-189">단일 값</span><span class="sxs-lookup"><span data-stu-id="d6cb7-189">Single values</span></span>

<span data-ttu-id="d6cb7-190">단일 메트릭 값을 전송하려면</span><span class="sxs-lookup"><span data-stu-id="d6cb7-190">To send a single metric value:</span></span>

<span data-ttu-id="d6cb7-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="d6cb7-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="d6cb7-193">메트릭 집계</span><span class="sxs-lookup"><span data-stu-id="d6cb7-193">Aggregating metrics</span></span>

<span data-ttu-id="d6cb7-194">앱에서 전송하기 전에 메트릭을 집계해서 대역폭 및 비용을 줄이고 성능을 개선하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="d6cb7-195">다음은 집계 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="d6cb7-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-196">*C#*</span></span>

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
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
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
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="d6cb7-197">메트릭 탐색기의 사용자 지정 메트릭</span><span class="sxs-lookup"><span data-stu-id="d6cb7-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="d6cb7-198">결과를 보려면 메트릭 탐색기를 열고 새 차트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="d6cb7-199">차트를 편집하여 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="d6cb7-200">사용자 지정 메트릭이 사용 가능한 메트릭 목록에 표시되는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![새 차트를 추가하거나 차트를 선택하고, 사용자 지정 아래에서 메트릭을 선택합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="d6cb7-202">분석의 사용자 지정 메트릭</span><span class="sxs-lookup"><span data-stu-id="d6cb7-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="d6cb7-203">[Application Insights 분석](app-insights-analytics.md)의 `customMetrics` 테이블에서 원격 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="d6cb7-204">각 행은 앱의 `trackMetric(..)` 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="d6cb7-205">`valueSum` - 측정값의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="d6cb7-206">평균 값을 가져오려면 `valueCount`로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="d6cb7-207">`valueCount` - 이 `trackMetric(..)` 호출로 집계된 측정값의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="d6cb7-208">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="d6cb7-208">Page views</span></span>
<span data-ttu-id="d6cb7-209">장치 또는 웹 페이지 앱에서 각 화면 또는 페이지가 로드되면 기본적으로 페이지 보기 원격 분석이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="d6cb7-210">하지만 추가 시간에 또는 다른 시간에 페이지 보기를 추적하도록 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="d6cb7-211">예를 들어 탭 또는 블레이드를 표시하는 앱에서 사용자가 새 블레이드를 열 때마다 "페이지"를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![개요 블레이드의 사용 현황 렌즈](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="d6cb7-213">사용자 및 세션 데이터는 페이지 보기와 함께 속성으로 전송됩니다. 따라서 페이지 보기 원격 분석이 있으면 사용자 및 세션 차트가 실시간으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="d6cb7-214">사용자 지정 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="d6cb7-214">Custom page views</span></span>
<span data-ttu-id="d6cb7-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="d6cb7-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="d6cb7-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="d6cb7-218">여러 다른 HTML 페이지 내에 여러 탭이 있으면 URL도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="d6cb7-219">페이지 보기 시간</span><span class="sxs-lookup"><span data-stu-id="d6cb7-219">Timing page views</span></span>
<span data-ttu-id="d6cb7-220">기본적으로 시간은 브라우저가 요청을 보낼 때부터 브라우저의 페이지 로드 이벤트를 호출할 때까지 측정되는 **페이지 보기 로드 시간**으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="d6cb7-221">대신, 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-221">Instead, you can either:</span></span>

* <span data-ttu-id="d6cb7-222">[trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) 호출에서 명시적 기간을 설정합니다. `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`</span><span class="sxs-lookup"><span data-stu-id="d6cb7-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="d6cb7-223">페이지 보기 시간 호출 `startTrackPage` 및 `stopTrackPage`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="d6cb7-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="d6cb7-225">...</span><span class="sxs-lookup"><span data-stu-id="d6cb7-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="d6cb7-226">첫 번째 매개 변수로 사용하는 이름은 시작 및 중지 호출을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="d6cb7-227">기본적으로 현재 페이지 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-227">It defaults to the current page name.</span></span>

<span data-ttu-id="d6cb7-228">메트릭 탐색기에 표시된 결과 페이지 로드 기간은 시작 및 중지 호출 사이의 간격에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="d6cb7-229">실제로 걸리는 시간 간격에 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="d6cb7-230">분석의 페이지 원격 분석</span><span class="sxs-lookup"><span data-stu-id="d6cb7-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="d6cb7-231">[분석](app-insights-analytics.md)에서 두 테이블이 브라우저 작업의 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="d6cb7-232">URL 및 페이지 제목에 대한 데이터가 포함된 `pageViews` 테이블</span><span class="sxs-lookup"><span data-stu-id="d6cb7-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="d6cb7-233">들어오는 데이터를 처리하는 데 걸리는 시간 등의 클라이언트 성능에 대한 데이터가 포함된 `browserTimings` 테이블</span><span class="sxs-lookup"><span data-stu-id="d6cb7-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="d6cb7-234">브라우저가 다른 페이지를 처리하는 데 걸리는 시간을 보려면</span><span class="sxs-lookup"><span data-stu-id="d6cb7-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="d6cb7-235">서로 다른 브라우저의 인기도를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="d6cb7-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="d6cb7-236">페이지 보기를 AJAX 호출과 상호 연결하려면(종속성과 조인)</span><span class="sxs-lookup"><span data-stu-id="d6cb7-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="d6cb7-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="d6cb7-237">TrackRequest</span></span>
<span data-ttu-id="d6cb7-238">서버 SDK는 TrackRequest를 사용하여 HTTP 요청을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="d6cb7-239">실행 중인 웹 서비스 모듈이 없는 상황에서 요청을 시뮬레이션하고 싶다면 사용자가 직접 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="d6cb7-240">그러나 요청 원격 분석을 전송하는 권장 방법은 요청이 <a href="#operation-context">작업 컨텍스트</a>로 작동하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="d6cb7-241">작업 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="d6cb7-241">Operation context</span></span>
<span data-ttu-id="d6cb7-242">원격 분석 항목을 일반 작업 ID에 연결하여 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="d6cb7-243">표준 요청 추적 모듈은 예외 및 HTTP 요청이 처리되는 동안 전송되는 다른 이벤트에 대해 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="d6cb7-244">[검색](app-insights-diagnostic-search.md) 및 [분석](app-insights-analytics.md)에서 ID를 사용하여 요청과 관련된 모든 이벤트를 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="d6cb7-245">ID를 설정하는 가장 쉬운 방법은 이 패턴을 사용하여 작업 컨텍스트를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="d6cb7-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="d6cb7-247">작업 컨텍스트 설정과 함께 `StartOperation`은 지정하는 유형의 원격 분석 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="d6cb7-248">작업을 삭제할 때 또는 명시적으로 `StopOperation`을 호출하는 경우 원격 분석 항목을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="d6cb7-249">원격 분석 형식으로 `RequestTelemetry`를 사용하는 경우 해당 기간은 시작 및 중지 사이의 시간 제한 간격으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="d6cb7-250">작업 컨텍스트는 중첩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="d6cb7-251">작업 컨텍스트가 이미 있는 경우 해당 ID가 `StartOperation`을 사용하여 만든 항목을 비롯한 모든 포함된 항목에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="d6cb7-252">검색에서 작업 컨텍스트는 **관련 항목** 목록을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![관련 항목](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="d6cb7-254">사용자 지정 작업 추적에 대한 자세한 내용은 [application-insights-custom-operations-tracking.md]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="d6cb7-255">분석의 요청</span><span class="sxs-lookup"><span data-stu-id="d6cb7-255">Requests in Analytics</span></span> 

<span data-ttu-id="d6cb7-256">[Application Insights 분석](app-insights-analytics.md)에서 요청은 `requests` 테이블에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="d6cb7-257">[샘플링](app-insights-sampling.md)이 작동 중이면 itemCount 속성에 1보다 큰 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="d6cb7-258">예를 들어 itemCount==10은 trackRequest()에 대한 10개 호출의 샘플링을 의미하며 샘플링 프로세스는 이 중 하나만 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="d6cb7-259">요청 이름별로 분할된 정확한 요청 수 및 평균 기간을 가져오려면 다음과 같은 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="d6cb7-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="d6cb7-260">TrackException</span></span>
<span data-ttu-id="d6cb7-261">Application Insights로 예외를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="d6cb7-262">문제의 빈도 표시로 [계산](app-insights-metrics-explorer.md)하려면</span><span class="sxs-lookup"><span data-stu-id="d6cb7-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="d6cb7-263">[개별 항목을 검사](app-insights-diagnostic-search.md)하려면</span><span class="sxs-lookup"><span data-stu-id="d6cb7-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="d6cb7-264">보고서는 스택 추적을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-264">The reports include the stack traces.</span></span>

<span data-ttu-id="d6cb7-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="d6cb7-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="d6cb7-267">SDK에서 대부분의 예외를 자동으로 catch하므로 항상 TrackException을 명시적으로 호출할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="d6cb7-268">ASP.NET: [예외를 catch하는 코드 작성](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="d6cb7-269">J2EE: [예외가 자동으로 catch됨](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="d6cb7-270">JavaScript: 예외가 자동으로 catch됨.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="d6cb7-271">자동 수집을 사용하지 않도록 설정하려면 웹 페이지에 삽입하는 코드 조각에 다음 한 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="d6cb7-272">분석의 예외</span><span class="sxs-lookup"><span data-stu-id="d6cb7-272">Exceptions in Analytics</span></span>

<span data-ttu-id="d6cb7-273">[Application Insights 분석](app-insights-analytics.md)에서 예외는 `exceptions` 테이블에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="d6cb7-274">[샘플링](app-insights-sampling.md)이 작동 중이면 `itemCount` 속성에 1보다 큰 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="d6cb7-275">예를 들어 itemCount==10은 trackException()에 대한 10개 호출의 샘플링을 의미하며 샘플링 프로세스는 이 중 하나만 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="d6cb7-276">예외 유형별로 분할된 정확한 예외 수를 가져오려면 다음과 같은 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="d6cb7-277">대부분의 중요한 스택 정보는 이미 별도 변수로 추출되지만 좀 더 자세한 정보를 위해 `details` 구조를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="d6cb7-278">이 구조는 동적이므로 원하는 유형으로 결과를 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="d6cb7-279">예:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="d6cb7-280">예외를 관련 요청과 연결하려면 다음과 같이 조인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="d6cb7-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="d6cb7-281">TrackTrace</span></span>
<span data-ttu-id="d6cb7-282">이 TrackTrace를 사용하여 Application Insights에 '이동 경로 트레일'을 전송하면 문제 진단에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="d6cb7-283">진단 데이터의 청크를 보내고 [진단 검색](app-insights-diagnostic-search.md)에서 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="d6cb7-284">[로그 어댑터](app-insights-asp-net-trace-logs.md)는 이 API를 사용하여 포털에 타사 로그를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="d6cb7-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="d6cb7-286">메시지 내용을 검색할 수 있지만 속성 값과는 달리 필터링할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="d6cb7-287">`message`의 크기 제한이 속성의 크기 제한보다 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="d6cb7-288">TrackTrace의 장점은 메시지에 상대적으로 긴 데이터를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="d6cb7-289">예를 들어, POST 데이터를 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="d6cb7-290">또한 메시지에 심각도 수준을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="d6cb7-291">또 다른 원격 분석처럼, 다른 추적 집합에 대해 필터링 또는 검색하는 데 도움이 되는 속성 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="d6cb7-292">예:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="d6cb7-293">[검색](app-insights-diagnostic-search.md)에서 특정 데이터베이스와 관련된 특정 심각도 수준의 모든 메시지를 쉽게 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="d6cb7-294">분석의 추적</span><span class="sxs-lookup"><span data-stu-id="d6cb7-294">Traces in Analytics</span></span>

<span data-ttu-id="d6cb7-295">[Application Insights 분석](app-insights-analytics.md)에서 TrackTrace에 대한 호출은 `traces` 테이블에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="d6cb7-296">[샘플링](app-insights-sampling.md)이 작동 중이면 itemCount 속성에 1보다 큰 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="d6cb7-297">예를 들어 itemCount==10은 `trackTrace()`에 대한 10개 호출 샘플링을 의미하며 샘플링 프로세스는 이 중 하나만 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="d6cb7-298">따라서 정확한 추적 호출 수를 가져오려면 `traces | summarize sum(itemCount)`와 같은 코드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="d6cb7-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="d6cb7-299">TrackDependency</span></span>
<span data-ttu-id="d6cb7-300">TrackDependency 호출을 사용하여 응답 시간과 외부 코드 부분에 대한 호출의 성공률을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="d6cb7-301">포털에서 종속성 차트에 결과가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-301">The results appear in the dependency charts in the portal.</span></span>

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

<span data-ttu-id="d6cb7-302">서버 SDK는 특정 종속성 호출(예: 데이터베이스 및 REST API)을 자동으로 검색하고 추적하는 [종속성 모듈](app-insights-asp-net-dependencies.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="d6cb7-303">모듈 작업을 만들기 위해 서버에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="d6cb7-304">자동화된 추적에서 포착하지 않는 호출을 추적하려는 경우 또는 에이전트를 설치하지 않으려는 경우, 이 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="d6cb7-305">표준 종속성 추적 모듈을 해제하려면 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)를 편집하고 `DependencyCollector.DependencyTrackingTelemetryModule`에 대한 참조를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="d6cb7-306">분석의 종속성</span><span class="sxs-lookup"><span data-stu-id="d6cb7-306">Dependencies in Analytics</span></span>

<span data-ttu-id="d6cb7-307">[Application Insights 분석](app-insights-analytics.md)에서 trackDependency 호출은 `dependencies` 테이블에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="d6cb7-308">[샘플링](app-insights-sampling.md)이 작동 중이면 itemCount 속성에 1보다 큰 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="d6cb7-309">예를 들어 itemCount==10은 trackDependency()에 대한 10개 호출의 샘플링을 의미하며 샘플링 프로세스는 이 중 하나만 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="d6cb7-310">대상 구성 요소별로 분할된 정확한 종속 수를 가져오려면 다음과 같은 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="d6cb7-311">종속성을 관련 요청과 연결하려면 다음과 같이 조인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="d6cb7-312">데이터 플러시</span><span class="sxs-lookup"><span data-stu-id="d6cb7-312">Flushing data</span></span>
<span data-ttu-id="d6cb7-313">일반적으로 SDK는 사용자에 미치는 영향을 최소화하기 위해 선택한 시간에 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="d6cb7-314">그러나 버퍼를 플러시하려는 경우가 있습니다. 종료되는 응용 프로그램에서 SDK를 사용하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="d6cb7-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="d6cb7-316">함수는 [서버 원격 분석 채널](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)에 대해 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="d6cb7-317">인증된 사용자</span><span class="sxs-lookup"><span data-stu-id="d6cb7-317">Authenticated users</span></span>
<span data-ttu-id="d6cb7-318">웹앱에서 사용자는 기본적으로 쿠키로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="d6cb7-319">사용자가 다른 컴퓨터 또는 브라우저에서 앱에 액세스하거나 쿠키를 삭제하는 경우 두 번 이상 계산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="d6cb7-320">사용자가 앱에 로그인하면 브라우저 코드에서 인증된 사용자 ID를 설정하여 보다 정확한 개수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="d6cb7-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="d6cb7-322">ASP.NET 웹 MVC 응용 프로그램에서의 예:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="d6cb7-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="d6cb7-324">사용자의 실제 로그인 이름을 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="d6cb7-325">해당 사용자에게 고유한 ID이기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="d6cb7-326">공백이나 `,;=|` 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="d6cb7-327">사용자 ID도 세션 쿠키에 설정되고 서버로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="d6cb7-328">서버 SDK가 설치된 경우 인증된 사용자 ID가 클라이언트 및 서버 원격 분석 둘 다에 대한 컨텍스트 속성의 일부로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="d6cb7-329">필터링하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-329">You can then filter and search on it.</span></span>

<span data-ttu-id="d6cb7-330">앱이 사용자를 계정으로 그룹화하는 경우 계정 식별자를 전달할 수도 있습니다(동일한 문자 제한이 적용됨).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="d6cb7-331">[메트릭 탐색기](app-insights-metrics-explorer.md)에서 **사용자, 인증** 및 **사용자 계정**을 계산하는 차트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="d6cb7-332">특정 사용자 이름과 계정으로 클라이언트 데이터 지점을 [검색](app-insights-diagnostic-search.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="d6cb7-333"><a name="properties"></a>속성을 사용하여 데이터를 필터링, 검색 및 세분화</span><span class="sxs-lookup"><span data-stu-id="d6cb7-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="d6cb7-334">이벤트에(그리고 메트릭, 페이지 보기, 예외 및 기타 원격 분석 데이터에) 속성 및 측정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="d6cb7-335">*속성*은 사용 현황 보고서에서 원격 분석을 필터링하는 데 사용할 수 있는 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="d6cb7-336">예를 들어 앱이 여러 게임을 제공하는 경우 각 이벤트에 게임 이름을 연결하여 인기가 더 많은 게임을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="d6cb7-337">문자열 길이는 8192로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="d6cb7-338">많은 양의 데이터를 보내려면 메시지 매개 변수 [TrackTrace](#track-trace)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="d6cb7-339">*메트릭* 은 그래픽으로 표시할 수 있는 숫자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="d6cb7-340">예를 들어 게이머의 획득 점수가 점진적으로 증가하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="d6cb7-341">여러 게임에 대한 별도의 그래프 또는 누적 그래프를 볼 수 있도록 이벤트와 함께 전송된 속성을 사용하여 그래프를 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="d6cb7-342">메트릭 값을 올바르게 표시하려면 0보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="d6cb7-343">[속성 수, 속성 값 및 메트릭에 사용 가능한 제한](#limits) 이 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="d6cb7-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-344">*JavaScript*</span></span>

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


<span data-ttu-id="d6cb7-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="d6cb7-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="d6cb7-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="d6cb7-348">속성에 개인 식별이 가능한 정보를 기록하지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="d6cb7-349">*메트릭을 사용한 경우* 메트릭 탐색기를 열고 **사용자 지정** 그룹에서 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![메트릭 탐색기를 열고, 차트를 선택하고, 메트릭을 선택합니다.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="d6cb7-351">메트릭이 표시되지 않거나 **사용자 지정** 머리글이 없는 경우 선택 블레이드를 닫고 나중에 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="d6cb7-352">때로는 메트릭이 파이프라인을 통해 집계되는 데 한 시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="d6cb7-353">*속성 및 메트릭을 사용한 경우*속성에 따라 메트릭을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![그룹화를 설정한 다음 그룹화 기준 아래에서 속성을 선택합니다.](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="d6cb7-355">*진단 검색*에서 개별 이벤트 항목의 속성 및 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![인스턴스를 선택한 다음 '...'를 선택합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="d6cb7-357">**검색** 필드를 사용하여 특정 속성 값이 포함된 이벤트 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![검색에 용어를 입력합니다.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="d6cb7-359">[검색 식에 대해 자세히 알아보세요](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="d6cb7-360">속성 및 메트릭을 설정하는 또 다른 방법</span><span class="sxs-lookup"><span data-stu-id="d6cb7-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="d6cb7-361">이벤트 매개 변수를 별도의 개체에 수집하는 방법이 더 편하다면 이 방법을 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="d6cb7-362">Track*()을 여러 번 호출하기 위해 같은 원격 분석 항목 인스턴스(이 예에서 `event`)를 다시 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="d6cb7-363">그러면 원격 분석을 잘못된 구성과 함께 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="d6cb7-364">분석의 사용자 지정 측정 및 속성</span><span class="sxs-lookup"><span data-stu-id="d6cb7-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="d6cb7-365">[분석](app-insights-analytics.md)에서 사용자 지정 메트릭 및 속성은 각 원격 분석 레코드의 `customMeasurements` 및 `customDimensions` 특성에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="d6cb7-366">예를 들어 요청 원격 분석에 "game"이라는 속성을 추가한 경우 다음 쿼리는 "game"의 값이 다를 때마다의 횟수를 계산하여 사용자 지정 메트릭 "score"의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="d6cb7-367">다음에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-367">Notice that:</span></span>

* <span data-ttu-id="d6cb7-368">customDimensions 또는 customMeasurements JSON에서 값을 추출하면 동적 유형이므로 `tostring` 또는 `todouble`로 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="d6cb7-369">[샘플링](app-insights-sampling.md)의 가능성을 고려하려면 `count()`가 아닌 `sum(itemCount)`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="d6cb7-370"><a name="timed"></a> 타이밍 이벤트</span><span class="sxs-lookup"><span data-stu-id="d6cb7-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="d6cb7-371">작업을 수행하는 데 걸리는 시간을 차트로 표시하고 싶은 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="d6cb7-372">예를 들어 게임에서 사용자가 옵션을 선택하는 데 걸리는 시간을 알고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="d6cb7-373">이를 위해 측정 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="d6cb7-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="d6cb7-375"><a name="defaults"></a>사용자 지정 원격 분석에 대한 기본 속성</span><span class="sxs-lookup"><span data-stu-id="d6cb7-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="d6cb7-376">작성하는 사용자 정의 이벤트의 일부에 대해 기본 속성 값을 설정하려는 경우 TelemetryClient 인스턴스에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="d6cb7-377">설정된 값은 해당 클라이언트에서 보낸 모든 원격 분석 항목에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="d6cb7-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="d6cb7-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="d6cb7-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="d6cb7-381">개별 원격 분석 호출이 자신의 속성 사전에 있는 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="d6cb7-382">*JavaScript 웹 클라이언트의 경우*[JavaScript 원격 분석 이니셜라이저를 사용합니다](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="d6cb7-383">표준 컬렉션 모듈의 데이터를 포함하여 *모든 원격 분석에 속성을 추가하려면* [`ITelemetryInitializer`를 구현합니다](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="d6cb7-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="d6cb7-384">원격 분석 샘플링, 필터링 및 처리</span><span class="sxs-lookup"><span data-stu-id="d6cb7-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="d6cb7-385">SDK에서 전송하기 전에 원격 분석을 처리하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="d6cb7-386">처리는 HTTP 요청 컬렉션 및 종속성 컬렉션과 같은 표준 원격 분석 모듈에서 전송된 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="d6cb7-387">`ITelemetryInitializer`를 구현하여 원격 분석에 [속성을 추가](app-insights-api-filtering-sampling.md#add-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="d6cb7-388">예를 들어 다른 속성에서 계산된 버전 번호 또는 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="d6cb7-389">`ITelemetryProcesor`를 구현하여 원격 분석이 SDK에서 전송되기 전에 [필터링](app-insights-api-filtering-sampling.md#filtering)을 통해 원격 분석을 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="d6cb7-390">전송 또는 삭제될 대상을 제어하지만 메트릭에 미치는 영향을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="d6cb7-391">항목 삭제 방법에 따라 관련된 항목 사이를 이동하는 기능이 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="d6cb7-392">[샘플링](app-insights-api-filtering-sampling.md)은 앱에서 포털로 전송되는 데이터의 양을 줄이는 패키지 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="d6cb7-393">표시된 메트릭에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="d6cb7-394">예외, 요청 및 페이지 뷰와 같은 관련된 항목 간을 이동하여 문제를 진단하는 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="d6cb7-395">[자세히 알아보세요](app-insights-api-filtering-sampling.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="d6cb7-396">원격 분석 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="d6cb7-396">Disabling telemetry</span></span>
<span data-ttu-id="d6cb7-397">원격 분석의 컬렉션 및 전송을 *동적으로 중지 및 시작하려면* :</span><span class="sxs-lookup"><span data-stu-id="d6cb7-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="d6cb7-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="d6cb7-399">*선택한 표준 수집기(예: 성능 카운터, HTTP 요청 또는 종속성)를 사용하지 않도록 설정*하려면 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 관련 줄을 삭제하거나 주석으로 처리합니다. 사용자 고유의 TrackRequest 데이터를 전송하려는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="d6cb7-400"><a name="debug"></a>개발자 모드</span><span class="sxs-lookup"><span data-stu-id="d6cb7-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="d6cb7-401">디버깅하는 동안 결과를 즉시 볼 수 있도록 파이프라인을 통해 원격 분석을 신속하게 처리할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="d6cb7-402">또한 원격 분석과 관련된 모든 문제를 추적하는 데 도움이 되는 추가 메시지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="d6cb7-403">앱이 느려질 수 있으므로 프로덕션 환경에서는 끄는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="d6cb7-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="d6cb7-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="d6cb7-406"><a name="ikey"></a> 선택한 사용자 지정 원격 분석에 대해 계측 키 설정</span><span class="sxs-lookup"><span data-stu-id="d6cb7-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="d6cb7-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="d6cb7-408"><a name="dynamic-ikey"></a> 동적 계측 키</span><span class="sxs-lookup"><span data-stu-id="d6cb7-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="d6cb7-409">개발, 테스트 및 프로덕션 환경에서 원격 분석이 섞이지 않게 방지하려면 [별도의 Application Insights 리소스를 만들고](app-insights-create-new-resource.md) 환경에 따라 키를 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="d6cb7-410">구성 파일에서 계측 키를 가져오는 대신 코드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="d6cb7-411">ASP.NET 서비스의 global.aspx.cs 같은 초기화 메서드에서 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="d6cb7-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="d6cb7-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="d6cb7-414">웹 페이지에서 문자 그대로 스크립트에 코딩하는 대신 웹 서버의 상태를 이용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="d6cb7-415">예를 들어 ASP.NET 앱에서 생성된 웹 페이지에서 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="d6cb7-416">*Razor에서 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="d6cb7-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="d6cb7-417">TelemetryContext</span></span>
<span data-ttu-id="d6cb7-418">TelemetryClient에는 컨텍스트 속성이 있고, 이 속성은 모든 원격 분석 데이터와 함께 전송되는 값을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="d6cb7-419">일반적으로 표준 원격 분석 모듈에 의해 설정되지만 사용자가 직접 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="d6cb7-420">예:</span><span class="sxs-lookup"><span data-stu-id="d6cb7-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="d6cb7-421">이러한 값을 직접 설정하는 경우 사용자의 값과 표준 값이 혼동되지 않도록 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 관련 줄을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="d6cb7-422">**Component**: 앱 및 앱 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="d6cb7-423">**Device**: 앱이 실행되는 장치에 대한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="d6cb7-424">(웹앱에서 원격 분석이 전송되는 서버 또는 클라이언트 장치입니다.)</span><span class="sxs-lookup"><span data-stu-id="d6cb7-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="d6cb7-425">**InstrumentationKey**: Azure에서 원격 분석이 표시되는 Application Insights 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="d6cb7-426">일반적으로 ApplicationInsights.config에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="d6cb7-427">**Location**: 장치의 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="d6cb7-428">**Operation**: 웹앱에서 현재 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="d6cb7-429">다른 유형의 앱에서는 이 값을 설정하여 이벤트를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="d6cb7-430">**Id**: 진단 검색의 이벤트를 검사할 때 "항목 관련"을 찾을 수 있도록 여러 이벤트를 상호 연결하는 생성된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="d6cb7-431">**Name**: 식별자이며, 일반적으로 HTTP 요청의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="d6cb7-432">**SyntheticSource**: null이거나 비어 있지 않다면 요청의 원본이 로봇 또는 웹 테스트로 확인되었음을 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="d6cb7-433">기본적으로 메트릭 탐색기의 계산에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="d6cb7-434">**Properties**: 모든 원격 분석 데이터와 함께 전송되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="d6cb7-435">개별 Track* 호출에서 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="d6cb7-436">**Session**: 사용자의 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-436">**Session**: The user's session.</span></span> <span data-ttu-id="d6cb7-437">ID는 생성된 값으로 설정되며, 사용자가 잠시 동안 비활성 상태이면 값이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="d6cb7-438">**User**: 사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="d6cb7-439">제한</span><span class="sxs-lookup"><span data-stu-id="d6cb7-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="d6cb7-440">데이터 속도 제한에 도달하지 않도록 하려면 [샘플링](app-insights-sampling.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="d6cb7-441">데이터 유지 기간을 결정하려면 [데이터 보존 및 개인 정보](app-insights-data-retention-privacy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="d6cb7-442">참조 문서</span><span class="sxs-lookup"><span data-stu-id="d6cb7-442">Reference docs</span></span>
* [<span data-ttu-id="d6cb7-443">ASP.NET 참조</span><span class="sxs-lookup"><span data-stu-id="d6cb7-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="d6cb7-444">Java 참조</span><span class="sxs-lookup"><span data-stu-id="d6cb7-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="d6cb7-445">JavaScript 참조</span><span class="sxs-lookup"><span data-stu-id="d6cb7-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="d6cb7-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="d6cb7-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="d6cb7-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="d6cb7-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="d6cb7-448">SDK 코드</span><span class="sxs-lookup"><span data-stu-id="d6cb7-448">SDK code</span></span>
* [<span data-ttu-id="d6cb7-449">ASP.NET 핵심 SDK</span><span class="sxs-lookup"><span data-stu-id="d6cb7-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="d6cb7-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="d6cb7-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="d6cb7-451">Windows Server 패키지</span><span class="sxs-lookup"><span data-stu-id="d6cb7-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="d6cb7-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="d6cb7-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="d6cb7-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="d6cb7-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="d6cb7-454">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="d6cb7-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="d6cb7-455">질문</span><span class="sxs-lookup"><span data-stu-id="d6cb7-455">Questions</span></span>
* <span data-ttu-id="d6cb7-456">*Track_() 호출에서 발생할 수 있는 예외는 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="d6cb7-457">없음.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-457">None.</span></span> <span data-ttu-id="d6cb7-458">try-catch 절에 래핑할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="d6cb7-459">SDK에 문제가 발생하는 경우 디버그 콘솔 출력에 메시지를 작성하고 메시지가 완료되는 경우 진단 검색에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="d6cb7-460">*포털에서 데이터를 가져오는 REST API가 있나요?*</span><span class="sxs-lookup"><span data-stu-id="d6cb7-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="d6cb7-461">예, [데이터 액세스 API](https://dev.applicationinsights.io/)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="d6cb7-462">데이터를 추출하는 다른 방법에는 [Analytics에서 Power BI로 내보내기](app-insights-export-power-bi.md) 및 [연속 내보내기](app-insights-export-telemetry.md)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6cb7-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="d6cb7-463"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6cb7-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="d6cb7-464">검색 이벤트 및 로그</span><span class="sxs-lookup"><span data-stu-id="d6cb7-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="d6cb7-465">문제 해결</span><span class="sxs-lookup"><span data-stu-id="d6cb7-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


