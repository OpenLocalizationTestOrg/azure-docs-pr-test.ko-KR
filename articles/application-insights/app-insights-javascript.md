---
title: "JavaScript 웹앱용 Azure Application Insights | Microsoft Docs"
description: "페이지 보기 및 세션 수와 웹 클라이언트 데이터를 가져오고 사용 패턴을 추적합니다. JavaScript 웹 페이지의 예외 및 성능 문제를 감지합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="60ce0-104">웹 페이지용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="60ce0-104">Application Insights for web pages</span></span>
<span data-ttu-id="60ce0-105">웹 페이지 또는 앱의 성능 및 사용 현황에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="60ce0-106">페이지 스크립트에 [Application Insights](app-insights-overview.md)를 추가하면 페이지 로드 및 AJAX 호출의 타이밍, 브라우저 예외 및 AJAX 실패의 개수 및 세부 정보뿐만 아니라 사용자 및 세션 개수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="60ce0-107">이러한 모든 요소를 페이지, 클라이언트 OS 및 브라우저 버전, 지리적 위치 및 기타 차원으로 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="60ce0-108">실패 횟수 또는 느린 페이지 로딩에 대한 경고를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="60ce0-109">또한 JavaScript 코드에 추적 호출을 삽입하여 웹 페이지 응용 프로그램의 다양한 기능 사용 방법을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="60ce0-110">Application Insights는 다른 웹 페이지와 함께 사용할 수 있습니다. 간단한 JavaScript만 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="60ce0-111">웹 서비스가 [Java](app-insights-java-get-started.md) 또한 [ASP.NET](app-insights-asp-net.md)인 경우, 서버 및 클라이언트의 원격 분석을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![portal.azure.com에서 앱의 리소스 열고 브라우저를 클릭합니다.](./media/app-insights-javascript/03.png)

