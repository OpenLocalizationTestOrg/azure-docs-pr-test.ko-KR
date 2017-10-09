---
title: "aaaUsing 분석-Azure Application Insights의 hello 강력한 검색 도구 | Microsoft Docs"
description: "Hello 분석, Application Insights의 hello 강력한 진단 검색 도구를 사용합니다. "
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
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="173ec-103">Application Insights에서 Analytics 사용</span><span class="sxs-lookup"><span data-stu-id="173ec-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="173ec-104">[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="173ec-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="173ec-106">**[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="173ec-107">**[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="173ec-108">Analytics 열기</span><span class="sxs-lookup"><span data-stu-id="173ec-108">Open Analytics</span></span>
<span data-ttu-id="173ec-109">Application Insights의 앱 홈 리소스에서 Analytics를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="173ec-111">hello 인라인 자습서 수행할 수 있는 작업에 대 한 몇 가지 아이디어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="173ec-112">[보다 광범위한 둘러보기는 여기](app-insights-analytics-tour.md)서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="173ec-113">원격 분석 쿼리</span><span class="sxs-lookup"><span data-stu-id="173ec-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="173ec-114">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="173ec-114">Write a query</span></span>
![스키마 표시](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="173ec-116">Hello 왼쪽에 나열 된 hello 테이블의 이름을 hello로 시작 (또는 hello [범위](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) 또는 [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) 연산자).</span><span class="sxs-lookup"><span data-stu-id="173ec-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="173ec-117">사용 하 여 `|` 의 파이프라인 a toocreate [연산자](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="173ec-118">IntelliSense 메시지 hello 연산자 및 사용할 수 있는 hello 식 요소와 함께 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="173ec-119">Hello 정보 아이콘을 클릭 (또는 CTRL + 스페이스바를 눌러) tooget 방법의 예제 및 자세한 설명과 toouse 각 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="173ec-120">Hello 참조 [분석 언어 자습서](app-insights-analytics-tour.md) 및 [언어 참조](app-insights-analytics-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="173ec-121">쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="173ec-121">Run a query</span></span>
![쿼리 실행](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="173ec-123">쿼리에서는 단일 줄 바꿈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="173ec-124">내부 또는 toorun hello 쿼리 hello 끝나기 전에 hello 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="173ec-125">쿼리 hello 시간 범위를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-125">Check hello time range of your query.</span></span> <span data-ttu-id="173ec-126">쿼리에 고유한 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 절을 포함하여 재정의하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="173ec-127">Go toorun hello 쿼리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="173ec-128">쿼리에 빈 줄을 넣으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="173ec-129">빈 줄로 구분하여 하나의 쿼리 탭에서 분리된 여러 개의 쿼리를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="173ec-130">Hello 커서 변수가 있는 hello 쿼리만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="173ec-131">쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="173ec-131">Save a query</span></span>
![쿼리 저장](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="173ec-133">Hello 현재 쿼리 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-133">Save hello current query file.</span></span>
2. <span data-ttu-id="173ec-134">저장된 쿼리 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-134">Open a saved query file.</span></span>
3. <span data-ttu-id="173ec-135">새 쿼리 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="173ec-136">Hello 세부 정보를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="173ec-136">See hello details</span></span>
<span data-ttu-id="173ec-137">전체 속성 목록이 hello 결과 toosee에 있는 모든 행을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="173ec-138">모든 속성은 구조화 된 값-예를 들어, 사용자 지정 차원 또는 예외가 나열 hello 스택 추가로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![행 확장](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="173ec-140">첫 번째 hello 결과 정렬</span><span class="sxs-lookup"><span data-stu-id="173ec-140">Arrange hello results</span></span>
<span data-ttu-id="173ec-141">있습니다 수 정렬, 필터링, 페이지를 매기는, 및를 쿼리에서 반환 된 hello 결과 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="173ec-142">정렬, 그룹화 및 필터링 hello 브라우저에서 쿼리를 다시 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="173ec-143">마지막 사용자 쿼리에 의해 반환 된 hello 결과 다시 정렬할 경우.</span><span class="sxs-lookup"><span data-stu-id="173ec-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="173ec-144">tooperform hello 결과가 반환 되 면 먼저 hello 서버에서 이러한 작업 hello와 함께 쿼리를 작성 [정렬](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [요약](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 및 [여기서](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="173ec-145">Hello 열 때와 마찬가지로 toosee를 끌 열 머리글 toorearrange 및 기본 형식 및 열 크기 조정 테두리를 끌어 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![열 정렬](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="173ec-147">항목 정렬 및 필터</span><span class="sxs-lookup"><span data-stu-id="173ec-147">Sort and filter items</span></span>
<span data-ttu-id="173ec-148">열의 hello 헤드를 클릭 하 여 결과 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="173ec-149">Toosort hello 다른 방법으로 다시 클릭 하 고 클릭 세 번째로 toorevert toohello 원래 순서 지정 하 여 쿼리에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="173ec-150">검색 필터 아이콘 toonarrow hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-150">Use hello filter icon toonarrow your search.</span></span>

![열 정렬 및 필터링](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="173ec-152">항목 그룹화</span><span class="sxs-lookup"><span data-stu-id="173ec-152">Group items</span></span>
<span data-ttu-id="173ec-153">toosort 둘 이상의 열으로 그룹화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="173ec-154">먼저,를 사용 하도록 설정 하 여 hello 테이블 위에 hello 공간으로 열 머리글을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![그룹](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="173ec-156">일부 결과가 누락되었나요?</span><span class="sxs-lookup"><span data-stu-id="173ec-156">Missing some results?</span></span>

<span data-ttu-id="173ec-157">예상 되는 모든 hello 결과 표시 되지 않으면 생각 되 면 몇 가지 가능한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="173ec-158">**시간 범위 필터**.</span><span class="sxs-lookup"><span data-stu-id="173ec-158">**Time range filter**.</span></span> <span data-ttu-id="173ec-159">기본적으로만 결과가 표시 되며 hello에서 지난 24 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="173ec-160">Hello 원본 테이블에서 검색 된 결과의 hello 범위를 제한 하는 자동 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="173ec-161">그러나 hello 시간 범위를 변경할 수 있습니다 hello 드롭다운 메뉴를 사용 하 여 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="173ec-162">사용자 고유의 포함 하 여 hello 자동 범위를 재정의할 수 있습니다 [ `where  ... timestamp ...` 절](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 쿼리로 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="173ec-163">예:</span><span class="sxs-lookup"><span data-stu-id="173ec-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="173ec-164">**결과 제한**.</span><span class="sxs-lookup"><span data-stu-id="173ec-164">**Results limit**.</span></span> <span data-ttu-id="173ec-165">Hello 포털에서 반환 된 hello 결과에 약 10, 000 행의 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="173ec-166">경고는 hello 제한을 초과할 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="173ec-167">이렇게 되 면 hello 테이블에 결과 정렬 표시 되지 않습니다 항상 하면 모든 hello 실제 첫 번째 또는 마지막 결과.</span><span class="sxs-lookup"><span data-stu-id="173ec-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="173ec-168">것 좋습니다 tooavoid 적중 hello 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="173ec-169">Hello 시간 범위 필터를 사용 하 여 또는 같은 연산자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="173ec-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="173ec-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="173ec-171">take 100</span><span class="sxs-lookup"><span data-stu-id="173ec-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="173ec-172">summarize </span><span class="sxs-lookup"><span data-stu-id="173ec-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="173ec-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="173ec-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="173ec-174">10,000개가 넘는 행을 원하는 경우</span><span class="sxs-lookup"><span data-stu-id="173ec-174">(Want more than 10k rows?</span></span> <span data-ttu-id="173ec-175">[연속 내보내기](app-insights-export-telemetry.md)를 대신 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="173ec-176">Analytics는 원시 데이터를 검색하기 위한 것이 아니라 분석용으로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="173ec-177">다이어그램</span><span class="sxs-lookup"><span data-stu-id="173ec-177">Diagrams</span></span>
<span data-ttu-id="173ec-178">원하는 다이어그램의 hello 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-178">Select hello type of diagram you'd like:</span></span>

![다이어그램 유형 선택](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="173ec-180">Hello 오른쪽 형식의 여러 열이 있으면 hello x 및 y 축을 기준으로 차원 toosplit hello 결과의 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="173ec-181">기본적으로 결과 테이블로 처음 표시 하 고 hello 다이어그램을 수동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="173ec-182">Hello를 사용할 수 있지만 [지시문 렌더링](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) 쿼리 tooselect 다이어그램의 hello 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="173ec-183">분석 진단</span><span class="sxs-lookup"><span data-stu-id="173ec-183">Analytics diagnostics</span></span>


<span data-ttu-id="173ec-184">급증 또는 단계 데이터에 있는 경우는 timechart에서 강조 표시 된 hello 선 위의 점을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="173ec-185">이 분석 진단 hello 갑자기 변화를 필터링 하는 속성의 조합에 식별에 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="173ec-186">Hello 지점 tooget hello 필터 및 toosee hello에 대 한 필터링 된 버전에서 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="173ec-187">이 변경 내용 발생된 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="173ec-188">진단 분석에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="173ec-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![분석 진단](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="173ec-190">Pin toodashboard</span><span class="sxs-lookup"><span data-stu-id="173ec-190">Pin toodashboard</span></span>
<span data-ttu-id="173ec-191">다이어그램이 나 테이블 tooone 고정할 수 있는 프로그램 [대시보드를 공유](app-insights-dashboards.md) -hello pin 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="173ec-192">(너무 해야[앱 가격 책정 패키지 업그레이드](app-insights-pricing.md) tooturn이이 기능을 합니다.)</span><span class="sxs-lookup"><span data-stu-id="173ec-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Hello pin을 클릭 합니다.](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="173ec-194">이 때 hello 성능 또는 웹 서비스의 사용을 모니터링할 대시보드 toohelp 종합적으로 포함할 수 있습니다 hello와 함께 매우 복잡 한 분석 기타 메트릭을 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="173ec-195">4 개 이하의 열 있으면 테이블 toohello 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="173ec-196">Hello 상위 7 개의 행만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="173ec-197">대시보드 새로 고침</span><span class="sxs-lookup"><span data-stu-id="173ec-197">Dashboard refresh</span></span>
<span data-ttu-id="173ec-198">hello 차트 고정 toohello 대시보드는 대략 시간 마다 hello 쿼리를 다시 실행 하 여 자동으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="173ec-199">Hello 새로 고침 단추를 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="173ec-200">자동 단순화</span><span class="sxs-lookup"><span data-stu-id="173ec-200">Automatic simplifications</span></span>

<span data-ttu-id="173ec-201">특정 가정을 tooa 대시보드에 고정 하면 적용된 tooa 차트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="173ec-202">**시간 제한을:** 쿼리는 자동으로 제한 toohello 지난 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="173ec-203">hello 효과 hello 동일한 쿼리에 포함 하는 경우 `where timestamp > ago(14d)`합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="173ec-204">**Bin 개수 제한:** 개별 저장소 (일반적으로 가로 막대형 차트의 경우) 덜 채워진된 bin는 자동으로 그룹화 되어 단일 "기타" hello 많이 포함 하는 차트를 표시 하는 경우 범주화 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="173ec-205">예를 들어 다음 쿼리는</span><span class="sxs-lookup"><span data-stu-id="173ec-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="173ec-206">분석에서 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-206">looks like this in Analytics:</span></span>

![길게 늘어지는 차트](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="173ec-208">하지만 tooa 대시보드 고정 때 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![제한된 막대가 있는 차트](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="173ec-210">TooExcel 내보내기</span><span class="sxs-lookup"><span data-stu-id="173ec-210">Export tooExcel</span></span>
<span data-ttu-id="173ec-211">쿼리를 실행한 후 .csv 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="173ec-212">**Excel로 내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="173ec-213">내보내기 tooPower BI</span><span class="sxs-lookup"><span data-stu-id="173ec-213">Export tooPower BI</span></span>
<span data-ttu-id="173ec-214">쿼리에서 hello 커서를 놓고 선택 **내보내기, Power BI**합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![BI 분석 tooPower에서 내보내기](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="173ec-216">Power BI에서 hello 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-216">You run hello query in Power BI.</span></span> <span data-ttu-id="173ec-217">일정에 따라 toorefresh 것 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="173ec-218">Power BI를 사용하여 다양한 원본에서 데이터를 결합하는 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="173ec-219">내보내기 tooPower BI에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="173ec-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="173ec-220">딥 링크</span><span class="sxs-lookup"><span data-stu-id="173ec-220">Deep link</span></span>

<span data-ttu-id="173ec-221">아래 링크 받기 **내보내기, 공유 링크** tooanother 사용자를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="173ec-222">Hello 사용자에 게 제공 [액세스 tooyour 리소스 그룹](app-insights-resources-roles-access-control.md), hello 쿼리 hello 분석 UI에서에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="173ec-223">(Hello 링크 hello 쿼리 텍스트 뒤에 표시 "? q =", gzip 압축 및 base 64 인코딩.</span><span class="sxs-lookup"><span data-stu-id="173ec-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="173ec-224">Toousers 제공 하는 코드 toogenerate 딥 링크를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="173ec-225">그러나 hello 코드에서 분석 방법은 toorun hello를 사용 하는 것을 권장 [REST API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="173ec-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="173ec-226">Automation</span><span class="sxs-lookup"><span data-stu-id="173ec-226">Automation</span></span>

<span data-ttu-id="173ec-227">사용 하 여 hello [데이터 액세스 REST API](https://dev.applicationinsights.io/) toorun 분석 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="173ec-228">[예](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count)(PowerShell 사용):</span><span class="sxs-lookup"><span data-stu-id="173ec-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="173ec-229">Hello 분석 UI, 달리 hello REST API 추가 되지 않습니다 자동으로 타임 스탬프 제한 tooyour 쿼리.</span><span class="sxs-lookup"><span data-stu-id="173ec-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="173ec-230">사용자 고유의 where 절, 거 대 한 응답을 얻기 tooavoid tooadd를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="173ec-231">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="173ec-231">Import data</span></span>

<span data-ttu-id="173ec-232">CSV 파일에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-232">You can import data from a CSV file.</span></span> <span data-ttu-id="173ec-233">일반적인 사용법은 tooimport 정적 데이터 원격 분석에서 테이블 가입할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="173ec-234">예를 들어 인증 된 사용자는 원격 분석에서 별칭 또는 난독 처리 된 id에서 지정 하는 경우 별칭 tooreal 이름을 매핑하는 테이블을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="173ec-235">조인을 hello 요청 원격 분석을 수행 하면 hello 분석 보고서의 실제 이름으로 사용자를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="173ec-236">데이터 스키마 정의</span><span class="sxs-lookup"><span data-stu-id="173ec-236">Define your data schema</span></span>

1. <span data-ttu-id="173ec-237">**설정**(왼쪽 위), **데이터 원본**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="173ec-238">Hello 지침을 진행 하 여 데이터 원본에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="173ec-239">toosupply 10 개 이상의 행을 포함 하는 hello 데이터 샘플을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="173ec-240">그런 다음 hello 스키마를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-240">You then correct hello schema.</span></span>

<span data-ttu-id="173ec-241">그런 다음 하 여 데이터 원본에 정의 합니다. tooimport 개별 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="173ec-242">테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="173ec-242">Import a table</span></span>

1. <span data-ttu-id="173ec-243">Hello 목록에서 데이터 원본 정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="173ec-244">"업로드 하세요."를 클릭 하 고 hello 명령 tooupload hello 테이블을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="173ec-245">여기에 호출 tooa REST API, 따라서 쉽게 tooautomate 합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="173ec-246">이제 Analytics 쿼리에서 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="173ec-247">Analytics에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="173ec-248">Hello 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="173ec-248">Use hello table</span></span>

<span data-ttu-id="173ec-249">`usermap`이라는 데이터 원본 정의가 있고 여기에 `realName` 및 `user_AuthenticatedId`라는 두 개의 필드가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="173ec-250">hello `requests` 테이블에도 라는 필드가 `user_AuthenticatedId`쉽게 toojoin 것 이므로, 해당:</span><span class="sxs-lookup"><span data-stu-id="173ec-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="173ec-251">hello 요청의 결과 테이블에는 추가 열 `realName`합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="173ec-252">LogStash에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="173ec-252">Import from LogStash</span></span>

<span data-ttu-id="173ec-253">사용 하는 경우 [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), 분석 tooquery 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="173ec-254">사용 하 여 hello [데이터 분석에 파이프 하는 플러그 인](https://github.com/Microsoft/logstash-output-application-insights)합니다.</span><span class="sxs-lookup"><span data-stu-id="173ec-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="173ec-255">비디오</span><span class="sxs-lookup"><span data-stu-id="173ec-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

