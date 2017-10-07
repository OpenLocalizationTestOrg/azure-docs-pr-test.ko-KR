---
title: "Azure Application Insights에서 분석을 통해 aaaA 둘러보기 | Microsoft Docs"
description: "모든 쿼리의 hello 주 분석에서 Application Insights의 hello 강력한 검색 도구 간단한 샘플입니다."
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
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="89b5a-103">Application Insights의 Analytics 둘러보기</span><span class="sxs-lookup"><span data-stu-id="89b5a-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="89b5a-104">[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="89b5a-105">다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="89b5a-106">**[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="89b5a-107">**[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="89b5a-108">**[SQL-사용자의 치트 시트](https://aka.ms/sql-analytics)**  hello 가장 일반적인 구문으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="89b5a-109">몇 가지 기본적인 쿼리 tooget 시작한 단계별로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="89b5a-110">Tooyour Application Insights 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="89b5a-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="89b5a-111">Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="89b5a-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n개의 행 표시</span><span class="sxs-lookup"><span data-stu-id="89b5a-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="89b5a-114">사용자 작업(일반적으로 웹앱에서 받는 HTTP 요청)을 기록하는 데이터 요소는 `requests`라는 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="89b5a-115">각 행에는 응용 프로그램에 Application Insights SDK hello에서 받은 원격 분석 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="89b5a-116">Hello 테이블의 몇 가지 샘플 행을 검사 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-116">Let's start by examining a few sample rows of hello table:</span></span>

