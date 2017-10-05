---
title: "Analytics - Azure Application Insights의 강력한 검색 도구 | Microsoft Docs"
description: "Application Insights의 강력한 진단 검색 도구인 분석의 개요입니다. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="f4ab4-103">Application Insights의 분석</span><span class="sxs-lookup"><span data-stu-id="f4ab4-103">Analytics in Application Insights</span></span>
<span data-ttu-id="f4ab4-104">[분석](app-insights-analytics.md)은 [Application Insights](app-insights-overview.md)의 강력한 검색 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f4ab4-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="f4ab4-106">**[소개 비디오 보기](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**</span><span class="sxs-lookup"><span data-stu-id="f4ab4-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="f4ab4-107">앱이 아직 데이터를 Application Insights로 전송하지 않은 경우, **[시뮬레이션된 데이터에 대한 분석을 테스트](https://analytics.applicationinsights.io/demo)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="f4ab4-108">**[SQL 사용자 치트 시트](https://aka.ms/sql-analytics)**에서는 가장 일반적인 코드를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="f4ab4-109">**[언어 참조](app-insights-analytics-reference.md)** - Log Analytics 쿼리 언어의 모든 강력한 기능을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="f4ab4-110">분석의 쿼리</span><span class="sxs-lookup"><span data-stu-id="f4ab4-110">Queries in Analytics</span></span>
<span data-ttu-id="f4ab4-111">일반적인 쿼리는 *원본* 테이블이며 그 뒤에 `|`로 구분된 일련의 *연산자*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="f4ab4-112">예를 들어 하이데라바드의 시민들이 하루 중 언제 웹앱을 시도하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="f4ab4-113">그리고 그곳에 있는 동안 해당 HTTP 요청에 반환되는 결과 코드를 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="f4ab4-114">지난 7일 동안 하루 중 시간 단위로 그룹화하여 고유 클라이언트 IP 주소의 개수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4ab4-115">이전 24시간 외의 결과를 얻으려면 쿼리에 'timestamp'를 명시적으로 포함하거나 시간 범위 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="f4ab4-116">다른 응답 코드의 결과를 누적하도록 선택하여 막대형 차트 프레젠테이션으로 결과를 표시해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![막대형 차트, X축 및 Y축 그리고 구분을 차례로 선택합니다.](./media/app-insights-analytics/020.png)

<span data-ttu-id="f4ab4-118">이 앱은 하이데라바드에서 점심 시간 및 취침 시간에 가장 인기 있는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="f4ab4-119">(또한 이러한 500개 코드를 조사해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f4ab4-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="f4ab4-120">또한 강력한 통계 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-120">There are also powerful statistical operations:</span></span>

![통계 쿼리의 결과](./media/app-insights-analytics/025.png)

<span data-ttu-id="f4ab4-122">언어에 다음과 같은 많은 유용한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-122">The language has many attractive features:</span></span>


* <span data-ttu-id="f4ab4-123">[필터링](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="f4ab4-124">[조인](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) - 요청을 페이지 뷰, 종속성 호출, 예외 및 로그 추적과 상호 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="f4ab4-125">강력한 통계 [집계](https://docs.loganalytics.io/learn/tutorials/aggregations.html)기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="f4ab4-126">복잡한 쿼리에 대해 SQL만큼 강력하지만 훨씬 쉽게 중첩문 대신 하나의 기본 연산에서 다음 연산으로 데이터를 파이프합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="f4ab4-127">즉각적이고 강력하게 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="f4ab4-128">[Azure 대시보드에 차트를 고정](app-insights-analytics-using.md#pin-to-dashboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="f4ab4-129">[Power BI로 쿼리를 내보냅니다](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="f4ab4-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="f4ab4-130">예를 들어 Powershell에서 프로그래밍 방식으로 쿼리를 실행하는 데 사용할 수 있는 [REST API](https://dev.applicationinsights.io/)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="f4ab4-131">Application Insights 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="f4ab4-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="f4ab4-132">Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="f4ab4-134">비디오</span><span class="sxs-lookup"><span data-stu-id="f4ab4-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="f4ab4-135">쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="f4ab4-135">Query examples</span></span>

<span data-ttu-id="f4ab4-136">다음 연습을 수행하여 분석의 유용한 기능을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="f4ab4-137">요청 기간의 급증 및 단계별 증가 자동 진단</span><span class="sxs-lookup"><span data-stu-id="f4ab4-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="f4ab4-138">시계열 분석으로 성능 저하 분석</span><span class="sxs-lookup"><span data-stu-id="f4ab4-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="f4ab4-139">autocluster 및 diffpatterns로 응용 프로그램 오류 분석</span><span class="sxs-lookup"><span data-stu-id="f4ab4-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="f4ab4-140">시계열 분석으로 고급 셰이프 검색</span><span class="sxs-lookup"><span data-stu-id="f4ab4-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="f4ab4-141">슬라이딩 윈도우 작업을 사용하여 응용 프로그램 사용량 분석(롤링 MAU/DAU 등)</span><span class="sxs-lookup"><span data-stu-id="f4ab4-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="f4ab4-142">[디버그 로그 분석을 기준으로 서비스 중단 검색](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) 및 관련 블로그 게시물([여기](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics))</span><span class="sxs-lookup"><span data-stu-id="f4ab4-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="f4ab4-143">[간단한 디버그 로그를 사용하여 응용 프로그램 성능 프로파일링](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/))</span><span class="sxs-lookup"><span data-stu-id="f4ab4-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="f4ab4-144">[간단한 디버그 로그를 사용하여 코드 흐름에서 각 단계의 지속 시간 측정](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/))</span><span class="sxs-lookup"><span data-stu-id="f4ab4-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="f4ab4-145">[간단한 디버그 로그를 사용하여 동시성 분석](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/))</span><span class="sxs-lookup"><span data-stu-id="f4ab4-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="f4ab4-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4ab4-146">Next steps</span></span>
* <span data-ttu-id="f4ab4-147">[언어 둘러보기](app-insights-analytics-tour.md)를 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ab4-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="f4ab4-148">[분석 사용](app-insights-analytics-using.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="f4ab4-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="f4ab4-149">[언어 참조](app-insights-analytics-reference.md)</span><span class="sxs-lookup"><span data-stu-id="f4ab4-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
