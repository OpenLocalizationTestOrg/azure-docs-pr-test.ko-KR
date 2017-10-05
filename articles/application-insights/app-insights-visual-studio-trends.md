---
title: "Visual Studio에서 추세 분석 | Microsoft Docs"
description: "Visual Studio의 Application Insights 원격 분석에서 추세를 분석, 시각화 및 탐색합니다."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 13fca37303296355ce601333b13110d04fa5fa4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="analyzing-trends-in-visual-studio"></a><span data-ttu-id="5d326-103">Visual Studio에서 추세 분석</span><span class="sxs-lookup"><span data-stu-id="5d326-103">Analyzing Trends in Visual Studio</span></span>
<span data-ttu-id="5d326-104">Application Insights 추세 도구는 웹 응용 프로그램의 중요한 원격 분석 이벤트가 시간이 지남에 따라 어떻게 변했는지 시각화하여, 문제와 잘못된 부분을 신속하게 식별하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-104">The Application Insights Trends tool visualizes how your web application's important telemetry events change over time, helping you quickly identify problems and anomalies.</span></span> <span data-ttu-id="5d326-105">더 자세한 진단 정보에 연결하면 추세를 통해 앱의 성능을 향상시키고 예외의 원인을 추적하며 사용자 지정 이벤트로부터 새로운 정보를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-105">By linking you to more detailed diagnostic information, Trends can help you improve your app's performance, track down the causes of exceptions, and uncover insights from your custom events.</span></span>