![결과](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="89b5a-118">Hello 커서 위치에 배치 hello 문의 이동을 클릭 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="89b5a-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="89b5a-119">문을 둘 이상의 행으로 분할할 수 있지만 문에 빈 줄을 넣으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="89b5a-120">빈 줄은 편리 tookeep 여러 hello 창에서 쿼리를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="89b5a-121">열을 선택하고 끌어서 놓고 열로 그룹화하고 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-121">Choose columns, drag them, group by columns, and filter:</span></span>

![결과의 오른쪽 위에 있는 열 선택을 클릭](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="89b5a-123">모든 항목 toosee hello 세부 정보를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-123">Expand any item toosee hello detail:</span></span>

![테이블을 선택하고 열을 구성](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="89b5a-125">열 순서 toore hello 결과 hello 웹 브라우저에서 사용할 수 있는의 hello 헤드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="89b5a-126">하지만 큰 결과 집합에 대 한 행 다운로드 한 toohello 브라우저의 hello 번호 제한 된다는 점에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="89b5a-127">이러한 방식으로 정렬 실제 최고 hello 또는 가장 낮은 항목을 항상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="89b5a-128">안전 하 게 사용 하 여 hello toosort 항목 `top` 또는 `sort` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="89b5a-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 및 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="89b5a-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="89b5a-130">`take`유용한 tooget 결과의 빠른 샘플 않으며 임의의 순서로 hello 테이블에서 행을 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="89b5a-131">tooget 순서가 지정 된 뷰를 사용 하 여 `top` (예) 또는 `sort` (hello 전체 테이블)를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="89b5a-132">Hello 처음 n 개의 행을 특정 열으로 정렬 표시:</span><span class="sxs-lookup"><span data-stu-id="89b5a-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="89b5a-133">*구문:* 대부분의 연산자에는 `by`와(과) 같은 키워드 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="89b5a-134">`desc`은(는) 내림차순을 의미하고 `asc`은(는) 오름차순을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="89b5a-135">`top...`을(를) 사용하면 `sort ... | take...`을(를) 보다 효율적으로 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="89b5a-136">다음과 같이 작성했을 수도 있음:</span><span class="sxs-lookup"><span data-stu-id="89b5a-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="89b5a-137">hello 라고 할 때 결과 hello 동일 하지만 약간 더 느리게 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="89b5a-138">`sort`의 별칭인 `order`을(를) 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="89b5a-139">hello 표 보기에서 열 머리글에 hello hello 결과 hello 화면에 사용 되는 toosort 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="89b5a-140">하지만 물론 사용한 적이 있다면 `take` 또는 `top` tooretrieve 테이블의 한 부분일 뿐, 순서를 변경할 hello 레코드만 검색 한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="89b5a-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): 조건에 대한 필터링</span><span class="sxs-lookup"><span data-stu-id="89b5a-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="89b5a-142">특정 결과 코드를 반환하는 요청만 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="89b5a-143">hello `where` 연산자는 부울 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="89b5a-144">여기서 이에 관한 몇 가지 중요한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-144">Here are some key points about them:</span></span>

* <span data-ttu-id="89b5a-145">`and`, `or`: 부울 연산자</span><span class="sxs-lookup"><span data-stu-id="89b5a-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="89b5a-146">`==`, `<>`, `!=`: 같음 및 같지 않음</span><span class="sxs-lookup"><span data-stu-id="89b5a-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="89b5a-147">`=~`, `!~`: 대/소문자 구분 없는 문자열 같음 및 같지 않음</span><span class="sxs-lookup"><span data-stu-id="89b5a-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="89b5a-148">더 많은 문자열 비교 연산자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="89b5a-149">Hello 오른쪽 유형이 나타났다</span><span class="sxs-lookup"><span data-stu-id="89b5a-149">Getting hello right type</span></span>
<span data-ttu-id="89b5a-150">성공하지 못한 요청 찾기</span><span class="sxs-lookup"><span data-stu-id="89b5a-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="89b5a-151">Time</span><span class="sxs-lookup"><span data-stu-id="89b5a-151">Time</span></span>

<span data-ttu-id="89b5a-152">기본적으로 쿼리 지난 24 시간 동안 제한 된 toohello을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="89b5a-153">그러나 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="89b5a-154">Hello 시간 범위를 언급 하는 쿼리를 작성 하 여 재정의 `timestamp` where 절에서.</span><span class="sxs-lookup"><span data-stu-id="89b5a-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="89b5a-155">예:</span><span class="sxs-lookup"><span data-stu-id="89b5a-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="89b5a-156">hello 시간 범위 기능은 해당 tooa hello 원본 테이블 중 하나에 대 한 각 언급이 다음 절을 삽입 하는 'where' 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="89b5a-157">`ago(3d)`는 '3일 전'을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="89b5a-158">기타 시간 단위에는 시간(`2h`, `2.5h`), 분(`25m`) 및 초(`10s`)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="89b5a-159">기타 예제:</span><span class="sxs-lookup"><span data-stu-id="89b5a-159">Other examples:</span></span>

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

<span data-ttu-id="89b5a-160">[날짜 및 시간 참조](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)</span><span class="sxs-lookup"><span data-stu-id="89b5a-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="89b5a-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): 열 선택, 이름 바꾸기 및 계산</span><span class="sxs-lookup"><span data-stu-id="89b5a-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="89b5a-162">사용 하 여 [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) hello 열만 원하는 아웃 toopick:</span><span class="sxs-lookup"><span data-stu-id="89b5a-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="89b5a-163">열 이름을 바꾸고 새 열을 정의할 수도 있음:</span><span class="sxs-lookup"><span data-stu-id="89b5a-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="89b5a-165">열 이름은 `['...']` 또는 `["..."]`와 같이 대괄호로 묶은 경우 공백이나 기호를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="89b5a-166">`%`모듈로 연산자는 일반적인는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="89b5a-167">`1d` (한 자릿수, 'd' 한 개)은(는) 하루를 의미하는 시간 간격 리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="89b5a-168">기타 시간 간격 리터럴에는 `12h`, `30m`, `10s`, `0.01s` 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="89b5a-169">`floor`(별칭 `bin`) 값 아래로 toohello hello 제공 하는 기준 값의 가장 가까운 배수로 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="89b5a-170">따라서 `floor(aTime, 1s)` 초 가장 가까운 toohello 다운 시간을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="89b5a-171">식은 모든 hello 일반적인 연산자를 포함할 수 있습니다 (`+`, `-`,...)를 다양 한 유용한 함수가 이며 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="89b5a-172">Extend</span><span class="sxs-lookup"><span data-stu-id="89b5a-172">Extend</span></span>
<span data-ttu-id="89b5a-173">사용 하 여 려는 스토리를 기존 tooadd 열 toohello 경우 [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="89b5a-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="89b5a-174">사용 하 여 [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) 보다 덜 자세 [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) 모든 기존 열을 hello tookeep 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="89b5a-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="89b5a-175">Toolocal 시간으로 변환</span><span class="sxs-lookup"><span data-stu-id="89b5a-175">Convert toolocal time</span></span>

<span data-ttu-id="89b5a-176">타임스탬프는 항상 UTC 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="89b5a-177">따라서 hello 미국 태평양 coast에 속하고 겨울 인 경우 사용자가 좋아할 만한이:</span><span class="sxs-lookup"><span data-stu-id="89b5a-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="89b5a-178">[요약](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): 행 그룹 집계</span><span class="sxs-lookup"><span data-stu-id="89b5a-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="89b5a-179">`Summarize` 은(는) 행 그룹에서 지정된 *집계 함수* 를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="89b5a-180">예를 들어 hello 웹 앱은 toorespond tooa 요청은 보고 된 시간 hello 필드에 `duration`합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="89b5a-181">살펴보겠습니다 hello 평균 응답 시간 tooall 요청:</span><span class="sxs-lookup"><span data-stu-id="89b5a-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="89b5a-182">또는 서로 다른 이름의 요청으로 hello 결과 분리 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="89b5a-183">`Summarize`수집은 hello에 대 한 그룹으로 hello 스트림의 데이터 요소 hello `by` 절이 동일 하 게 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="89b5a-184">द क र hello `by` 식을-hello 위 예제에서에서 각 작업 이름-hello 결과 테이블의 행에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="89b5a-185">또는 하루 중 시간으로 결과를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="89b5a-186">Hello 사용 하는지 어떻게 알 `bin` 함수 (즉, `floor`).</span><span class="sxs-lookup"><span data-stu-id="89b5a-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="89b5a-187">`by timestamp`을(를) 사용하면 모든 입력 행이 고유한 작은 그룹이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="89b5a-188">모든 연속 스칼라 숫자 like 시간이 나 서로 다른 관리 가능한 수의 불연속 값으로 toobreak hello 연속 범위에 있다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="89b5a-189">`bin`-방금 hello 친숙 한 반올림 다운은 `floor` 함수-hello 가장 쉬운 방법은 toodo은입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="89b5a-190">사용 하는 문자열의 동일한 기술을 tooreduce 범위 hello:</span><span class="sxs-lookup"><span data-stu-id="89b5a-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="89b5a-191">사용할 수 있는 알림 `name=` tooset hello 이름 hello 집계 식 또는 hello by-절에 결과 열입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="89b5a-192">샘플링된 데이터 수 계산</span><span class="sxs-lookup"><span data-stu-id="89b5a-192">Counting sampled data</span></span>
<span data-ttu-id="89b5a-193">`sum(itemCount)`hello 권장 집계 toocount 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="89b5a-194">대부분의 경우 itemCount 목록을 = = 1 이면 hello 함수를 단순히 hello hello 그룹의 행 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="89b5a-195">되지만 [샘플링](app-insights-sampling.md) 은 작업에서 hello 원래 이벤트의 일부만 변수로 유지 됩니다 Application Insights에서 데이터 요소 참조 하면 각 데이터 요소에 대 한 개가 되도록 `itemCount` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="89b5a-196">예를 들어 샘플링 hello 원래 이벤트가 다음 itemCount의 75%를 삭제 하는 경우 = = 4 hello 유지 레코드-즉, 보존 된 모든 레코드에 대해 있었습니다 4 개의 원래 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="89b5a-197">적응 샘플링 itemCount toobe 높은 경우 응용 프로그램 사용이 기간 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="89b5a-198">이벤트의 hello 원래 수의 적절 한 예측 데이터를 제공 따라서 itemCount를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="89b5a-199">또한 한 `count()` 집계 (및 count 연산)을 실제로 수행 하려는 경우 toocount hello 그룹의 행 수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="89b5a-200">[집계 함수](https://docs.loganalytics.io/learn/tutorials/aggregations.html)의 범위가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="89b5a-201">Hello 결과 차트</span><span class="sxs-lookup"><span data-stu-id="89b5a-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="89b5a-202">기본적으로 결과는 테이블로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="89b5a-203">Hello 표 보기 보다 더 잘 수행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-203">We can do better than hello table view.</span></span> <span data-ttu-id="89b5a-204">Hello 세로 막대 옵션으로 hello 차트 뷰에서 hello 결과에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![차트를 클릭한 다음 세로 막대 차트를 선택하고 x 및 y축을 할당](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="89b5a-206">되지만 (보시 hello 테이블 디스플레이에서) 시간별 hello 결과 정렬 하지 않은, hello 차트 표시에는 항상 올바른 순서로 datetime 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="89b5a-207">시간 차트</span><span class="sxs-lookup"><span data-stu-id="89b5a-207">Timecharts</span></span>
<span data-ttu-id="89b5a-208">각 시간에 발생한 이벤트 수 표시:</span><span class="sxs-lookup"><span data-stu-id="89b5a-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="89b5a-209">Hello 차트 표시 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-209">Select hello Chart display option:</span></span>

![시간 차트](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="89b5a-211">여러 계열</span><span class="sxs-lookup"><span data-stu-id="89b5a-211">Multiple series</span></span>
<span data-ttu-id="89b5a-212">Hello에서 여러 개의 식을 `summarize` 절 여러 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="89b5a-213">Hello에서 여러 개의 식을 `by` 절 값의 각 조합에 대해 하나씩 여러 개의 행을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![시간 및 위치별 요청 테이블](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="89b5a-215">차원으로 차트를 분할</span><span class="sxs-lookup"><span data-stu-id="89b5a-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="89b5a-216">문자열 열과 hello 문자열에 숫자 열이 있는 테이블 차트 수 있으면 사용된 toosplit hello 숫자 데이터를 별도 일련의 점입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="89b5a-217">여러 개의 문자열 열 이면 hello 판별자로 어떤 열 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![분석 차트 분할](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="89b5a-219">반송률</span><span class="sxs-lookup"><span data-stu-id="89b5a-219">Bounce rate</span></span>

<span data-ttu-id="89b5a-220">부울 tooa 문자열 toouse 변환 판별자로:</span><span class="sxs-lookup"><span data-stu-id="89b5a-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="89b5a-221">여러 메트릭 표시</span><span class="sxs-lookup"><span data-stu-id="89b5a-221">Display multiple metrics</span></span>
<span data-ttu-id="89b5a-222">또한 toohello 타임 스탬프에 둘 이상의 숫자 열이 있는 테이블, 차트 어떠한 조합의 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![분석 차트 분할](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="89b5a-224">**분할하지 않음**을 선택해야 여러 숫자 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="89b5a-225">분할할 수 없습니다 hello에서 문자열 열에 따라 같은 시간으로 여러 개의 숫자 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="89b5a-226">일일 평균 주기</span><span class="sxs-lookup"><span data-stu-id="89b5a-226">Daily average cycle</span></span>
<span data-ttu-id="89b5a-227">Hello 평균 하루를 통해 사용량 달라질?</span><span class="sxs-lookup"><span data-stu-id="89b5a-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="89b5a-228">개수 요청 1 일, 모듈로 hello 시간별 시간으로 범주화 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="89b5a-230">현재 있는지 tooconvert 시간 기간 toodatetimes 순서 toodisplay에서 꺾은선형 차트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="89b5a-231">여러 개의 일일 계열 비교</span><span class="sxs-lookup"><span data-stu-id="89b5a-231">Compare multiple daily series</span></span>
<span data-ttu-id="89b5a-232">어떻게는 사용 시간의 경과 따라 hello 하루 중 다른 국가에서?</span><span class="sxs-lookup"><span data-stu-id="89b5a-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="89b5a-234">분포 출력</span><span class="sxs-lookup"><span data-stu-id="89b5a-234">Plot a distribution</span></span>
<span data-ttu-id="89b5a-235">서로 다른 길이의 세션이 몇 개 있습니까?</span><span class="sxs-lookup"><span data-stu-id="89b5a-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="89b5a-236">hello 마지막 줄은 필요한 tooconvert toodatetime입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="89b5a-237">현재는 차트의 hello x 축 날짜/시간 경우에 스칼라도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="89b5a-238">hello `where` 절 제외 원 샷 세션 (sessionDuration = = 0) 및 집합 hello hello x 축의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="89b5a-239">백분위수</span><span class="sxs-lookup"><span data-stu-id="89b5a-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="89b5a-240">서로 다른 세션 백분위수를 다루는 기간 범위는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="89b5a-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="89b5a-241">쿼리를 위에 hello를 사용 하 여 하지만 hello 마지막 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="89b5a-242">또한 hello 상한값 hello 절 순서 tooget 수치 요청이 둘 이상 있는 모든 세션을 포함 하 여 해결 하는 위치에서 제거:</span><span class="sxs-lookup"><span data-stu-id="89b5a-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="89b5a-244">확인할 수 있는 사항:</span><span class="sxs-lookup"><span data-stu-id="89b5a-244">From which we can see that:</span></span>

* <span data-ttu-id="89b5a-245">세션의 5%가 3분 34초 미만의 기간을 가지고 있음;</span><span class="sxs-lookup"><span data-stu-id="89b5a-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="89b5a-246">세션의 50%가 36분 미만 동안 지속</span><span class="sxs-lookup"><span data-stu-id="89b5a-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="89b5a-247">세션의 5%가 7일보다 오래 지속</span><span class="sxs-lookup"><span data-stu-id="89b5a-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="89b5a-248">각 국가 대 한 별도 분석 tooget 연산자 요약 둘 다를 통해 개별적으로 toobring hello client_CountryOrRegion 열은:</span><span class="sxs-lookup"><span data-stu-id="89b5a-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="89b5a-249">Join</span><span class="sxs-lookup"><span data-stu-id="89b5a-249">Join</span></span>
<span data-ttu-id="89b5a-250">요청 및 예외를 비롯 하 여 액세스 tooseveral 테이블 했습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="89b5a-251">toofind hello 예외 관련된 tooa 요청 실패 응답을 반환 하는 hello 테이블에 참여할 수 있습니다 `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="89b5a-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="89b5a-252">것이 좋습니다 toouse `project` tooselect 정당한 hello 열을 수행 하기 전에 필요한 hello 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="89b5a-253">Hello에 동일한 절 hello 타임 스탬프 열의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="89b5a-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): 결과 tooa 변수 할당</span><span class="sxs-lookup"><span data-stu-id="89b5a-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="89b5a-255">사용 하 여 `let` tooseparate hello 이전 식의 hello 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="89b5a-256">hello 결과가 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="89b5a-257">Hello 분석 클라이언트에서 hello 쿼리의 hello 부분 사이 빈 줄을 넣지 마세요.</span><span class="sxs-lookup"><span data-stu-id="89b5a-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="89b5a-258">해당 내용을 모두 tooexecute 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="89b5a-259">사용 하 여 `toscalar` tooconvert 단일 테이블 셀 tooa 값:</span><span class="sxs-lookup"><span data-stu-id="89b5a-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="89b5a-260">함수</span><span class="sxs-lookup"><span data-stu-id="89b5a-260">Functions</span></span>

<span data-ttu-id="89b5a-261">사용 하 여 *Let* toodefine 함수:</span><span class="sxs-lookup"><span data-stu-id="89b5a-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="89b5a-262">중첩된 개체에 액세스</span><span class="sxs-lookup"><span data-stu-id="89b5a-262">Accessing nested objects</span></span>
<span data-ttu-id="89b5a-263">중첩된 개체에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="89b5a-264">예를 들어 hello 예외 스트림 다음과 같이 구조화 된 개체를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="89b5a-266">에 관심이 hello 속성을 선택 하 여 평면화를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="89b5a-267">Toocast hello 결과 toohello 적절 한 형식을 사용 해야 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="89b5a-268">사용자 지정 속성 및 측정</span><span class="sxs-lookup"><span data-stu-id="89b5a-268">Custom properties and measurements</span></span>
<span data-ttu-id="89b5a-269">응용 프로그램에 연결 되 면 [사용자 지정 차원 (속성) 및 사용자 지정 측정](app-insights-api-custom-events-metrics.md#properties) tooevents, 다음에 해당 오류가 표시 hello `customDimensions` 및 `customMeasurements` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="89b5a-270">예를 들어 앱이 다음을 포함한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="89b5a-271">tooextract 분석에서 이러한 값:</span><span class="sxs-lookup"><span data-stu-id="89b5a-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="89b5a-272">tooverify 특정 유형의 사용자 지정 차원 인지 여부.</span><span class="sxs-lookup"><span data-stu-id="89b5a-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="89b5a-273">대시보드</span><span class="sxs-lookup"><span data-stu-id="89b5a-273">Dashboards</span></span>
<span data-ttu-id="89b5a-274">모든 가장 중요 한 차트와 테이블 함께 순서 toobring에서 결과 tooa 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="89b5a-275">[Azure 공유 대시보드](app-insights-dashboards.md#share-dashboards): hello 고정 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="89b5a-276">이렇게 하려면 공유 대시보드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="89b5a-277">Hello Azure 포털에서에서 열기 또는 대시보드를 만들 하 고 공유를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="89b5a-278">[Power BI 대시보드](app-insights-export-power-bi.md): 내보내기, Power BI 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="89b5a-279">이 대체의 장점은 광범위한 원본의 다른 결과와 함께 쿼리를 표시할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="89b5a-280">가져온 데이터와 결합</span><span class="sxs-lookup"><span data-stu-id="89b5a-280">Combine with imported data</span></span>

<span data-ttu-id="89b5a-281">분석 보고서 hello 대시보드에서 멋진 보이지만 tootranslate hello 데이터 tooa를 원하는 경우에 따라 더 많은 양이 양식입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="89b5a-282">예를 들어, 인증 된 사용자가 별칭으로 hello 원격 분석에서 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="89b5a-283">결과에 자신의 실제 이름을 tooshow를 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="89b5a-284">toodo이 hello 별칭 toohello 실제 이름에서 매핑하는 CSV 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="89b5a-285">데이터 파일을 가져오고 (요청, 예외 및 등) hello 표준 테이블 처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="89b5a-286">자체적으로 쿼리하거나 다른 테이블과 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="89b5a-287">예를 들어 usermap, 라는 테이블이 있고에 열 `realName` 및 `userId`, tootranslate hello를 사용할 수 있습니다 `user_AuthenticatedId` hello 요청 원격 분석에서 필드:</span><span class="sxs-lookup"><span data-stu-id="89b5a-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="89b5a-288">tooimport hello 스키마 블레이드에서 테이블에서 **기타 데이터 소스**, hello 지침 tooadd 새 데이터 원본을 데이터의 샘플을 업로드 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="89b5a-289">그런 다음이 정의 tooupload 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="89b5a-290">hello 가져오기 기능은 현재 미리 보기에서 다른 데이터 원본"."에서 "사용자 의견" 링크 처음 되므로</span><span class="sxs-lookup"><span data-stu-id="89b5a-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="89b5a-291">이 toosign toohello 미리 보기 프로그램을 사용 하 고 hello 링크 "새 데이터 소스 추가" 단추는으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="89b5a-292">테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-292">Tables</span></span>
<span data-ttu-id="89b5a-293">응용 프로그램에서 수신 하는 원격 분석의 hello 스트림이 여러 테이블을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="89b5a-294">각 테이블에 대해 사용할 수 있는 속성의 hello 스키마 hello 창의 hello 왼쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="89b5a-295">요청 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-295">Requests table</span></span>
<span data-ttu-id="89b5a-296">Count HTTP 요청 tooyour web app 및 페이지 이름으로 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="89b5a-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="89b5a-298">가장에 실패 하는 hello 요청을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-298">Find hello requests that fail most:</span></span>

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="89b5a-300">사용자 지정 이벤트 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-300">Custom events table</span></span>
<span data-ttu-id="89b5a-301">사용 하는 경우 [의 trackevent ()](app-insights-api-custom-events-metrics.md#trackevent) toosend 사용자 고유의 이벤트를 읽을 수 있습니다이 테이블에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="89b5a-302">응용 프로그램 코드에 이러한 줄을 포함하는 사례:</span><span class="sxs-lookup"><span data-stu-id="89b5a-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="89b5a-303">이러한 이벤트의 hello 빈도 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-303">Display hello frequency of these events:</span></span>

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="89b5a-305">측정값 및 차원을 hello 이벤트에서 추출:</span><span class="sxs-lookup"><span data-stu-id="89b5a-305">Extract measurements and dimensions from hello events:</span></span>

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="89b5a-307">사용자 지정 메트릭 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-307">Custom metrics table</span></span>
<span data-ttu-id="89b5a-308">사용 중인 경우 [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) toosend 메트릭 값을 직접 hello에서 그 결과 확인할 수 있습니다 **customMetrics** 스트림 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="89b5a-309">예:</span><span class="sxs-lookup"><span data-stu-id="89b5a-309">For example:</span></span>  

![Application Insights 분석의 사용자 지정 메트릭](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="89b5a-311">[메트릭 탐색기](app-insights-metrics-explorer.md), 연결 된 tooany 유형의 원격 분석 메트릭 사용 하 여 보낸 함께 hello 메트릭 블레이드에 함께 표시 하는 모든 사용자 지정 측정 `TrackMetric()`합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="89b5a-312">분석에서 사용자 지정 측정은 여전히 하지만 연결 toowhichever 유형의 원격 분석 자신의 스트림의 TrackMetric 전송한 메트릭을 표시 하는 동안 (이벤트 또는 요청, 및 등)에 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="89b5a-313">성능 카운터 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-313">Performance counters table</span></span>
<span data-ttu-id="89b5a-314">[성능 카운터](app-insights-performance-counters.md)는 CPU, 메모리, 네트워크 사용률 등 앱에 대한 기본 시스템 메트릭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="89b5a-315">Hello SDK toosend 추가 카운터를 사용자 지정 카운터를 포함 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="89b5a-316">hello **performanceCounters** 스키마는 hello 노출 `category`, `counter` 이름 및 `instance` 각 성능 카운터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="89b5a-317">카운터 인스턴스 이름이 해당 toosome 성능 카운터만 되며 일반적으로 hello 프로세스 toowhich hello 수의 hello 이름을 연결 됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="89b5a-318">각 응용 프로그램에 대 한 hello 원격 분석에서 해당 응용 프로그램에 대 한 hello 카운터에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="89b5a-319">예를 들어 toosee 어떤 카운터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-319">For example, toosee what counters are available:</span></span>

![Application Insights 분석의 성능 카운터](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="89b5a-321">hello 통해 사용 가능한 메모리의 차트 tooget 기간 선택:</span><span class="sxs-lookup"><span data-stu-id="89b5a-321">tooget a chart of available memory over hello selected period:</span></span>

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="89b5a-323">마찬가지로 다른 원격 분석 **performanceCounters** 열도 `cloud_RoleInstance` 앱 실행 되 고 있는 hello 호스트 컴퓨터의 hello id를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="89b5a-324">예를 들어 toocompare hello 응용 프로그램의 성능을 hello 서로 다른 컴퓨터에서:</span><span class="sxs-lookup"><span data-stu-id="89b5a-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="89b5a-326">예외 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-326">Exceptions table</span></span>
<span data-ttu-id="89b5a-327">[앱에서 보고된 예외](app-insights-asp-net-exceptions.md)는 이 테이블에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="89b5a-328">toofind hello hello 예외가 발생 했을 때 앱을 처리 하는 HTTP 요청, operation_Id에 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Operation_Id에 요청을 사용하여 예외를 조인](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="89b5a-330">브라우저 타이밍 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-330">Browser timings table</span></span>
<span data-ttu-id="89b5a-331">`browserTimings`은 사용자의 브라우저에서 수집된 페이지 로드 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="89b5a-332">[클라이언트 쪽 원격 분석을 위한 응용 프로그램 설정](app-insights-javascript.md) 의 순서로 toosee 이러한 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="89b5a-333">hello 스키마에는 [hello 길이의 hello 페이지 로드 프로세스의 여러 단계를 나타내는 메트릭](app-insights-javascript.md#page-load-performance)합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="89b5a-334">(사용자가 페이지를 읽을 시간의 hello 길이 나타냅니다 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="89b5a-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="89b5a-335">서로 다른 페이지의 hello popularities를 표시 하 고 각 페이지에 대 한 시간 로드:</span><span class="sxs-lookup"><span data-stu-id="89b5a-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="89b5a-337">가용성 결과 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-337">Availability results table</span></span>
<span data-ttu-id="89b5a-338">`availabilityResults`표시의 결과 hello 프로그램 [웹 테스트](app-insights-monitor-web-app-availability.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="89b5a-339">각 테스트 위치에서 테스트가 실행될 때마다 개별적으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-339">Each run of your tests from each test location is reported separately.</span></span>

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="89b5a-341">종속성 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-341">Dependencies table</span></span>
<span data-ttu-id="89b5a-342">호출의 결과 포함 tooTrackDependency() 호출 toodatabases 및 REST Api 및 기타 앱이 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="89b5a-343">또한 hello 브라우저에서 AJAX 호출을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="89b5a-344">Hello 브라우저에서 AJAX 호출:</span><span class="sxs-lookup"><span data-stu-id="89b5a-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="89b5a-345">종속성 호출 hello 서버에서:</span><span class="sxs-lookup"><span data-stu-id="89b5a-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="89b5a-346">서버 쪽 종속성 결과 항상 표시 `success==False` hello Application Insights 에이전트는 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="89b5a-347">그러나 hello 다른 데이터 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="89b5a-348">추적 테이블</span><span class="sxs-lookup"><span data-stu-id="89b5a-348">Traces table</span></span>
<span data-ttu-id="89b5a-349">Tracktrace ()를 사용 하 여 앱에서 보낸 hello 원격 분석을 포함 또는 [다른 로깅 프레임 워크](app-insights-asp-net-trace-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="89b5a-350">비디오</span><span class="sxs-lookup"><span data-stu-id="89b5a-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="89b5a-351">고급 쿼리:</span><span class="sxs-lookup"><span data-stu-id="89b5a-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="89b5a-352">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89b5a-352">Next steps</span></span>
* [<span data-ttu-id="89b5a-353">분석 언어 참조</span><span class="sxs-lookup"><span data-stu-id="89b5a-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="89b5a-354">[SQL-사용자의 치트 시트](https://aka.ms/sql-analytics) hello 가장 일반적인 구문으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89b5a-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