<span data-ttu-id="60ce0-113">[Microsoft Azure](https://azure.com)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="60ce0-114">팀에 조직 구독이 있는 경우 자신의 Microsoft 계정을 여기에 추가해도 되는지 소유자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="60ce0-115">개발 및 소규모 사용에는 별도의 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="60ce0-116">웹 페이지용 Application Insights 설치</span><span class="sxs-lookup"><span data-stu-id="60ce0-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="60ce0-117">웹 페이지에 다음과 같이 로더 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="60ce0-118">Application Insights 리소스 열기 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="60ce0-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="60ce0-119">Application Insights 리소스는 페이지의 성능 및 사용 현황에 대한 데이터가 표시되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="60ce0-120">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="60ce0-121">응용 프로그램의 서버측에 대한 모니터링을 이미 설정한 경우 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![찾아보기, 개발자 서비스, Application Insights를 선택합니다.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="60ce0-123">계정이 없는 경우 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-123">If you don't have one, create it:</span></span>

![새로 만들기, 개발자 서비스, Application Insights를 선택합니다.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="60ce0-125">*벌써 질문이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="60ce0-125">*Questions already?*</span></span> <span data-ttu-id="60ce0-126">[리소스 만들기에 대해 자세히 알아보세요](app-insights-create-new-resource.md)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="60ce0-127">앱 또는 웹 페이지에 SDK 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="60ce0-128">빠른 시작에서 웹 페이지용 스크립트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-128">In Quick Start, get the script for web pages:</span></span>

![앱 개요 블레이드에서 빠른 시작, 내 웹 페이지를 모니터링할 코드 가져오기를 선택합니다.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="60ce0-131">추적하려는 모든 페이지의 `</head>` 태그 바로 앞의 이 스크립트를 삽입합니다. 웹 사이트에 마스터 페이지가 있는 경우 이 페이지에 스크립트를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="60ce0-132">예:</span><span class="sxs-lookup"><span data-stu-id="60ce0-132">For example:</span></span>

* <span data-ttu-id="60ce0-133">ASP.NET MVC 프로젝트에서는 `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="60ce0-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="60ce0-134">SharePoint 사이트의 경우 제어판에서 [사이트 설정/마스터 페이지](app-insights-sharepoint.md)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="60ce0-135">스크립트에는 Application Insights 리소스에 데이터를 전달하는 계측 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="60ce0-136">([스크립트에 대한 자세한 설명.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="60ce0-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="60ce0-137">*(잘 알려진 웹 페이지 프레임워크를 사용하는 경우 Application Insights 어댑터를 찾아보세요. 예를 들어 [AngularJS 모듈](http://ngmodules.org/modules/angular-appinsights)이 있습니다.)*</span><span class="sxs-lookup"><span data-stu-id="60ce0-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="60ce0-138">자세한 구성</span><span class="sxs-lookup"><span data-stu-id="60ce0-138">Detailed configuration</span></span>
<span data-ttu-id="60ce0-139">몇 가지 [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)를 설정할 수 있지만 대부분의 경우에서 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="60ce0-140">예를 들어, 트래픽을 줄이기 위해 페이지 보기 당 보고된 Ajax 호출 수를 사용하지 않도록 설정하거나 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="60ce0-141">또는 디버그 모드를 설정하여 배치되지 않고 파이프라인을 통해 원격 분석을 빠르게 이동시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="60ce0-142">이러한 매개 변수를 설정하려면 코드 조각에서 이 줄을 찾고 쉼표로 구분하여 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="60ce0-143">[사용 가능한 매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) 는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="60ce0-144"><a name="run"></a>앱 실행</span><span class="sxs-lookup"><span data-stu-id="60ce0-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="60ce0-145">웹앱을 실행하고, 잠깐 사용하여 원격 분석을 생성하고, 잠시 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="60ce0-146">개발 컴퓨터에서 **F5** 키를 사용하여 실행하거나 사용자가 실행할 수 있도록 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="60ce0-147">웹앱에서 Application Insights로 보내는 원격 분석을 확인하려면 브라우저의 디버깅 도구(대부분의 브라우저는**F12** 키)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="60ce0-148">데이터가 dc.services.visualstudio.com으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="60ce0-149">브라우저 성능 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="60ce0-149">Explore your browser performance data</span></span>
<span data-ttu-id="60ce0-150">사용자의 브라우저에서 집계된 성능 데이터를 표시하도록 브라우저 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![Portal.azure.com에서 앱의 리소스 열고 설정, 브라우저를 클릭합니다.](./media/app-insights-javascript/03.png)

<span data-ttu-id="60ce0-152">*아직 아무 데이터도 없나요? 페이지 위쪽에서 **새로 고침**을 클릭합니다. 여전히 아무 데이터도 없나요? [문제 해결](app-insights-troubleshoot-faq.md)을 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="60ce0-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="60ce0-153">브라우저 블레이드는 미리 설정된 필터와 차트를 선택할 수 있는 [메트릭 탐색기 블레이드](app-insights-metrics-explorer.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="60ce0-154">원하는 경우 시간 범위, 필터 및 차트 구성을 편집하고 즐겨찾기로 결과를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="60ce0-155">**기본값 복원**을 클릭하여 원래 블레이드 구성으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="60ce0-156">페이지 로드 성능</span><span class="sxs-lookup"><span data-stu-id="60ce0-156">Page load performance</span></span>
<span data-ttu-id="60ce0-157">맨 위에 있는 것이 페이지 로드 시간의 분할된 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="60ce0-158">차트의 전체 높이는 사용자의 브라우저의 앱에서 페이지를 로드하고 페이지를 표시하는 평균 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="60ce0-159">레이아웃 및 실행 스크립트를 포함하여 모든 동기 로드 이벤트가 처리될 때까지 브라우저가 초기 HTTP 요청을 보낼 때부터 시간이 측정됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="60ce0-160">AJAX 호출로부터 웹 파트를 로드하는 등의 비동기 작업은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="60ce0-161">차트는 총 페이지 로드 시간을 [W3C에서 정의한 표준 타이밍](http://www.w3.org/TR/navigation-timing/#processing-model)으로 분할한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="60ce0-162">*네트워크 연결* 시간은 가끔 예상보다 짧습니다. 브라우저에서 서버로 보내는 모든 요청의 평균값이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="60ce0-163">서버에 대한 활성 연결이 이미 있기 때문에 연결 시간이 0인 개별 요청이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="60ce0-164">로드가 느립니까?</span><span class="sxs-lookup"><span data-stu-id="60ce0-164">Slow loading?</span></span>
<span data-ttu-id="60ce0-165">느린 페이지 로드는 사용자가 가장 불만족을 느끼는 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="60ce0-166">차트가 느린 페이지 로드를 나타내는 경우, 일부 진단 조사를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="60ce0-167">차트는 앱에서 모든 페이지를 로드하는 평균 시간을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="60ce0-168">이 문제가 특정 페이지에 국한되는지 확인하려면, 블레이드 아래의 페이지 URL별로 분류된 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60ce0-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="60ce0-169">페이지 보기 수 및 표준 편차를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="60ce0-170">페이지 수가 매우 낮은 경우 사용자에게 큰 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="60ce0-171">높은 표준 편차(자체 평균 비교 시)는 개별 측정값 간의 차이가 많음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="60ce0-172">**한 URL 및 한 페이지 보기에서 확대합니다.**</span><span class="sxs-lookup"><span data-stu-id="60ce0-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="60ce0-173">해당 URL에 대해서만 필터링된 브라우저 차트의 블레이드를 보려면 페이지 이름을 클릭한 다음, 페이지 보기의 인스턴스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="60ce0-174">`...`을(를) 클릭하여 해당 이벤트에 대한 속성의 전체 목록을 보거나 Ajax 호출 및 관련된 이벤트를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="60ce0-175">느린 Ajax 호출은 동기화할 때 전체 페이지 로드 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="60ce0-176">관련된 이벤트에는 동일한 URL에 대한 서버 요청을 포함합니다(웹 서버에서 Application Insights를 설정한 경우).</span><span class="sxs-lookup"><span data-stu-id="60ce0-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="60ce0-177">**시간에 따른 페이지 성능**</span><span class="sxs-lookup"><span data-stu-id="60ce0-177">**Page performance over time.**</span></span> <span data-ttu-id="60ce0-178">브라우저 블레이드로 돌아와서 특정 시간에 최대치가 있는지 확인하기 위해 페이지 보기 로드 시간 표를 꺾은선형 차트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![표의 머리글을 클릭하고 새 차트 종류를 선택합니다.](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="60ce0-180">**다른 차원으로 분류**</span><span class="sxs-lookup"><span data-stu-id="60ce0-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="60ce0-181">특정 브라우저, 클라이언트 OS 또는 사용자 거주지에 따라 페이지 로드 시간이 느려질 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="60ce0-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="60ce0-182">새 차트를 추가하고 **Group-by** 차원을 실험해봅니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="60ce0-183">AJAX 성능</span><span class="sxs-lookup"><span data-stu-id="60ce0-183">AJAX Performance</span></span>
<span data-ttu-id="60ce0-184">웹 페이지의 모든 AJAX 호출이 정상적으로 수행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="60ce0-185">종종 페이지의 부분들을 비동기적으로 채우는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="60ce0-186">전체 페이지가 신속하게 로드되더라도 사용자는 빈 웹 부분을 응시하면서 데이터가 표시되기를 기다리는 데 불만을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="60ce0-187">웹 페이지에서 이루어진 AJAX 호출은 브라우저 블레이드에 종속성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="60ce0-188">블레이드의 상단 부분에 있는 요약 차트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="60ce0-189">그리고 상세한 표가 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="60ce0-190">특정 세부 정보를 보려면 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="60ce0-191">블레이드에서 브라우저 필터를 삭제하면 서버와 AJAX 종속성이 이 차트에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="60ce0-192">필터를 다시 구성하려면 기본값 복원을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="60ce0-193">**실패한 Ajax 호출을 분석하려면** 종속성 실패 그리드로 아래로 스크롤한 다음, 보려는 특정 인스턴스의 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="60ce0-194">Ajax 호출에 대한 전체 원격 분석을 하려면 `...`을(를) 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="60ce0-195">Ajax 호출이 보고되지 않았습니까?</span><span class="sxs-lookup"><span data-stu-id="60ce0-195">No Ajax calls reported?</span></span>
<span data-ttu-id="60ce0-196">Ajax 호출은 웹 페이지의 스크립트에서 이루어진 HTTP/HTTPS 호출을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="60ce0-197">보고된 호출이 없는 경우, 코드 조각이 `disableAjaxTracking` 또는 `maxAjaxCallsPerView` [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)를 설정하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="60ce0-198">브라우저 예외</span><span class="sxs-lookup"><span data-stu-id="60ce0-198">Browser exceptions</span></span>
<span data-ttu-id="60ce0-199">브라우저 블레이드에는 예외 요약 차트가 있고 좀 더 아래에는 예외 형식의 표가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="60ce0-200">보고된 브라우저 예외가 없는 경우, 코드 조각이 `disableExceptionTracking` [매개 변수](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)를 설정하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="60ce0-201">개별 페이지 보기 이벤트 검사</span><span class="sxs-lookup"><span data-stu-id="60ce0-201">Inspect individual page view events</span></span>

<span data-ttu-id="60ce0-202">일반적으로 페이지 보기 원격 분석은 Application Insights에서 분석하며 모든 사용자에 대해 계산된 평균이 포함된 누적 보고서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="60ce0-203">그러나 디버깅을 위해 개별 페이지 보기 이벤트를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="60ce0-204">진단 검색 블레이드에서 필터를 페이지 보기로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="60ce0-205">보다 자세한 정보를 확인하려면 원하는 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-205">Select any event to see more detail.</span></span> <span data-ttu-id="60ce0-206">세부 정보 페이지에서 더 자세한 정보를 보려면 "..."를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="60ce0-207">[Search](app-insights-diagnostic-search.md)를 사용하는 경우 전체 단어가 일치해야 합니다. "Abou"와 "bout"은 "About"과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="60ce0-208">또한 강력한 [Log Analytics 쿼리 언어](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table)를 사용하여 페이지 보기를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="60ce0-209">페이지 보기 속성</span><span class="sxs-lookup"><span data-stu-id="60ce0-209">Page view properties</span></span>
* <span data-ttu-id="60ce0-210">**페이지 보기 기간**</span><span class="sxs-lookup"><span data-stu-id="60ce0-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="60ce0-211">기본적으로 클라이언트 요청에서 전체 로드로 페이지를 로드하는 데 걸리는 시간(보조 파일을 포함하지만 Ajax 호출과 같은 비동기 작업은 제외)입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="60ce0-212">[페이지 구성](#detailed-configuration)에서 `overridePageViewDuration`을 설정한 경우 첫 번째 `trackPageView` 실행에 대한 클라이언트 요청 간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="60ce0-213">스크립트의 초기화 후 일반적인 위치에서 trackPageView를 이동한 경우 다른 값이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="60ce0-214">`overridePageViewDuration`을 설정하고 `trackPageView()` 호출에서 기간 인수가 제공된 경우 인수 값이 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="60ce0-215">사용자 지정 페이지 수</span><span class="sxs-lookup"><span data-stu-id="60ce0-215">Custom page counts</span></span>
<span data-ttu-id="60ce0-216">기본적으로는 새 페이지를 클라이언트 브라우저로 로드할 때마다 페이지 수가 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="60ce0-217">그러나 추가 페이지 보기를 계산에 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-217">But you might want to count additional page views.</span></span> <span data-ttu-id="60ce0-218">예를 들어 탭에 콘텐츠가 표시되는 페이지에서 사용자가 탭을 전환할 때 페이지 수를 계산하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="60ce0-219">또는 페이지의 JavaScript 코드가 브라우저 URL은 변경하지 않고 새 콘텐츠를 로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="60ce0-220">클라이언트 코드의 적절한 지점에 다음과 같은 JavaScript 호출을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="60ce0-221">페이지 이름은 URL과 같은 문자를 포함할 수 있지만 "#" 또는 "?" 뒤의 모든 문자는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60ce0-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="60ce0-222">사용 추적</span><span class="sxs-lookup"><span data-stu-id="60ce0-222">Usage tracking</span></span>
<span data-ttu-id="60ce0-223">사용자가 앱으로 어떤 작업을 수행하려고 하는지 확인하고 싶나요?</span><span class="sxs-lookup"><span data-stu-id="60ce0-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="60ce0-224">사용 추적에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="60ce0-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="60ce0-225">[사용자 지정 이벤트 및 메트릭 API에 대해 자세히 알아보세요](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="60ce0-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="60ce0-226"><a name="video"></a>동영상</span><span class="sxs-lookup"><span data-stu-id="60ce0-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="60ce0-227"><a name="next"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="60ce0-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="60ce0-228">사용 현황 추적</span><span class="sxs-lookup"><span data-stu-id="60ce0-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="60ce0-229">사용자 지정 이벤트 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="60ce0-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="60ce0-230">빌드 - 측정 - 학습</span><span class="sxs-lookup"><span data-stu-id="60ce0-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

