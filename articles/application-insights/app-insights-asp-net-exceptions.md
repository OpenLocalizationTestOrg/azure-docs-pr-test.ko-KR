---
title: "aaaDiagnose 오류와 예외를 웹 Azure Application Insights를 사용 하 여 앱 | Microsoft Docs"
description: "요청 원격 분석과 함께 ASP.NET 앱에서 예외를 캡처합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="37c4a-103">Application Insights를 사용하여 웹앱에서 예외 진단</span><span class="sxs-lookup"><span data-stu-id="37c4a-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="37c4a-104">라이브 웹앱의 예외는 [Application Insights](app-insights-overview.md)에서 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="37c4a-105">Hello 원인을 빠르게 진단할 수 있도록 실패 한 요청 예외 및 hello 클라이언트와 서버 모두에서 다른 이벤트와 연관 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="37c4a-106">예외 보고 설정</span><span class="sxs-lookup"><span data-stu-id="37c4a-106">Set up exception reporting</span></span>
* <span data-ttu-id="37c4a-107">서버 응용 프로그램에서 보고 한 toohave 예외:</span><span class="sxs-lookup"><span data-stu-id="37c4a-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="37c4a-108">앱 코드에서 [Application Insights SDK](app-insights-asp-net.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="37c4a-109">IIS 웹 서버: [Application Insights 에이전트](app-insights-monitor-performance-live-website-now.md)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="37c4a-110">Azure 웹 앱: hello 추가 [Application Insights 확장이](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="37c4a-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="37c4a-111">Java 웹 응용 프로그램: 설치 hello [Java 에이전트](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="37c4a-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="37c4a-112">Hello 설치 [JavaScript 코드 조각을](app-insights-javascript.md) 프로그램 웹 페이지 toocatch 브라우저 예외에서입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="37c4a-113">일부 응용 프로그램 프레임 워크 또는 일부 설정을 사용 하 여 필요한 tootake 몇 가지 추가 단계 toocatch 예외가 더 이상 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="37c4a-114">웹 양식</span><span class="sxs-lookup"><span data-stu-id="37c4a-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="37c4a-115">MVC</span><span class="sxs-lookup"><span data-stu-id="37c4a-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="37c4a-116">Web API 1.*</span><span class="sxs-lookup"><span data-stu-id="37c4a-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="37c4a-117">Web API 2.*</span><span class="sxs-lookup"><span data-stu-id="37c4a-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="37c4a-118">WCF</span><span class="sxs-lookup"><span data-stu-id="37c4a-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="37c4a-119">Visual Studio를 사용하여 예외 진단</span><span class="sxs-lookup"><span data-stu-id="37c4a-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="37c4a-120">디버깅이 설정 된 상태로 Visual Studio toohelp에서 hello 응용 프로그램 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="37c4a-121">F5 키를 사용 하 여 개발 컴퓨터 또는 서버에서 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="37c4a-122">Visual Studio에서 Application Insights 검색 창 hello를 열고 앱에서 toodisplay 이벤트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="37c4a-123">디버그 하는 동안 hello Application Insights 단추를 클릭 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights를 선택한 열려 있습니다.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="37c4a-125">공지 hello 보고서 tooshow 정당한 예외를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="37c4a-126">*예외가 표시되지 않나요? [예외 캡처](#exceptions)를 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="37c4a-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="37c4a-127">예외 보고서 tooshow 해당 스택 추적을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="37c4a-128">Hello 스택 추적 tooopen hello 관련 코드 파일에서에서 선 참조를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="37c4a-129">Hello 코드에서 CodeLens hello 예외에 대 한 데이터를 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![CodeLens 예외 알림.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="37c4a-131">Hello Azure 포털을 사용 하 여 오류 진단</span><span class="sxs-lookup"><span data-stu-id="37c4a-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="37c4a-132">응용 프로그램의 hello Application Insights 개요에서 hello 오류 타일 예외에 대 한 차트 보여 주고 hello 목록과 함께 hello 가장 자주 오류가 발생 하는 Url 요청 HTTP 요청에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![설정 선택, 오류](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="37c4a-134">클릭 hello 중 하나를 통해 실패 예외 hello hello 세부 정보를 볼 수 있습니다, 스택 추적의 hello 목록 tooget tooindividual 발견에서 예외 형식:</span><span class="sxs-lookup"><span data-stu-id="37c4a-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![실패 한 요청 및 예외 세부 정보에서 인스턴스를 hello 예외의 tooinstances 설정 됩니다.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="37c4a-136">**또는** 요청의 hello 목록에서 시작 하 고 관련된 tooit 예외를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="37c4a-137">*예외가 표시되지 않나요? [예외 캡처](#exceptions)를 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="37c4a-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="37c4a-138">사용자 지정 추적 및 로그 데이터</span><span class="sxs-lookup"><span data-stu-id="37c4a-138">Custom tracing and log data</span></span>
<span data-ttu-id="37c4a-139">tooget 진단 데이터를 특정 tooyour 응용 프로그램, 코드 toosend 삽입할 수 있습니다 자신만 원격 분석 데이터.</span><span class="sxs-lookup"><span data-stu-id="37c4a-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="37c4a-140">이 hello 요청, 페이지 보기 및 기타 자동으로 수집 된 데이터와 함께 진단 검색에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="37c4a-141">여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-141">You have several options:</span></span>

* <span data-ttu-id="37c4a-142">[trackevent ()](app-insights-api-custom-events-metrics.md#trackevent) hello 데이터도 보냅니다 진단 검색에서 사용자 지정 이벤트 아래에 표시 되지만 사용 패턴, 모니터링을 위해 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="37c4a-143">이벤트의 이름을 지정하고, [진단 검색을 필터링](app-insights-diagnostic-search.md)할 수 있는 문자열 속성 및 숫자 메트릭 수를 수행할 수있습니다. </span><span class="sxs-lookup"><span data-stu-id="37c4a-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="37c4a-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 를 사용하여 POST 정보와 같은 긴데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="37c4a-145">[TrackException()](#exceptions) 은 스택 추적을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="37c4a-146">[예외에 대해 자세히 알아보세요](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="37c4a-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="37c4a-147">사용자가 이미 Log4Net 또는 NLog와 같은 로깅 프레임워크를 사용하는 경우, 요청과 예외 데이터와 함께 진단 검색 안에서 [이러한 로그를 캡처](app-insights-asp-net-trace-logs.md)하고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="37c4a-148">이러한 이벤트를 열고 toosee [검색](app-insights-diagnostic-search.md)필터를 열고 사용자 지정 이벤트, 추적 또는 예외를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![드릴스루](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="37c4a-150">응용 프로그램 원격 분석을 많이 생성, hello 적응 샘플링 모듈 toohello 포털 이벤트의 대표 일부만 전송 하 여 전송 된 hello 볼륨을 자동으로 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="37c4a-151">관련된 이벤트를 탐색할 수 있도록 동일한 작업을 선택 하거나 그룹으로 선택 취소 해야 하는 hello에 포함 된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="37c4a-152">샘플링에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="37c4a-153">Toosee 게시 데이터를 요청 하는 방법</span><span class="sxs-lookup"><span data-stu-id="37c4a-153">How toosee request POST data</span></span>
<span data-ttu-id="37c4a-154">요청 정보 tooyour 앱 POST 호출에 전송 된 hello 데이터를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="37c4a-155">toohave이이 데이터를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-155">toohave this data reported:</span></span>

* <span data-ttu-id="37c4a-156">[Hello SDK 설치](app-insights-asp-net.md) 응용 프로그램 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="37c4a-157">응용 프로그램 toocall에 코드를 삽입 [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace)합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="37c4a-158">Hello 메시지 매개 변수에서 hello 게시 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="37c4a-159">않으므로 헤드가 허용 toohello 크기 제한 toosend 정당한 hello 중요 한 데이터를 시도해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="37c4a-160">실패 한 요청을 조사 하는 경우 연결 된 hello 추적을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-160">When you investigate a failed request, find hello associated traces.</span></span>  

![드릴스루](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="37c4a-162"><a name="exceptions"></a> 예외 및 관련 진단 데이터 캡처</span><span class="sxs-lookup"><span data-stu-id="37c4a-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="37c4a-163">처음에 표시 되지 않습니다 hello 포털에서 응용 프로그램에서 실패를 야기 하는 모든 hello 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="37c4a-164">모든 브라우저 예외 표시 됩니다 (hello를 사용 하 여 [JavaScript SDK](app-insights-javascript.md) 웹 페이지에서).</span><span class="sxs-lookup"><span data-stu-id="37c4a-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="37c4a-165">IIS가 대부분 서버 예외를 발견 하 고 toowrite 약간의 코드 toosee 해야 하지만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="37c4a-166">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-166">You can:</span></span>

* <span data-ttu-id="37c4a-167">**예외를 명시적으로 기록** 예외 처리기 tooreport hello 예외에서 코드를 삽입 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="37c4a-168">**예외를 자동으로 캡처** 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="37c4a-169">다양 한 유형의 프레임 워크에 대 한 hello 필요한 추가 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="37c4a-170">예외를 명시적으로 보고</span><span class="sxs-lookup"><span data-stu-id="37c4a-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="37c4a-171">hello 가장 간단한 방법은 tooinsert 예외 처리기에서 호출 tooTrackException()입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="37c4a-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="37c4a-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="37c4a-173">C#</span><span class="sxs-lookup"><span data-stu-id="37c4a-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="37c4a-174">VB</span><span class="sxs-lookup"><span data-stu-id="37c4a-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="37c4a-175">hello 속성 및 값 매개 변수는 선택적 이지만 필요한 [필터링 및 추가](app-insights-diagnostic-search.md) 추가 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="37c4a-176">예를 들어 여러 게임을 실행할 수 있는 앱이 있는 경우 모든 hello 예외 보고서 관련된 tooa 특정 게임을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="37c4a-177">Tooeach 사전 처럼 때 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="37c4a-178">브라우저 예외</span><span class="sxs-lookup"><span data-stu-id="37c4a-178">Browser exceptions</span></span>
<span data-ttu-id="37c4a-179">대부분의 브라우저 예외가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="37c4a-180">웹 페이지 콘텐츠 배달 네트워크 또는 다른 도메인에서 스크립트 파일을 포함 하는 경우 스크립트 태그에 hello 특성 확인 ```crossorigin="anonymous"```, 해당 hello 서버 보냅니다 [CORS 헤더](http://enable-cors.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="37c4a-181">이렇게 하면 스택 추적 tooget 및 이러한 리소스에서 처리 되지 않은 JavaScript 예외에 대 한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="37c4a-182">웹 양식</span><span class="sxs-lookup"><span data-stu-id="37c4a-182">Web forms</span></span>
<span data-ttu-id="37c4a-183">Web forms hello HTTP 모듈 CustomErrors를 사용 하 여 구성 리디렉션을 없는 경우 수 toocollect hello 예외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="37c4a-184">하지만 활성 리디렉션을 설정한 경우 hello 줄 toohello Application_Error 함수 Global.asax.cs에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="37c4a-185">(아직 없는 경우 Global.asax 파일 추가).</span><span class="sxs-lookup"><span data-stu-id="37c4a-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="37c4a-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="37c4a-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="37c4a-187">MVC</span><span class="sxs-lookup"><span data-stu-id="37c4a-187">MVC</span></span>
<span data-ttu-id="37c4a-188">경우 hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 구성은 `Off`, 예외는 hello에 사용할 수 있는 경우가 [HTTP 모듈](https://msdn.microsoft.com/library/ms178468.aspx) toocollect 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="37c4a-189">그러나이 경우 `RemoteOnly` (기본값), 또는 `On`, 다음 hello 예외가 지워집니다 및 tooautomatically 수집할 Application Insights에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="37c4a-190">Hello를 재정의 하 여이 해결할 수 [System.Web.Mvc.HandleErrorAttribute 클래스](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), hello 다른 버전에 대해 MVC 아래와 같이 재정의 hello 클래스를 적용 하 고 ([github 소스](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="37c4a-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="37c4a-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="37c4a-191">MVC 2</span></span>
<span data-ttu-id="37c4a-192">컨트롤러에서 새 특성으로 hello HandleError 특성을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="37c4a-193">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="37c4a-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="37c4a-194">MVC 3</span></span>
<span data-ttu-id="37c4a-195">Global.asax.cs에서 `AiHandleErrorAttribute` 를 글로벌 필터로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="37c4a-196">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="37c4a-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="37c4a-197">MVC 4, MVC5</span></span>
<span data-ttu-id="37c4a-198">FilterConfig.cs에서 AiHandleErrorAttribute를 글로벌 필터로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="37c4a-199">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="37c4a-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="37c4a-200">Web API 1.x</span></span>
<span data-ttu-id="37c4a-201">System.Web.Http.Filters.ExceptionFilterAttribute를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="37c4a-202">Hello 경우 WebApiConfig 클래스에서 toohello 전역 필터 구성을 추가 하거나이 재정의 된 특성 toospecific 컨트롤러를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="37c4a-203">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="37c4a-204">Hello 예외 필터를 처리할 수 없는 경우에 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="37c4a-205">예:</span><span class="sxs-lookup"><span data-stu-id="37c4a-205">For example:</span></span>

* <span data-ttu-id="37c4a-206">컨트롤러 생성자에서 throw된 예외</span><span class="sxs-lookup"><span data-stu-id="37c4a-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="37c4a-207">메시지 처리기에서 throw된 예외</span><span class="sxs-lookup"><span data-stu-id="37c4a-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="37c4a-208">라우팅 중에 throw된 예외</span><span class="sxs-lookup"><span data-stu-id="37c4a-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="37c4a-209">응답 콘텐츠를 직렬화하는 동안 throw된 예외</span><span class="sxs-lookup"><span data-stu-id="37c4a-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="37c4a-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="37c4a-210">Web API 2.x</span></span>
<span data-ttu-id="37c4a-211">IExceptionLogger를 추가로 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="37c4a-212">경우 WebApiConfig이 toohello 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="37c4a-213">}</span><span class="sxs-lookup"><span data-stu-id="37c4a-213">}</span></span>

[<span data-ttu-id="37c4a-214">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="37c4a-215">또는 다음 방법을 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="37c4a-216">대체 hello IExceptionHandler의 사용자 지정 구현으로 ExceptionHandler만 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="37c4a-217">이 동작은 때 호출 hello 프레임 워크는 응답 메시지 (hello 연결 예를 들어 중단 될 때에 not) toosend 여전히 수 toochoose</span><span class="sxs-lookup"><span data-stu-id="37c4a-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="37c4a-218">(에 설명 된 대로 웹 API 1.x 컨트롤러 위의 hello 섹션)-예외 필터를 모든 경우에에서 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="37c4a-219">WCF</span><span class="sxs-lookup"><span data-stu-id="37c4a-219">WCF</span></span>
<span data-ttu-id="37c4a-220">특성을 확장하고 IErrorHandler 및 IServiceBehavior를 구현하는 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="37c4a-221">Hello 특성 toohello 서비스 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="37c4a-222">샘플</span><span class="sxs-lookup"><span data-stu-id="37c4a-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="37c4a-223">예외 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="37c4a-223">Exception performance counters</span></span>
<span data-ttu-id="37c4a-224">있는 경우 [hello Application Insights 에이전트를 설치](app-insights-monitor-performance-live-website-now.md) 서버에서.NET으로 측정 된 hello 예외 속도 차트를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="37c4a-225">여기에는 처리된 .NET 예외와 처리되지 않은 .NET 예외가 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="37c4a-226">메트릭 탐색기 블레이드를 열고 새 차트를 추가한 다음 성능 카운터 아래에 나열된 **예외 속도**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="37c4a-227">hello.NET framework의 예외 hello 수를 계산 하는 간격에 되며 hello 간격의 길이 hello 나누어 hello 속도 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="37c4a-228">Note 하다는 점을 TrackException 보고서를 계산 하 여 hello Application Insights 포털에서 계산 하는 hello '예외' 개수와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="37c4a-229">hello 샘플링 간격 다르고 hello SDK 모든 처리 및 처리 되지 않은 예외에 대 한 TrackException 보고서를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37c4a-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="37c4a-230">비디오</span><span class="sxs-lookup"><span data-stu-id="37c4a-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="37c4a-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37c4a-231">Next steps</span></span>
* [<span data-ttu-id="37c4a-232">REST, SQL 및 기타 호출 toodependencies 모니터링</span><span class="sxs-lookup"><span data-stu-id="37c4a-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="37c4a-233">페이지 로드 시간, 브라우저 예외 및 AJAX 호출 모니터링</span><span class="sxs-lookup"><span data-stu-id="37c4a-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="37c4a-234">성능 카운터 모니터링</span><span class="sxs-lookup"><span data-stu-id="37c4a-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
