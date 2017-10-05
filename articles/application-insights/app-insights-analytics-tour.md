---
title: "Azure Application Insights 내 Analytics 둘러보기 | Microsoft Docs"
description: "Application Insights의 강력한 검색 도구인 Analytics의 모든 주요 쿼리에 대한 간단한 샘플"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="77efa-103">Application Insights의 Analytics 둘러보기</span><span class="sxs-lookup"><span data-stu-id="77efa-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="77efa-104">[분석](app-insights-analytics.md)은 [Application Insights](app-insights-overview.md)의 강력한 검색 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="77efa-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="77efa-106">**[소개 비디오 보기](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**</span><span class="sxs-lookup"><span data-stu-id="77efa-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="77efa-107">앱이 아직 데이터를 Application Insights로 전송하지 않은 경우, **[시뮬레이션된 데이터에 대한 분석을 테스트](https://analytics.applicationinsights.io/demo)**합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="77efa-108">**[SQL 사용자 치트 시트](https://aka.ms/sql-analytics)**에서는 가장 일반적인 코드를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="77efa-109">시작하기 위해 몇 가지 기본적인 쿼리를 연습해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="77efa-110">Application Insights 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="77efa-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="77efa-111">Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="77efa-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n개의 행 표시</span><span class="sxs-lookup"><span data-stu-id="77efa-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="77efa-114">사용자 작업(일반적으로 웹앱에서 받는 HTTP 요청)을 기록하는 데이터 요소는 `requests`라는 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="77efa-115">각 행은 앱의 Application Insights SDK에서 수신된 원격 분석 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="77efa-116">테이블의 몇 가지 샘플 행을 검사하는 것으로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-116">Let's start by examining a few sample rows of the table:</span></span>

![결과](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="77efa-118">이동을 클릭하기 전에 커서를 문의 어딘가에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="77efa-119">문을 둘 이상의 행으로 분할할 수 있지만 문에 빈 줄을 넣으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="77efa-120">빈 줄은 창에서 여러 개의 별도 쿼리를 유지하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="77efa-121">열을 선택하고 끌어서 놓고 열로 그룹화하고 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-121">Choose columns, drag them, group by columns, and filter:</span></span>

![결과의 오른쪽 위에 있는 열 선택을 클릭](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="77efa-123">세부 정보를 보려면 모든 항목을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-123">Expand any item to see the detail:</span></span>

![테이블을 선택하고 열을 구성](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="77efa-125">웹 브라우저에서 사용할 수 있는 결과의 순서를 변경하려면 열 머리글을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="77efa-126">단, 큰 결과 집합의 경우에는 브라우저에 다운로드되는 행의 수가 제한된다는 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="77efa-127">이 방식으로 정렬한다고 해서 항상 최상위 항목이나 최하위 항목이 표시되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="77efa-128">항목을 안정적으로 정렬하려면 `top` 또는 `sort` 연산자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="77efa-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 및 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="77efa-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="77efa-130">`take` 은(는) 빨리 확인할 결과 샘플을 가져오는 데 유용하지만 테이블의 행을 특정 순서 없이 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="77efa-131">순서가 지정된 보기를 가져오려면 `top`(샘플의 경우) 또는 `sort`(전체 테이블에 대해)을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="77efa-132">특정 열을 기준으로 순서가 정해진 처음 n 행 표시:</span><span class="sxs-lookup"><span data-stu-id="77efa-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="77efa-133">*구문:* 대부분의 연산자에는 `by`와(과) 같은 키워드 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="77efa-134">`desc`은(는) 내림차순을 의미하고 `asc`은(는) 오름차순을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="77efa-135">`top...`을(를) 사용하면 `sort ... | take...`을(를) 보다 효율적으로 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="77efa-136">다음과 같이 작성했을 수도 있음:</span><span class="sxs-lookup"><span data-stu-id="77efa-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="77efa-137">결과는 같지만 조금 더 느리게 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="77efa-138">`sort`의 별칭인 `order`을(를) 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="77efa-139">테이블 보기의 열 머리글을 사용하여 화면에서 결과를 정렬할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="77efa-140">하지만 물론 `take` 또는 `top`을(를) 사용하여 테이블의 일부만 검색했다면 검색한 레코드의 순서만 변경될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="77efa-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): 조건에 대한 필터링</span><span class="sxs-lookup"><span data-stu-id="77efa-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="77efa-142">특정 결과 코드를 반환하는 요청만 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="77efa-143">`where` 연산자는 부울 식을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="77efa-144">여기서 이에 관한 몇 가지 중요한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-144">Here are some key points about them:</span></span>

* <span data-ttu-id="77efa-145">`and`, `or`: 부울 연산자</span><span class="sxs-lookup"><span data-stu-id="77efa-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="77efa-146">`==`, `<>`, `!=`: 같음 및 같지 않음</span><span class="sxs-lookup"><span data-stu-id="77efa-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="77efa-147">`=~`, `!~`: 대/소문자 구분 없는 문자열 같음 및 같지 않음</span><span class="sxs-lookup"><span data-stu-id="77efa-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="77efa-148">더 많은 문자열 비교 연산자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="77efa-149">올바른 형식 가져오기</span><span class="sxs-lookup"><span data-stu-id="77efa-149">Getting the right type</span></span>
<span data-ttu-id="77efa-150">성공하지 못한 요청 찾기</span><span class="sxs-lookup"><span data-stu-id="77efa-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="77efa-151">Time</span><span class="sxs-lookup"><span data-stu-id="77efa-151">Time</span></span>

<span data-ttu-id="77efa-152">기본적으로 쿼리는 마지막 24시간으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="77efa-153">그러나 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="77efa-154">where 절에서 `timestamp`를 언급하는 쿼리를 작성하여 시간 범위를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="77efa-155">예:</span><span class="sxs-lookup"><span data-stu-id="77efa-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="77efa-156">시간 범위 기능은 원본 테이블 중 하나를 언급할 때마다 그 다음에 나오는 'where' 절에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="77efa-157">`ago(3d)`는 '3일 전'을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="77efa-158">기타 시간 단위에는 시간(`2h`, `2.5h`), 분(`25m`) 및 초(`10s`)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="77efa-159">기타 예제:</span><span class="sxs-lookup"><span data-stu-id="77efa-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="77efa-160">[날짜 및 시간 참조](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)</span><span class="sxs-lookup"><span data-stu-id="77efa-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="77efa-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): 열 선택, 이름 바꾸기 및 계산</span><span class="sxs-lookup"><span data-stu-id="77efa-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="77efa-162">원하는 열만 선택하려면 [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="77efa-163">열 이름을 바꾸고 새 열을 정의할 수도 있음:</span><span class="sxs-lookup"><span data-stu-id="77efa-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="77efa-165">열 이름은 `['...']` 또는 `["..."]`와 같이 대괄호로 묶은 경우 공백이나 기호를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="77efa-166">`%` 은(는) 일반적인 모듈로 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="77efa-167">`1d` (한 자릿수, 'd' 한 개)은(는) 하루를 의미하는 시간 간격 리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="77efa-168">기타 시간 간격 리터럴에는 `12h`, `30m`, `10s`, `0.01s` 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="77efa-169">`floor`(별칭 `bin`)은(는) 값을 사용자가 입력하는 기준 값에 가장 가까운 낮은 배수로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="77efa-170">따라서 `floor(aTime, 1s)` 은(는) 시간을 가장 가까운 초로 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="77efa-171">식은 일반적인 연산자(`+`,`-`, ...)를 모두 포함할 수 있으며, 유용한 함수가 다양하게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="77efa-172">Extend</span><span class="sxs-lookup"><span data-stu-id="77efa-172">Extend</span></span>
<span data-ttu-id="77efa-173">기존 열에 열을 추가하기만 하려면 [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html)을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="77efa-174">기존 열을 모두 유지하려는 경우 [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html)을(를) 사용하면 [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)에 비해 표시되는 정보가 상세하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="77efa-175">현지 시간으로 변환</span><span class="sxs-lookup"><span data-stu-id="77efa-175">Convert to local time</span></span>

<span data-ttu-id="77efa-176">타임스탬프는 항상 UTC 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="77efa-177">따라서 미국 태평양 연안에 있으며 계절이 겨울이면 다음과 같이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="77efa-178">[요약](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): 행 그룹 집계</span><span class="sxs-lookup"><span data-stu-id="77efa-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="77efa-179">`Summarize` 은(는) 행 그룹에서 지정된 *집계 함수* 를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="77efa-180">예를 들어 웹앱이 요청에 응답하는 데 걸리는 시간은 `duration`필드에 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="77efa-181">모든 요청에 대한 평균 응답 시간을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="77efa-182">또는 결과를 다양한 이름의 요청으로 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="77efa-183">`Summarize`은(는) 스트림의 데이터 요소를 `by` 절에서 동일하게 평가하는 그룹으로 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="77efa-184">`by` 식의 각 값(예: 위 예제의 경우 각 작업 이름)은 결과 테이블의 행이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="77efa-185">또는 하루 중 시간으로 결과를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="77efa-186">`bin` 함수(즉, `floor`)를 사용하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="77efa-187">`by timestamp`을(를) 사용하면 모든 입력 행이 고유한 작은 그룹이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="77efa-188">시간 또는 숫자와 같은 임의 연속 스칼라의 경우 연속되는 범위를 관리할 수 있는 불연속 값의 수로 나누어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="77efa-189">익숙한 자리 내림 `floor` 함수인 `bin`은 이 작업을 수행하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="77efa-190">동일한 기술을 사용하여 문자열의 범위를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="77efa-191">`name=`을(를) 사용하여 집계 식 또는 by 절에서 결과 열의 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="77efa-192">샘플링된 데이터 수 계산</span><span class="sxs-lookup"><span data-stu-id="77efa-192">Counting sampled data</span></span>
<span data-ttu-id="77efa-193">`sum(itemCount)` 이벤트 수에 대한 권장 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="77efa-194">대부분의 경우 itemCount=1이므로 함수는 단순히 그룹의 행 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="77efa-195">하지만 [샘플링](app-insights-sampling.md)이 작동 중인 경우에는 Application Insights에서 원래 이벤트의 일부만 데이터 요소로 유지되므로 각 데이터 요소에 `itemCount`개의 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="77efa-196">예를 들어 샘플링에서 원래 이벤트의 75%를 삭제하는 경우 유지되는 레코드에서 itemCount==4가 됩니다. 즉, 유지된 모든 레코드마다 4개의 원본 레코드가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="77efa-197">적응 샘플링을 사용하면 응용 프로그램이 과도하게 사용되는 기간 동안 itemCount가 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="77efa-198">따라서 itemCount를 합하면 원래 이벤트 수에 대한 적절한 추정치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="77efa-199">그룹의 행 수를 계산하려는 경우 `count()` 집계(및 개수 계산 작업)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="77efa-200">[집계 함수](https://docs.loganalytics.io/learn/tutorials/aggregations.html)의 범위가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="77efa-201">결과 차트로 작성</span><span class="sxs-lookup"><span data-stu-id="77efa-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="77efa-202">기본적으로 결과는 테이블로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="77efa-203">테이블 보기보다 더 효과적인 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-203">We can do better than the table view.</span></span> <span data-ttu-id="77efa-204">세로 막대 옵션을 사용하여 차트 보기에서 결과를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![차트를 클릭한 다음 세로 막대 차트를 선택하고 x 및 y축을 할당](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="77efa-206">참고로 결과를 시간에 의해 정렬하지 않았지만(테이블 표시에서 확인 가능) 차트 표시는 언제나 날짜 및 시간을 정확한 순서로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="77efa-207">시간 차트</span><span class="sxs-lookup"><span data-stu-id="77efa-207">Timecharts</span></span>
<span data-ttu-id="77efa-208">각 시간에 발생한 이벤트 수 표시:</span><span class="sxs-lookup"><span data-stu-id="77efa-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="77efa-209">차트 표시 옵션 선택:</span><span class="sxs-lookup"><span data-stu-id="77efa-209">Select the Chart display option:</span></span>

![시간 차트](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="77efa-211">여러 계열</span><span class="sxs-lookup"><span data-stu-id="77efa-211">Multiple series</span></span>
<span data-ttu-id="77efa-212">`summarize` 절의 여러 식은 여러 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="77efa-213">`by` 절의 여러 식은 값의 각 조합에 대해 하나씩 여러 행을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![시간 및 위치별 요청 테이블](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="77efa-215">차원으로 차트를 분할</span><span class="sxs-lookup"><span data-stu-id="77efa-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="77efa-216">문자열 열과 숫자 열이 있는 테이블을 차트화할 경우 숫자 데이터를 별도 계열 요소로 분할하는 데 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="77efa-217">둘 이상의 문자열 열이 있는 경우 판별자로 사용할 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![분석 차트 분할](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="77efa-219">반송률</span><span class="sxs-lookup"><span data-stu-id="77efa-219">Bounce rate</span></span>

<span data-ttu-id="77efa-220">부울을 문자열로 변환하여 판별자로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-220">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="77efa-221">여러 메트릭 표시</span><span class="sxs-lookup"><span data-stu-id="77efa-221">Display multiple metrics</span></span>
<span data-ttu-id="77efa-222">둘 이상의 숫자 열이 있는 테이블을 차트화할 경우 타임스탬프 외에도 모든 조합을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![분석 차트 분할](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="77efa-224">**분할하지 않음**을 선택해야 여러 숫자 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="77efa-225">둘 이상의 숫자 열을 표시하면서 동시에 문자열 열로 분할할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="77efa-226">일일 평균 주기</span><span class="sxs-lookup"><span data-stu-id="77efa-226">Daily average cycle</span></span>
<span data-ttu-id="77efa-227">사용량은 평균 일에 대해 얼마나 변화합니까?</span><span class="sxs-lookup"><span data-stu-id="77efa-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="77efa-228">시간으로 범주화된 시간 모듈로 하루 기준 계산 요청:</span><span class="sxs-lookup"><span data-stu-id="77efa-228">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![평균 일의 시간에 대한 꺾은선형 차트](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="77efa-230">참고로 현재 우리는 꺾은선형 차트에 표시하기 위해 기간을 날짜 및 시간으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="77efa-231">여러 개의 일일 계열 비교</span><span class="sxs-lookup"><span data-stu-id="77efa-231">Compare multiple daily series</span></span>
<span data-ttu-id="77efa-232">서로 다른 국가에서 시각에 따라 사용량은 어떻게 변화합니까?</span><span class="sxs-lookup"><span data-stu-id="77efa-232">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![client_CountryOrRegion별로 분할](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="77efa-234">분포 출력</span><span class="sxs-lookup"><span data-stu-id="77efa-234">Plot a distribution</span></span>
<span data-ttu-id="77efa-235">서로 다른 길이의 세션이 몇 개 있습니까?</span><span class="sxs-lookup"><span data-stu-id="77efa-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="77efa-236">마지막 줄은 날짜/시간으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="77efa-237">현재 차트의 x축은 날짜/시간인 경우에만 스칼라로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="77efa-238">`where` 절은 단발 세션(sessionDuration==0)을 제외하고 x축의 길이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="77efa-239">백분위수</span><span class="sxs-lookup"><span data-stu-id="77efa-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="77efa-240">서로 다른 세션 백분위수를 다루는 기간 범위는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="77efa-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="77efa-241">위의 쿼리를 사용하되 마지막 줄을 다음으로 바꿈:</span><span class="sxs-lookup"><span data-stu-id="77efa-241">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="77efa-242">또한 둘 이상의 요청을 포함하고 있는 모든 세션을 비롯하여 정확한 그림을 가져오기 위해 where 절에서 상한을 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="77efa-244">확인할 수 있는 사항:</span><span class="sxs-lookup"><span data-stu-id="77efa-244">From which we can see that:</span></span>

* <span data-ttu-id="77efa-245">세션의 5%가 3분 34초 미만의 기간을 가지고 있음;</span><span class="sxs-lookup"><span data-stu-id="77efa-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="77efa-246">세션의 50%가 36분 미만 동안 지속</span><span class="sxs-lookup"><span data-stu-id="77efa-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="77efa-247">세션의 5%가 7일보다 오래 지속</span><span class="sxs-lookup"><span data-stu-id="77efa-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="77efa-248">각 국가에 대해 별도의 분석을 가져오기 위해 summarize 연산자 둘 다를 통해 client_CountryOrRegion 열을 따로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="77efa-249">Join</span><span class="sxs-lookup"><span data-stu-id="77efa-249">Join</span></span>
<span data-ttu-id="77efa-250">요청 및 예외를 비롯한 일부 테이블에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="77efa-251">실패 응답을 반환하는 요청과 관련된 예외를 찾으려면 `session_Id`에 대해 테이블을 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="77efa-252">조인을 수행하기 전에 `project`을(를) 사용하여 필요한 열만 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="77efa-253">동일한 절에서 타임스탬프 열의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="77efa-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): 변수에 결과 할당</span><span class="sxs-lookup"><span data-stu-id="77efa-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="77efa-255">`let`을 사용하여 이전 식의 일부를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="77efa-256">결과는 변하지 않음:</span><span class="sxs-lookup"><span data-stu-id="77efa-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="77efa-257">Analytics 클라이언트에서 쿼리 부분 사이에 공백 줄을 넣지 마세요.</span><span class="sxs-lookup"><span data-stu-id="77efa-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="77efa-258">이 부분을 모두 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="77efa-259">`toscalar`를 사용하여 단일 표 셀을 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-259">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="77efa-260">함수</span><span class="sxs-lookup"><span data-stu-id="77efa-260">Functions</span></span>

<span data-ttu-id="77efa-261">*Let*을 사용하여 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="77efa-262">중첩된 개체에 액세스</span><span class="sxs-lookup"><span data-stu-id="77efa-262">Accessing nested objects</span></span>
<span data-ttu-id="77efa-263">중첩된 개체에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="77efa-264">예를 들어 예외 스트림에서 다음과 같이 구조화된 개체가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="77efa-266">관심이 있는 속성을 선택하여 평면화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="77efa-267">결과를 적절한 형식으로 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="77efa-268">사용자 지정 속성 및 측정</span><span class="sxs-lookup"><span data-stu-id="77efa-268">Custom properties and measurements</span></span>
<span data-ttu-id="77efa-269">응용 프로그램이 이벤트에 대한 [사용자 지정 차원(속성) 및 사용자 지정 측정](app-insights-api-custom-events-metrics.md#properties)에 연결되면 `customDimensions` 및 `customMeasurements` 개체에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="77efa-270">예를 들어 앱이 다음을 포함한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="77efa-271">분석에서 이러한 값을 추출하려면:</span><span class="sxs-lookup"><span data-stu-id="77efa-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="77efa-272">사용자 지정 차원이 특정 형식인지 여부를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="77efa-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="77efa-273">대시보드</span><span class="sxs-lookup"><span data-stu-id="77efa-273">Dashboards</span></span>
<span data-ttu-id="77efa-274">가장 중요한 모든 차트와 테이블을 결합하기 위해 결과를 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="77efa-275">[Azure 공유 대시보드](app-insights-dashboards.md#share-dashboards): 고정 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="77efa-276">이렇게 하려면 공유 대시보드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="77efa-277">Azure Portal에서 대시보드를 열거나 만들고 공유를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="77efa-278">[Power BI 대시보드](app-insights-export-power-bi.md): 내보내기, Power BI 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="77efa-279">이 대체의 장점은 광범위한 원본의 다른 결과와 함께 쿼리를 표시할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="77efa-280">가져온 데이터와 결합</span><span class="sxs-lookup"><span data-stu-id="77efa-280">Combine with imported data</span></span>

<span data-ttu-id="77efa-281">분석 보고서는 대시보드에서 보기 좋게 표시되지만 좀 더 이해하기 쉬운 형태로 데이터를 변환하고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="77efa-282">예를 들어 인증된 사용자는 원격 분석에서 별칭으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="77efa-283">결과에 실제 이름을 표시하고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="77efa-284">이렇게 하려면 별칭을 실제 이름에 매핑하는 CSV 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="77efa-285">데이터 파일을 가져오고 표준 테이블(요청, 예외 등)처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="77efa-286">자체적으로 쿼리하거나 다른 테이블과 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="77efa-287">예를 들어 usermap이라는 테이블이 있고 `realName` 및 `userId` 열이 있으면 요청 원격 분석에서 `user_AuthenticatedId` 필드를 변환하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="77efa-288">테이블을 가져오려면 스키마 블레이드의 **기타 데이터 원본** 아래에서 지침에 따라 데이터 샘플을 업로드하여 새 데이터 원본을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="77efa-289">그런 다음 이 정의를 사용하여 테이블을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="77efa-290">가져오기 기능은 현재 미리 보기 상태이므로 처음에 "기타 데이터 원본" 아래 "문의처" 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="77efa-291">이 링크를 사용하여 미리 보기 프로그램에 등록하고 나면 링크가 "새 데이터 원본 추가" 단추로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="77efa-292">테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-292">Tables</span></span>
<span data-ttu-id="77efa-293">앱에서 수신하는 원격 분석의 스트림이 여러 테이블을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="77efa-294">각 테이블에 대해 사용할 수 있는 속성의 스키마는 창의 왼쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="77efa-295">요청 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-295">Requests table</span></span>
<span data-ttu-id="77efa-296">웹 앱 및 페이지 이름별 세그먼트에 대 한 HTTP 요청 수 계산:</span><span class="sxs-lookup"><span data-stu-id="77efa-296">Count HTTP requests to your web app and segment by page name:</span></span>

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="77efa-298">가장 많이 실패하는 요청 찾기:</span><span class="sxs-lookup"><span data-stu-id="77efa-298">Find the requests that fail most:</span></span>

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="77efa-300">사용자 지정 이벤트 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-300">Custom events table</span></span>
<span data-ttu-id="77efa-301">사용자 고유의 이벤트를 보내기 위해 [Trackevent()](app-insights-api-custom-events-metrics.md#trackevent)를 사용하면 이 테이블에서 이벤트를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="77efa-302">응용 프로그램 코드에 이러한 줄을 포함하는 사례:</span><span class="sxs-lookup"><span data-stu-id="77efa-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="77efa-303">이러한 이벤트의 빈도 표시:</span><span class="sxs-lookup"><span data-stu-id="77efa-303">Display the frequency of these events:</span></span>

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="77efa-305">측정값 및 차원을 이벤트에서 추출:</span><span class="sxs-lookup"><span data-stu-id="77efa-305">Extract measurements and dimensions from the events:</span></span>

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="77efa-307">사용자 지정 메트릭 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-307">Custom metrics table</span></span>
<span data-ttu-id="77efa-308">사용자 지정 메트릭 값을 보내기 위해 [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric)을 사용하면 **customMetrics** 스트림에 결과가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="77efa-309">예:</span><span class="sxs-lookup"><span data-stu-id="77efa-309">For example:</span></span>  

![Application Insights 분석의 사용자 지정 메트릭](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="77efa-311">[메트릭 탐색기](app-insights-metrics-explorer.md)에서 원격 분석의 모든 형식에 연결된 모든 사용자 지정 측정값은 `TrackMetric()`을(를) 사용하여 전송되는 메트릭과 함께 메트릭 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="77efa-312">하지만 분석에서 사용자 지정 측정은 이벤트, 요청 등 수행된 형식의 원격 분석에 연결되고 TrackMetric에 의해 전송된 메트릭은 해당 스트림에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="77efa-313">성능 카운터 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-313">Performance counters table</span></span>
<span data-ttu-id="77efa-314">[성능 카운터](app-insights-performance-counters.md)는 CPU, 메모리, 네트워크 사용률 등 앱에 대한 기본 시스템 메트릭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="77efa-315">사용자 지정 카운터를 포함하여 추가 카운터를 보내도록 SDK를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="77efa-316">**performanceCounters** 스키마는 `category`, `counter` 이름 및 각 성능 카운터의 `instance` 이름을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="77efa-317">카운터 인스턴스 이름은 일부 성능 카운터에만 적용할 수 있으며 일반적으로 개수와 관련된 프로세스의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="77efa-318">각 응용 프로그램에 대한 원격 분석 데이터에는 해당 응용 프로그램에 대한 카운터에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="77efa-319">예를 들면 어떤 카운터를 사용할 수 있는지 알아보기:</span><span class="sxs-lookup"><span data-stu-id="77efa-319">For example, to see what counters are available:</span></span>

![Application Insights 분석의 성능 카운터](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="77efa-321">선택한 기간 동안 사용 가능한 메모리의 차트를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="77efa-321">To get a chart of available memory over the selected period:</span></span>

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="77efa-323">다른 원격 분석과 마찬가지로, **performanceCounters**에도 앱이 실행되는 호스트 컴퓨터의 id를 나타내는 열 `cloud_RoleInstance`이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="77efa-324">예를 들어, 서로 다른 컴퓨터에서 앱의 성능을 비교하려면:</span><span class="sxs-lookup"><span data-stu-id="77efa-324">For example, to compare the performance of your app on the different machines:</span></span>

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="77efa-326">예외 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-326">Exceptions table</span></span>
<span data-ttu-id="77efa-327">[앱에서 보고된 예외](app-insights-asp-net-exceptions.md)는 이 테이블에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="77efa-328">예외가 발생하는 경우 앱이 처리하는 HTTP 요청을 찾으려면 operation_Id에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Operation_Id에 요청을 사용하여 예외를 조인](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="77efa-330">브라우저 타이밍 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-330">Browser timings table</span></span>
<span data-ttu-id="77efa-331">`browserTimings`은 사용자의 브라우저에서 수집된 페이지 로드 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="77efa-332">이러한 메트릭을 보려면 [클라이언트쪽 원격 분석을 위해 앱을 설정](app-insights-javascript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="77efa-333">스키마에 [페이지 로드 프로세스의 여러 단계의 길이를 나타내는 메트릭](app-insights-javascript.md#page-load-performance)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="77efa-334">(사용자가 한 페이지를 읽는 시간의 길이 나타내지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="77efa-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="77efa-335">서로 다른 페이지의 popularities 표시하고 각 페이지에 대한 시간을 로드:</span><span class="sxs-lookup"><span data-stu-id="77efa-335">Show the popularities of different pages, and load times for each page:</span></span>

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="77efa-337">가용성 결과 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-337">Availability results table</span></span>
<span data-ttu-id="77efa-338">`availabilityResults`은 [웹 테스트](app-insights-monitor-web-app-availability.md) 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="77efa-339">각 테스트 위치에서 테스트가 실행될 때마다 개별적으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-339">Each run of your tests from each test location is reported separately.</span></span>

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="77efa-341">종속성 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-341">Dependencies table</span></span>
<span data-ttu-id="77efa-342">앱이 데이터베이스 및 REST Api에 대해 수행한 호출과 TrackDependency()에 대한 다른 호출의 결과가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="77efa-343">또한 브라우저에서 생성된 AJAX 호출을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="77efa-344">브라우저의 AJAX 호출:</span><span class="sxs-lookup"><span data-stu-id="77efa-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="77efa-345">서버의 종속성 호출:</span><span class="sxs-lookup"><span data-stu-id="77efa-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="77efa-346">Application Insights 에이전트가 설치되지 않은 경우 서버 쪽 종속성 결과에는 항상 `success==False`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="77efa-347">그러나 다른 데이터는 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="77efa-348">추적 테이블</span><span class="sxs-lookup"><span data-stu-id="77efa-348">Traces table</span></span>
<span data-ttu-id="77efa-349">Tracktrace()를 사용하여 앱에서 보낸 원격 분석 데이터나 [다른 로깅 프레임워크](app-insights-asp-net-trace-logs.md)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="77efa-350">비디오</span><span class="sxs-lookup"><span data-stu-id="77efa-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="77efa-351">고급 쿼리:</span><span class="sxs-lookup"><span data-stu-id="77efa-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="77efa-352">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77efa-352">Next steps</span></span>
* [<span data-ttu-id="77efa-353">분석 언어 참조</span><span class="sxs-lookup"><span data-stu-id="77efa-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="77efa-354">[SQL 사용자 치트 시트](https://aka.ms/sql-analytics)에서는 가장 일반적인 코드를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="77efa-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
