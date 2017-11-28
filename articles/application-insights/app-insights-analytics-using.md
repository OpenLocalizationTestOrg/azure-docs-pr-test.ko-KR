---
title: "Analytics 사용 - Azure Application Insights의 강력한 검색 도구 | Microsoft Docs"
description: "Application Insights의 강력한 진단 검색 도구인 Analytics를 사용하는 방법에 대해 설명합니다. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="e5ded-103">Application Insights에서 Analytics 사용</span><span class="sxs-lookup"><span data-stu-id="e5ded-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="e5ded-104">[분석](app-insights-analytics.md)은 [Application Insights](app-insights-overview.md)의 강력한 검색 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e5ded-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="e5ded-106">**[소개 비디오 보기](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**</span><span class="sxs-lookup"><span data-stu-id="e5ded-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="e5ded-107">앱이 아직 데이터를 Application Insights로 전송하지 않은 경우, **[시뮬레이션된 데이터에 대한 분석을 테스트](https://analytics.applicationinsights.io/demo)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="e5ded-108">Analytics 열기</span><span class="sxs-lookup"><span data-stu-id="e5ded-108">Open Analytics</span></span>
<span data-ttu-id="e5ded-109">Application Insights의 앱 홈 리소스에서 Analytics를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="e5ded-111">인라인 자습서에서 수행할 수 있는 몇 가지 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="e5ded-112">[보다 광범위한 둘러보기는 여기](app-insights-analytics-tour.md)서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="e5ded-113">원격 분석 쿼리</span><span class="sxs-lookup"><span data-stu-id="e5ded-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="e5ded-114">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="e5ded-114">Write a query</span></span>
![스키마 표시](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="e5ded-116">왼쪽에 나열된 테이블의 이름(또는 [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) 또는 [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) 연산자)으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="e5ded-117">[연산자](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html) 파이프라인을 만들려면 `|`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="e5ded-118">IntelliSense에 사용할 수 있는 연산자 및 식 요소를 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="e5ded-119">정보 아이콘을 클릭하거나 Ctrl+스페이스바를 눌러 보다 긴 설명 및 각 요소를 사용하는 방법에 대한 예제를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="e5ded-120">[Analytics 언어 개요](app-insights-analytics-tour.md) 및 [언어 참조](app-insights-analytics-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5ded-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="e5ded-121">쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="e5ded-121">Run a query</span></span>
![쿼리 실행](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="e5ded-123">쿼리에서는 단일 줄 바꿈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="e5ded-124">실행하려는 쿼리의 내부 또는 끝에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="e5ded-125">쿼리 시간 범위를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-125">Check the time range of your query.</span></span> <span data-ttu-id="e5ded-126">쿼리에 고유한 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 절을 포함하여 재정의하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="e5ded-127">이동을 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="e5ded-128">쿼리에 빈 줄을 넣으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="e5ded-129">빈 줄로 구분하여 하나의 쿼리 탭에서 분리된 여러 개의 쿼리를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="e5ded-130">커서가 있는 쿼리만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="e5ded-131">쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="e5ded-131">Save a query</span></span>
![쿼리 저장](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="e5ded-133">현재 쿼리 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-133">Save the current query file.</span></span>
2. <span data-ttu-id="e5ded-134">저장된 쿼리 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-134">Open a saved query file.</span></span>
3. <span data-ttu-id="e5ded-135">새 쿼리 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="e5ded-136">세부 정보 참조</span><span class="sxs-lookup"><span data-stu-id="e5ded-136">See the details</span></span>
<span data-ttu-id="e5ded-137">속성의 전체 목록을 보려면 결과의 행을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="e5ded-138">구조화된 값이 있는 속성(예: 사용자 지정 차원 또는 예외에 나열된 스택)을 추가로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![행 확장](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="e5ded-140">결과 정렬</span><span class="sxs-lookup"><span data-stu-id="e5ded-140">Arrange the results</span></span>
<span data-ttu-id="e5ded-141">쿼리에서 반환된 결과를 정렬하고, 필터링하고, 페이지를 매기고, 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="e5ded-142">브라우저에서 정렬, 그룹화 및 필터링을 수행해도 쿼리가 다시 실행되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="e5ded-143">마지막 쿼리에서 반환된 결과만 다시 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="e5ded-144">결과가 반환하기 전에 서버에서 이러한 작업을 수행하려면 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 및 [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 연산자를 사용하여 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="e5ded-145">보려는 열을 선택하고, 열 머리글을 끌어 다시 정렬하고, 테두리를 끌어 열 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![열 정렬](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="e5ded-147">항목 정렬 및 필터</span><span class="sxs-lookup"><span data-stu-id="e5ded-147">Sort and filter items</span></span>
<span data-ttu-id="e5ded-148">열의 제목을 클릭하여 결과를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="e5ded-149">다른 방법으로 정렬하려면 다시 클릭하고, 쿼리에서 반환된 원래 순서로 되돌리려면 세 번째로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="e5ded-150">필터 아이콘을 사용하여 검색 범위를 좁힙니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-150">Use the filter icon to narrow your search.</span></span>

![열 정렬 및 필터링](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="e5ded-152">항목 그룹화</span><span class="sxs-lookup"><span data-stu-id="e5ded-152">Group items</span></span>
<span data-ttu-id="e5ded-153">둘 이상의 열로 정렬하려면 그룹화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="e5ded-154">먼저 사용하도록 설정한 후 열 머리글을 테이블 위의 공간으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-154">First enable it, and then drag column headers into the space above the table.</span></span>

![그룹](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="e5ded-156">일부 결과가 누락되었나요?</span><span class="sxs-lookup"><span data-stu-id="e5ded-156">Missing some results?</span></span>

<span data-ttu-id="e5ded-157">예상한 결과 중 일부가 표시되지 않는 경우 두 가지 가능한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="e5ded-158">**시간 범위 필터**.</span><span class="sxs-lookup"><span data-stu-id="e5ded-158">**Time range filter**.</span></span> <span data-ttu-id="e5ded-159">기본적으로 지난 24시간 동안의 결과만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="e5ded-160">원본 테이블에서 검색된 결과의 범위를 제한하는 자동 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="e5ded-161">그러나 드롭다운 메뉴를 사용하여 시간 범위 필터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="e5ded-162">또는 [`where  ... timestamp ...` 절](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)을 쿼리에 포함하여 자동 범위를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="e5ded-163">예:</span><span class="sxs-lookup"><span data-stu-id="e5ded-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="e5ded-164">**결과 제한**.</span><span class="sxs-lookup"><span data-stu-id="e5ded-164">**Results limit**.</span></span> <span data-ttu-id="e5ded-165">포털에서 반환된 결과에 대해 약 10,000개의 행 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="e5ded-166">이 제한을 초과하면 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="e5ded-167">이런 경우 테이블의 결과를 정렬한다고 해서 항상 첫 번째 또는 마지막 실제 결과가 모두 표시되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="e5ded-168">이 제한에 도달하지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="e5ded-169">시간 범위 필터를 사용하거나 다음과 같은 연산자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="e5ded-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="e5ded-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="e5ded-171">take 100</span><span class="sxs-lookup"><span data-stu-id="e5ded-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="e5ded-172">summarize </span><span class="sxs-lookup"><span data-stu-id="e5ded-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="e5ded-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="e5ded-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="e5ded-174">10,000개가 넘는 행을 원하는 경우</span><span class="sxs-lookup"><span data-stu-id="e5ded-174">(Want more than 10k rows?</span></span> <span data-ttu-id="e5ded-175">[연속 내보내기](app-insights-export-telemetry.md)를 대신 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="e5ded-176">Analytics는 원시 데이터를 검색하기 위한 것이 아니라 분석용으로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="e5ded-177">다이어그램</span><span class="sxs-lookup"><span data-stu-id="e5ded-177">Diagrams</span></span>
<span data-ttu-id="e5ded-178">원하는 다이어그램의 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-178">Select the type of diagram you'd like:</span></span>

![다이어그램 유형 선택](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="e5ded-180">적합한 유형의 열이 여러 개인 경우 x축과 y축 및 결과 정렬 기준으로 사용할 크기의 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="e5ded-181">기본적으로 결과는 처음에는 테이블로 표시되며 다이어그램은 수동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="e5ded-182">하지만 쿼리 끝에 [render 지시문](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) 을 사용하여 다이어그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="e5ded-183">분석 진단</span><span class="sxs-lookup"><span data-stu-id="e5ded-183">Analytics diagnostics</span></span>


<span data-ttu-id="e5ded-184">시간 차트에서 데이터에 갑작스러운 스파이크 또는 단계가 나타날 경우 선에서 강조 표시된 점을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="e5ded-185">이것은 분석 진단이 급격한 변화를 필터링하는 속성 조합을 확인했다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="e5ded-186">해당 점을 클릭하여 필터에 대한 자세한 내용을 확인하고 필터링된 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="e5ded-187">이렇게 하면 변화의 원인을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="e5ded-188">진단 분석에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="e5ded-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![분석 진단](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="e5ded-190">대시보드에 고정</span><span class="sxs-lookup"><span data-stu-id="e5ded-190">Pin to dashboard</span></span>
<span data-ttu-id="e5ded-191">다이어그램 또는 테이블을 [대시보드 공유](app-insights-dashboards.md) 중 하나에 고정할 수 있습니다. 핀을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="e5ded-192">(이 기능을 설정하려면 [앱의 가격 패키지를 업그레이드](app-insights-pricing.md)해야 할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e5ded-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![핀 클릭](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="e5ded-194">즉, 웹 서비스의 성능 또는 사용 현황을 모니터링하기 위해 대시보드를 함께 사용하는 경우 매우 복잡한 분석을 기타 메트릭과 함께 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="e5ded-195">테이블에 열이 네 개 이하인 경우 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="e5ded-196">상위 7개의 행만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="e5ded-197">대시보드 새로 고침</span><span class="sxs-lookup"><span data-stu-id="e5ded-197">Dashboard refresh</span></span>
<span data-ttu-id="e5ded-198">대시보드에 고정된 차트는 약 1시간마다 쿼리를 다시 실행하여 자동으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="e5ded-199">새로 고침 단추를 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="e5ded-200">자동 단순화</span><span class="sxs-lookup"><span data-stu-id="e5ded-200">Automatic simplifications</span></span>

<span data-ttu-id="e5ded-201">차트를 대시보드에 고정할 때 특정 단순화가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="e5ded-202">**시간 제한:** 쿼리는 지난 14일로 자동으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="e5ded-203">이는 쿼리에 `where timestamp > ago(14d)`를 포함한 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="e5ded-204">**Bin 수 제한:** 수많은 불연속 막대(일반적으로 가로 막대형 차트)가 있는 차트를 표시할 경우 덜 채워진 막대가 하나의 "기타" 막대로 자동으로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="e5ded-205">예를 들어 다음 쿼리는</span><span class="sxs-lookup"><span data-stu-id="e5ded-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="e5ded-206">분석에서 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-206">looks like this in Analytics:</span></span>

![길게 늘어지는 차트](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="e5ded-208">하지만 대시보드에 이를 고정하면 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-208">but when you pin it to a dashboard, it looks like this:</span></span>

![제한된 막대가 있는 차트](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="e5ded-210">Excel로 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5ded-210">Export to Excel</span></span>
<span data-ttu-id="e5ded-211">쿼리를 실행한 후 .csv 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="e5ded-212">**Excel로 내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="e5ded-213">Power BI에 내보내기</span><span class="sxs-lookup"><span data-stu-id="e5ded-213">Export to Power BI</span></span>
<span data-ttu-id="e5ded-214">쿼리에 커서를 놓고 **Power BI로 내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Analytics에서 Power BI로 내보내기](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="e5ded-216">Power BI에서 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-216">You run the query in Power BI.</span></span> <span data-ttu-id="e5ded-217">일정에 따라 새로 고침을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="e5ded-218">Power BI를 사용하여 다양한 원본에서 데이터를 결합하는 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="e5ded-219">Power BI에 내보내기에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e5ded-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="e5ded-220">딥 링크</span><span class="sxs-lookup"><span data-stu-id="e5ded-220">Deep link</span></span>

<span data-ttu-id="e5ded-221">다른 사용자에게 보낼 수 있는 **공유 링크로 내보내기**에서 링크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="e5ded-222">사용자에게 [리소스 그룹에 대한 액세스 권한](app-insights-resources-roles-access-control.md)이 있는 경우 해당 쿼리가 Analytics UI에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="e5ded-223">(링크에서 쿼리 텍스트는 "?q=", gzip 압축 및 base-64 인코딩 다음에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="e5ded-224">코드를 작성하여 사용자에게 제공하는 딥 링크를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="e5ded-225">단, [REST API](https://dev.applicationinsights.io/)를 사용하여 코드에서 분석을 실행하는 것이 좋습니다.)</span><span class="sxs-lookup"><span data-stu-id="e5ded-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="e5ded-226">Automation</span><span class="sxs-lookup"><span data-stu-id="e5ded-226">Automation</span></span>

<span data-ttu-id="e5ded-227">[데이터 액세스 REST API](https://dev.applicationinsights.io/)를 실행하여 분석 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="e5ded-228">[예](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count)(PowerShell 사용):</span><span class="sxs-lookup"><span data-stu-id="e5ded-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="e5ded-229">분석 UI와는 달리 REST API가 타임스탬프 제한을 쿼리에 자동으로 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="e5ded-230">엄청난 응답을 받지 않으려면 반드시 where-clause를 직접 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="e5ded-231">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="e5ded-231">Import data</span></span>

<span data-ttu-id="e5ded-232">CSV 파일에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-232">You can import data from a CSV file.</span></span> <span data-ttu-id="e5ded-233">일반적인 용도는 원격 분석에서 테이블을 결합할 수 있는 정적 데이터를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="e5ded-234">예를 들어 원격 분석에서 인증된 사용자가 별칭 또는 임시 ID로 식별되는 경우 별칭을 실제 이름에 매핑하는 테이블을를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="e5ded-235">요청 원격 분석에서 조인을 수행하여 Analytics 보고서의 실제 이름으로 사용자를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="e5ded-236">데이터 스키마 정의</span><span class="sxs-lookup"><span data-stu-id="e5ded-236">Define your data schema</span></span>

1. <span data-ttu-id="e5ded-237">**설정**(왼쪽 위), **데이터 원본**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="e5ded-238">지침에 따라 데이터 원본을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="e5ded-239">10개 이상의 행을 포함해야 하는 데이터의 샘플을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="e5ded-240">그런 다음 스키마를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-240">You then correct the schema.</span></span>

<span data-ttu-id="e5ded-241">그러면 개별 테이블을 가져오는 데 사용할 수 있는 데이터 원본이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="e5ded-242">테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="e5ded-242">Import a table</span></span>

1. <span data-ttu-id="e5ded-243">목록에서 데이터 원본 정의를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="e5ded-244">"업로드"를 클릭하고 지침에 따라 테이블을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="e5ded-245">여기에는 REST API에 대한 호출이 포함되므로 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="e5ded-246">이제 Analytics 쿼리에서 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="e5ded-247">Analytics에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="e5ded-248">테이블 사용</span><span class="sxs-lookup"><span data-stu-id="e5ded-248">Use the table</span></span>

<span data-ttu-id="e5ded-249">`usermap`이라는 데이터 원본 정의가 있고 여기에 `realName` 및 `user_AuthenticatedId`라는 두 개의 필드가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="e5ded-250">`requests` 테이블에도 `user_AuthenticatedId` 필드가 있으므로 쉽게 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="e5ded-251">요청의 결과 테이블에는 `realName`이라는 추가 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="e5ded-252">LogStash에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="e5ded-252">Import from LogStash</span></span>

<span data-ttu-id="e5ded-253">[LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html)를 사용하는 경우 Analytics를 사용하여 로그를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="e5ded-254">[Analytics로 데이터를 파이프하는 플러그 인](https://github.com/Microsoft/logstash-output-application-insights)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ded-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="e5ded-255">비디오</span><span class="sxs-lookup"><span data-stu-id="e5ded-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

