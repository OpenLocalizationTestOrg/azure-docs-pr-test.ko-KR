---
title: "aaaAnalytics-Azure Application Insights의 hello 강력한 검색 도구 | Microsoft Docs"
description: "분석, Application Insights의 hello 강력한 진단 검색 도구 간략하게 설명 합니다. "
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
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="04c97-103">Application Insights의 분석</span><span class="sxs-lookup"><span data-stu-id="04c97-103">Analytics in Application Insights</span></span>
<span data-ttu-id="04c97-104">[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="04c97-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="04c97-106">**[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="04c97-107">**[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="04c97-108">**[SQL-사용자의 치트 시트](https://aka.ms/sql-analytics)**  hello 가장 일반적인 구문으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="04c97-109">**[언어 참조](app-insights-analytics-reference.md)**  모든 toouse hello 로그 분석 쿼리 언어의 강력한 기능을 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="04c97-110">분석의 쿼리</span><span class="sxs-lookup"><span data-stu-id="04c97-110">Queries in Analytics</span></span>
<span data-ttu-id="04c97-111">일반적인 쿼리는 *원본* 테이블이며 그 뒤에 `|`로 구분된 일련의 *연산자*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="04c97-112">예를 들어 살펴보겠습니다 Hyderabad의 hello 시민 하루 중 시간과 웹 앱을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="04c97-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="04c97-113">및 we're 발생 하는 동안의 tootheir HTTP 요청을 반환 하는 어떤 결과 코드 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="04c97-114">그룹화 시간별 hello hello hello를 통해 지난 7 일 고유 클라이언트 IP 주소를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="04c97-115">hello 이전 24 시간 동안, 외부 tooget 결과 'timestamp'를 명시적으로 쿼리에 포함 하거나 hello 시간 범위 드롭다운 메뉴를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="04c97-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="04c97-116">차트 프레젠테이션, toostack hello 결과 서로 다른 응답 코드에서 선택 막대 hello로 hello 결과 표시 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![막대형 차트, X축 및 Y축 그리고 구분을 차례로 선택합니다.](./media/app-insights-analytics/020.png)

<span data-ttu-id="04c97-118">이 앱은 하이데라바드에서 점심 시간 및 취침 시간에 가장 인기 있는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="04c97-119">(또한 이러한 500개 코드를 조사해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="04c97-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="04c97-120">또한 강력한 통계 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-120">There are also powerful statistical operations:</span></span>

![통계 쿼리의 결과](./media/app-insights-analytics/025.png)

<span data-ttu-id="04c97-122">hello 언어는 많은 매력적인 기능:</span><span class="sxs-lookup"><span data-stu-id="04c97-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="04c97-123">[필터링](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="04c97-124">[조인](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) - 요청을 페이지 뷰, 종속성 호출, 예외 및 로그 추적과 상호 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="04c97-125">강력한 통계 [집계](https://docs.loganalytics.io/learn/tutorials/aggregations.html)기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="04c97-126">SQL 디버깅, 만큼 강력한 하지만 복잡 한 쿼리에 훨씬 더 쉽게: 중첩 문 대신 파이프 하면에서 하나의 기본 작업 toohello hello 데이터 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="04c97-127">즉각적이고 강력하게 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="04c97-128">[Pin tooAzure 대시보드 차트](app-insights-analytics-using.md#pin-to-dashboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="04c97-129">[내보내기 쿼리 tooPower BI](app-insights-analytics-using.md#export-to-power-bi)합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="04c97-130">한 [REST API](https://dev.applicationinsights.io/) 사용할 수 있는 toorun 쿼리 프로그래밍 방식으로, 예를 들어 Powershell에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="04c97-131">Tooyour Application Insights 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="04c97-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="04c97-132">Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="04c97-134">비디오</span><span class="sxs-lookup"><span data-stu-id="04c97-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="04c97-135">쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="04c97-135">Query examples</span></span>

<span data-ttu-id="04c97-136">이러한 연습 tooillustrate hello 전원을 분석을 사용 하 여 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="04c97-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="04c97-137">요청 기간의 급증 및 단계별 증가 자동 진단</span><span class="sxs-lookup"><span data-stu-id="04c97-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="04c97-138">시계열 분석으로 성능 저하 분석</span><span class="sxs-lookup"><span data-stu-id="04c97-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="04c97-139">autocluster 및 diffpatterns로 응용 프로그램 오류 분석</span><span class="sxs-lookup"><span data-stu-id="04c97-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="04c97-140">시계열 분석으로 고급 셰이프 검색</span><span class="sxs-lookup"><span data-stu-id="04c97-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="04c97-141">슬라이딩 창 작업 tooanalyze 응용 프로그램 사용 현황 (롤링 MAU/DAU 등)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="04c97-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="04c97-142">[디버그 로그 분석을 기준으로 서비스 중단 검색](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) 및 관련 블로그 게시물([여기](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics))</span><span class="sxs-lookup"><span data-stu-id="04c97-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="04c97-143">[간단한 디버그 로그를 사용하여 응용 프로그램 성능 프로파일링](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/))</span><span class="sxs-lookup"><span data-stu-id="04c97-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="04c97-144">[간단한 디버그 로그를 사용 하 여 코드 흐름의 각 단계에 대 한 hello 기간 측정](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) 와 일치 하는 블로그 게시물 [여기](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="04c97-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="04c97-145">[간단한 디버그 로그를 사용하여 동시성 분석](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/))</span><span class="sxs-lookup"><span data-stu-id="04c97-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="04c97-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04c97-146">Next steps</span></span>
* <span data-ttu-id="04c97-147">Hello로 시작 하는 것이 좋습니다 [언어 자습서](app-insights-analytics-tour.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="04c97-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="04c97-148">[분석 사용](app-insights-analytics-using.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="04c97-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="04c97-149">[언어 참조](app-insights-analytics-reference.md)</span><span class="sxs-lookup"><span data-stu-id="04c97-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