![예제 추세 창](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a><span data-ttu-id="5d326-107">Application Insights의 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="5d326-107">Configure your web app for Application Insights</span></span>

<span data-ttu-id="5d326-108">이 작업을 아직 수행하지 않은 경우 [Application Insights의 웹앱을 구성](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-108">If you haven't done this already, [configure your web app for Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5d326-109">그러면 Application Insights 포털에 원격 분석을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-109">This allows it to send telemetry to the Application Insights portal.</span></span> <span data-ttu-id="5d326-110">추세 도구에서는 원격 분석 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-110">The Trends tool reads the telemetry from there.</span></span>

<span data-ttu-id="5d326-111">Application Insights 추세는 Visual Studio 2015 업데이트 3 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-111">Application Insights Trends is available in Visual Studio 2015 Update 3 and later.</span></span>

## <a name="open-application-insights-trends"></a><span data-ttu-id="5d326-112">Application Insights 추세 열기</span><span class="sxs-lookup"><span data-stu-id="5d326-112">Open Application Insights Trends</span></span>
<span data-ttu-id="5d326-113">Application Insights 추세 창을 열려면:</span><span class="sxs-lookup"><span data-stu-id="5d326-113">To open the Application Insights Trends window:</span></span>

* <span data-ttu-id="5d326-114">Application Insights 도구 모음 단추에서 **원격 분석 추세 탐색**을 선택합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="5d326-114">From the Application Insights toolbar button, choose **Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="5d326-115">프로젝트 상황에 맞는 메뉴에서 **Application Insights > 원격 분석 추세 탐색**을 선택합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="5d326-115">From the project context menu, choose **Application Insights > Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="5d326-116">Visual Studio 메뉴 모음에서 **보기 > 다른 창 > Application Insights 추세**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-116">From the Visual Studio menu bar, choose **View > Other Windows > Application Insights Trends**.</span></span>

<span data-ttu-id="5d326-117">리소스를 선택하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-117">You may see a prompt to select a resource.</span></span> <span data-ttu-id="5d326-118">**리소스 선택**을 클릭하고 Azure 구독을 사용하여 로그인한 다음, 원격 분석 추세를 분석하려는 목록에서 Application Insights 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-118">Click **Select a resource**, sign in with an Azure subscription, then choose an Application Insights resource from the list for which you'd like to analyze telemetry trends.</span></span>

## <a name="choose-a-trend-analysis"></a><span data-ttu-id="5d326-119">추세 분석 선택</span><span class="sxs-lookup"><span data-stu-id="5d326-119">Choose a trend analysis</span></span>
![일반적인 유형의 추세 분석 메뉴](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

<span data-ttu-id="5d326-121">지난 24시간 동안의 데이터를 각각 분석한 5개의 공통 추세 분석 중에서 하나를 선택하여 다음을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-121">Get started by choosing from one of five common trend analyses, each analyzing data from the last 24 hours:</span></span>

* <span data-ttu-id="5d326-122">**서버 요청을 통해 성능 문제 조사** - 서비스에 대한 요청으로, 응답 시간별로 그룹화됨</span><span class="sxs-lookup"><span data-stu-id="5d326-122">**Investigate performance issues with your server requests** - Requests made to your service, grouped by response times</span></span>
* <span data-ttu-id="5d326-123">**서버 요청에서 오류 분석** - 서비스에 대한 요청으로, HTTP 응답 코드별로 그룹화됨</span><span class="sxs-lookup"><span data-stu-id="5d326-123">**Analyze errors in your server requests** - Requests made to your service, grouped by HTTP response code</span></span>
* <span data-ttu-id="5d326-124">**응용 프로그램에서 예외 검사** - 서비스의 예외로, 예외 유형별로 그룹화됨</span><span class="sxs-lookup"><span data-stu-id="5d326-124">**Examine the exceptions in your application** - Exceptions from your service, grouped by exception type</span></span>
* <span data-ttu-id="5d326-125">**응용 프로그램의 종속성 성능 확인** - 서비스별로 호출된 서비스로, 서비스 응답 시간별로 그룹화됨</span><span class="sxs-lookup"><span data-stu-id="5d326-125">**Check the performance of your application's dependencies** - Services called by your service, grouped by response times</span></span>
* <span data-ttu-id="5d326-126">**사용자 지정 이벤트 검사** - 서비스에 대해 설정한 사용자 지정 이벤트로, 이벤트 유형별로 그룹화됨</span><span class="sxs-lookup"><span data-stu-id="5d326-126">**Inspect your custom events** - Custom events you've set up for your service, grouped by event type.</span></span>

<span data-ttu-id="5d326-127">이들 미리 작성된 분석은 추세 창의 왼쪽 위 모서리에 있는 **일반적인 유형의 원격 분석 보기** 단추를 통해 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-127">These pre-built analyses are available later from the **View common types of telemetry analysis** button in the upper-left corner of the Trends window.</span></span>

## <a name="visualize-trends-in-your-application"></a><span data-ttu-id="5d326-128">응용 프로그램에서 추세 시각화</span><span class="sxs-lookup"><span data-stu-id="5d326-128">Visualize trends in your application</span></span>
<span data-ttu-id="5d326-129">Application Insights 추세는 앱의 원격 분석으로부터 시계열 시각화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-129">Application Insights Trends creates a time series visualization from your app's telemetry.</span></span> <span data-ttu-id="5d326-130">각 시계열 시각화는 어떤 시간 범위 동안 한 원격 분석 유형을 표시하며, 해당 원격 분석의 한 가지 속성으로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-130">Each time series visualization displays one type of telemetry, grouped by one property of that telemetry, over some time range.</span></span> <span data-ttu-id="5d326-131">예를 들어 지난 24시간 동안 출신 국가별로 그룹화하여 서버 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-131">For example, you might want to view server requests, grouped by the country from which they originated, over the last 24 hours.</span></span> <span data-ttu-id="5d326-132">이 예에서 시각화의 각 거품은 1시간 동안 일부 국가/지역에 대한 서버 요청 수를 나타낸 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-132">In this example, each bubble on the visualization would represent a count of the server requests for some country/region during one hour.</span></span>

<span data-ttu-id="5d326-133">창 맨 위에 있는 컨트롤을 사용하여 보려는 유형의 원격 분석 데이터를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-133">Use the controls at the top of the window to adjust what types of telemetry you view.</span></span> <span data-ttu-id="5d326-134">첫째, 다음과 같이 관심 있는 원격 분석 유형 선택을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-134">First, choose the telemetry types in which you're interested:</span></span>

* <span data-ttu-id="5d326-135">**원격 분석 유형** - 서버 요청, 예외, 종속성 또는 사용자 지정 이벤트</span><span class="sxs-lookup"><span data-stu-id="5d326-135">**Telemetry Type** - Server requests, exceptions, depdendencies, or custom events</span></span>
* <span data-ttu-id="5d326-136">**시간 범위** - 지난 30분에서 지난 3일까지의 범위</span><span class="sxs-lookup"><span data-stu-id="5d326-136">**Time Range** - Anywhere from the last 30 minutes to the last 3 days</span></span>
* <span data-ttu-id="5d326-137">**그룹별** - 예외 형식, 문제 ID, 국가/지역 등</span><span class="sxs-lookup"><span data-stu-id="5d326-137">**Group By** - Exception type, problem ID, country/region, and more.</span></span>

<span data-ttu-id="5d326-138">그런 다음 **분석 원격 분석** 을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-138">Then, click **Analyze Telemetry** to run the query.</span></span>

<span data-ttu-id="5d326-139">시각화의 거품 사이를 이동하려면:</span><span class="sxs-lookup"><span data-stu-id="5d326-139">To navigate between bubbles in the visualization:</span></span>

* <span data-ttu-id="5d326-140">한 거품을 클릭하면, 창의 아래쪽에 있는 필터를 업데이트하고 특정 기간 동안 발생한 이벤트만 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-140">Click to select a bubble, which updates the filters at the bottom of the window, summarizing just the events that occurred during a specific time period</span></span>
* <span data-ttu-id="5d326-141">거품을 두 번 클릭하여 검색 도구를 이동하고 해당 기간 동안 발생한 개별 원격 분석 이벤트를 모두 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-141">Double-click a bubble to navigate to the Search tool and see all of the individual telemetry events that occured during that time period</span></span>
* <span data-ttu-id="5d326-142">시각화 요소에서 선택 취소하려면 거품을 Ctrl 키를 누르고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-142">Ctrl-click a bubble to de-select it in the visualization.</span></span>

> [!TIP]
> <span data-ttu-id="5d326-143">추세 및 검색 도구를 함께 사용하면 수천 개의 원격 분석 이벤트 중에서 서비스 문제의 원인을 찾는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-143">The Trends and Search tools work together to help you pinpoint the causes of issues in your service among thousands of telemetry events.</span></span> <span data-ttu-id="5d326-144">예를 들어, 어느 날 오후 고객이 앱의 응답 속도 저하를 인지한 경우 추세를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-144">For example, if one afternoon your customers notice your app is being less responsive, start with Trends.</span></span> <span data-ttu-id="5d326-145">지난 몇 시간 동안 서비스에 대한 요청을 분석하여, 응답 시간별로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-145">Analyze requests made to your service over the past several hours, grouped by response time.</span></span> <span data-ttu-id="5d326-146">비정상적으로 큰 느린 요청 클러스터가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-146">See if there's an unusually large cluster of slow requests.</span></span> <span data-ttu-id="5d326-147">그런 다음 해당 거품을 두 번 클릭하여 검색 도구로 이동하고 요청 이벤트에 대해 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-147">Then double click that bubble to go to the Search tool, filtered to those request events.</span></span> <span data-ttu-id="5d326-148">검색에서 요청 내용을 탐색할 수 있으며 문제를 해결하기 위해 관련 코드로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-148">From Search, you can explore the contents of those requests and navigate to the code involved to resolve the issue.</span></span>
> 
> 

## <a name="filter"></a><span data-ttu-id="5d326-149">Filter</span><span class="sxs-lookup"><span data-stu-id="5d326-149">Filter</span></span>
<span data-ttu-id="5d326-150">창의 맨 아래에서 필터 컨트롤로 보다 구체적인 추세를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-150">Discover more specific trends with the filter controls at the bottom of the window.</span></span> <span data-ttu-id="5d326-151">필터를 적용하려면 해당 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-151">To apply a filter, click on its name.</span></span> <span data-ttu-id="5d326-152">원격 분석의 특정 차원에 숨어 있을 수 있는 추세를 검색하기 위해 여러 필터 사이를 신속하게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-152">You can quickly switch between different filters to discover trends that may be hiding in a particular dimension of your telemetry.</span></span> <span data-ttu-id="5d326-153">예외 형식 등 한 차원에서 필터를 적용하는 경우, 흐리게 표시되더라도 다른 차원의 필터를 클릭할 수 있습니다. 필터를 적용하지 않으려면 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-153">If you apply a filter in one dimension, like Exception Type, filters in other dimensions remain clickable even though they appear grayed-out. To un-apply a filter, click it again.</span></span> <span data-ttu-id="5d326-154">동일한 차원의 여러 필터를 선택하려면 Ctrl 키를 누르고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-154">Ctrl-click to select multiple filters in the same dimension.</span></span>

![추세 필터](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

<span data-ttu-id="5d326-156">여러 필터를 적용하려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="5d326-156">What if you want to apply multiple filters?</span></span> 

1. <span data-ttu-id="5d326-157">첫 번째 필터를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-157">Apply the first filter.</span></span> 
2. <span data-ttu-id="5d326-158">첫 번째 필터 차원의 이름 옆에 있는 **선택한 필터를 적용하고 다시 쿼리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-158">Click the **Apply selected filters and query again** button by the name of the dimension of your first filter.</span></span> <span data-ttu-id="5d326-159">이렇게 하면 첫 번째 필터와 일치하는 이벤트에 대해서만 원격 분석을 다시 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-159">This will re-query your telemetry for only events that match the first filter.</span></span> 
3. <span data-ttu-id="5d326-160">두 번째 필터를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-160">Apply a second filter.</span></span> 
4. <span data-ttu-id="5d326-161">원격 분석의 특정 하위 집합에서 추세를 찾기 위해 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-161">Repeat the process to find trends in specific subsets of your telemetry.</span></span> <span data-ttu-id="5d326-162">예를 들어, "GET Home/Index"라는 서버 요청 *및* 독일에서 발생한 서버 요청 *및* 500 응답 코드를 수신한 서버 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-162">For example, server requests named "GET Home/Index" *and* that came from Germany *and* that received a 500 response code.</span></span> 

<span data-ttu-id="5d326-163">이들 필터 중 하나를 적용하지 않으려면 해당 차원의 **선택한 필터를 제거하고 다시 쿼리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-163">To un-apply one of these filters, click the **Remove selected filters and query again** button for the dimension.</span></span>

![여러 필터](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a><span data-ttu-id="5d326-165">잘못된 부분을 찾기</span><span class="sxs-lookup"><span data-stu-id="5d326-165">Find anomalies</span></span>
<span data-ttu-id="5d326-166">추세 도구는 같은 시계열에서 다른 거품에 비해 비정상적인 거품 이벤트를 강조 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-166">The Trends tool can highlight bubbles of events that are anomalous compared to other bubbles in the same time series.</span></span> <span data-ttu-id="5d326-167">보기 유형 드롭다운에서 **시간 버킷의 수(변칙 강조 표시)** 또는 **시간 버킷의 백분율(변칙 강조 표시)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-167">In the View Type dropdown, choose **Counts in time bucket (highlight anomalies)** or **Percentages in time bucket (highlight anomalies)**.</span></span> <span data-ttu-id="5d326-168">빨간색 거품이 잘못된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-168">Red bubbles are anomalous.</span></span> <span data-ttu-id="5d326-169">거품의 개수/비율이 지난 두 기간(지난 24시간을 보는 경우 48시간 등) 동안 발생한 개수/비율의 표준 편차를 2.1배 초과하는 경우 잘못된 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-169">Anomalies are defined as bubbles with counts/percentages exceeding 2.1 times the standard deviation of the counts/percentages that occured in the past two time periods (48 hours if you're viewing the last 24 hours, etc.).</span></span>

![컬러 점은 잘못된 부분을 나타냅니다.](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> <span data-ttu-id="5d326-171">잘못된 부분을 강조 표시하면, 그렇지 않은 경우 비슷하게 보일 수 있는 작은 거품의 시계열에서 이상값을 찾는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-171">Highlighting anomalies is especially helpful for finding outliers in time series of small bubbles that may otherwise look similarly sized.</span></span>  
> 
> 

## <span data-ttu-id="5d326-172"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d326-172"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="5d326-173">**[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="5d326-173">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="5d326-174">원격 분석을 검색하고, CodeLens에서 데이터를 확인하며, Application Insights를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-174">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="5d326-175">Visual Studio 내에서 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-175">All within Visual Studio.</span></span> |![프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 및 검색을 선택합니다.](./media/app-insights-visual-studio-trends/34.png) |
| <span data-ttu-id="5d326-177">**[더 많은 데이터 추가](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="5d326-177">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="5d326-178">사용량, 가용성, 종속성, 예외를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-178">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="5d326-179">로깅 프레임 워크의 추적을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-179">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="5d326-180">사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-180">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio-trends/64.png) |
| <span data-ttu-id="5d326-182">**[Application Insights 포털 사용](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="5d326-182">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="5d326-183">대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기입니다.</span><span class="sxs-lookup"><span data-stu-id="5d326-183">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](./media/app-insights-visual-studio-trends/62.png) |

