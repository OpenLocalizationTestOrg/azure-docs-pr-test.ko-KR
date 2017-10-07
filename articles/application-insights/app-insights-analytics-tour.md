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
# <a name="a-tour-of-analytics-in-application-insights"></a>Application Insights의 Analytics 둘러보기
[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다. 다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.

* **[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.
* **[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.
* **[SQL-사용자의 치트 시트](https://aka.ms/sql-analytics)**  hello 가장 일반적인 구문으로 변환 합니다.

몇 가지 기본적인 쿼리 tooget 시작한 단계별로 살펴보겠습니다.

## <a name="connect-tooyour-application-insights-data"></a>Tooyour Application Insights 데이터에 연결
Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다.

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n개의 행 표시
사용자 작업(일반적으로 웹앱에서 받는 HTTP 요청)을 기록하는 데이터 요소는 `requests`라는 테이블에 저장됩니다. 각 행에는 응용 프로그램에 Application Insights SDK hello에서 받은 원격 분석 데이터 요소입니다.

Hello 테이블의 몇 가지 샘플 행을 검사 하 여 시작 하겠습니다.

![결과](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Hello 커서 위치에 배치 hello 문의 이동을 클릭 하기 전에. 문을 둘 이상의 행으로 분할할 수 있지만 문에 빈 줄을 넣으면 안 됩니다. 빈 줄은 편리 tookeep 여러 hello 창에서 쿼리를 구분 합니다.
>
>

열을 선택하고 끌어서 놓고 열로 그룹화하고 필터링합니다.

![결과의 오른쪽 위에 있는 열 선택을 클릭](./media/app-insights-analytics-tour/030.png)

모든 항목 toosee hello 세부 정보를 확장 합니다.

![테이블을 선택하고 열을 구성](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> 열 순서 toore hello 결과 hello 웹 브라우저에서 사용할 수 있는의 hello 헤드를 클릭 합니다. 하지만 큰 결과 집합에 대 한 행 다운로드 한 toohello 브라우저의 hello 번호 제한 된다는 점에 유의 합니다. 이러한 방식으로 정렬 실제 최고 hello 또는 가장 낮은 항목을 항상 표시 되지 않습니다. 안전 하 게 사용 하 여 hello toosort 항목 `top` 또는 `sort` 연산자입니다.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 및 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`유용한 tooget 결과의 빠른 샘플 않으며 임의의 순서로 hello 테이블에서 행을 표시 하는 것입니다. tooget 순서가 지정 된 뷰를 사용 하 여 `top` (예) 또는 `sort` (hello 전체 테이블)를 통해 합니다.

Hello 처음 n 개의 행을 특정 열으로 정렬 표시:

```AIQL

    requests | top 10 by timestamp desc
```

* *구문:* 대부분의 연산자에는 `by`와(과) 같은 키워드 매개 변수가 있습니다.
* `desc`은(는) 내림차순을 의미하고 `asc`은(는) 오름차순을 의미합니다.

![](./media/app-insights-analytics-tour/260.png)

`top...`을(를) 사용하면 `sort ... | take...`을(를) 보다 효율적으로 설명할 수 있습니다. 다음과 같이 작성했을 수도 있음:

```AIQL

    requests | sort by timestamp desc | take 10
```

hello 라고 할 때 결과 hello 동일 하지만 약간 더 느리게 실행 됩니다. `sort`의 별칭인 `order`을(를) 작성할 수도 있습니다.

hello 표 보기에서 열 머리글에 hello hello 결과 hello 화면에 사용 되는 toosort 될 수도 있습니다. 하지만 물론 사용한 적이 있다면 `take` 또는 `top` tooretrieve 테이블의 한 부분일 뿐, 순서를 변경할 hello 레코드만 검색 한 수행 합니다.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): 조건에 대한 필터링

특정 결과 코드를 반환하는 요청만 살펴보겠습니다.

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

hello `where` 연산자는 부울 식을 사용 합니다. 여기서 이에 관한 몇 가지 중요한 사항이 있습니다.

* `and`, `or`: 부울 연산자
* `==`, `<>`, `!=`: 같음 및 같지 않음
* `=~`, `!~`: 대/소문자 구분 없는 문자열 같음 및 같지 않음 더 많은 문자열 비교 연산자가 있습니다.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Hello 오른쪽 유형이 나타났다
성공하지 못한 요청 찾기

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Time

기본적으로 쿼리 지난 24 시간 동안 제한 된 toohello을 됩니다. 그러나 이 값을 변경할 수 있습니다.

![](./media/app-insights-analytics-tour/change-time-range.png)

Hello 시간 범위를 언급 하는 쿼리를 작성 하 여 재정의 `timestamp` where 절에서. 예:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

hello 시간 범위 기능은 해당 tooa hello 원본 테이블 중 하나에 대 한 각 언급이 다음 절을 삽입 하는 'where' 있습니다.

`ago(3d)`는 '3일 전'을 의미합니다. 기타 시간 단위에는 시간(`2h`, `2.5h`), 분(`25m`) 및 초(`10s`)가 포함됩니다.

기타 예제:

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

[날짜 및 시간 참조](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): 열 선택, 이름 바꾸기 및 계산
사용 하 여 [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) hello 열만 원하는 아웃 toopick:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

열 이름을 바꾸고 새 열을 정의할 수도 있음:

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

* 열 이름은 `['...']` 또는 `["..."]`와 같이 대괄호로 묶은 경우 공백이나 기호를 포함할 수 있습니다.
* `%`모듈로 연산자는 일반적인는 hello입니다.
* `1d` (한 자릿수, 'd' 한 개)은(는) 하루를 의미하는 시간 간격 리터럴입니다. 기타 시간 간격 리터럴에는 `12h`, `30m`, `10s`, `0.01s` 등이 있습니다.
* `floor`(별칭 `bin`) 값 아래로 toohello hello 제공 하는 기준 값의 가장 가까운 배수로 반올림 합니다. 따라서 `floor(aTime, 1s)` 초 가장 가까운 toohello 다운 시간을 반올림 합니다.

식은 모든 hello 일반적인 연산자를 포함할 수 있습니다 (`+`, `-`,...)를 다양 한 유용한 함수가 이며 합니다.

## <a name="extend"></a>Extend
사용 하 여 려는 스토리를 기존 tooadd 열 toohello 경우 [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

사용 하 여 [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) 보다 덜 자세 [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) 모든 기존 열을 hello tookeep 하려는 경우.

### <a name="convert-toolocal-time"></a>Toolocal 시간으로 변환

타임스탬프는 항상 UTC 기준입니다. 따라서 hello 미국 태평양 coast에 속하고 겨울 인 경우 사용자가 좋아할 만한이:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[요약](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): 행 그룹 집계
`Summarize` 은(는) 행 그룹에서 지정된 *집계 함수* 를 적용합니다.

예를 들어 hello 웹 앱은 toorespond tooa 요청은 보고 된 시간 hello 필드에 `duration`합니다. 살펴보겠습니다 hello 평균 응답 시간 tooall 요청:

![](./media/app-insights-analytics-tour/410.png)

또는 서로 다른 이름의 요청으로 hello 결과 분리 수 없습니다.

![](./media/app-insights-analytics-tour/420.png)

`Summarize`수집은 hello에 대 한 그룹으로 hello 스트림의 데이터 요소 hello `by` 절이 동일 하 게 평가 합니다. द क र hello `by` 식을-hello 위 예제에서에서 각 작업 이름-hello 결과 테이블의 행에 발생 합니다.

또는 하루 중 시간으로 결과를 그룹화할 수 있습니다.

![](./media/app-insights-analytics-tour/430.png)

Hello 사용 하는지 어떻게 알 `bin` 함수 (즉, `floor`). `by timestamp`을(를) 사용하면 모든 입력 행이 고유한 작은 그룹이 됩니다. 모든 연속 스칼라 숫자 like 시간이 나 서로 다른 관리 가능한 수의 불연속 값으로 toobreak hello 연속 범위에 있다고 합니다. `bin`-방금 hello 친숙 한 반올림 다운은 `floor` 함수-hello 가장 쉬운 방법은 toodo은입니다.

사용 하는 문자열의 동일한 기술을 tooreduce 범위 hello:

![](./media/app-insights-analytics-tour/440.png)

사용할 수 있는 알림 `name=` tooset hello 이름 hello 집계 식 또는 hello by-절에 결과 열입니다.

## <a name="counting-sampled-data"></a>샘플링된 데이터 수 계산
`sum(itemCount)`hello 권장 집계 toocount 이벤트입니다. 대부분의 경우 itemCount 목록을 = = 1 이면 hello 함수를 단순히 hello hello 그룹의 행 수를 계산 합니다. 되지만 [샘플링](app-insights-sampling.md) 은 작업에서 hello 원래 이벤트의 일부만 변수로 유지 됩니다 Application Insights에서 데이터 요소 참조 하면 각 데이터 요소에 대 한 개가 되도록 `itemCount` 이벤트입니다.

예를 들어 샘플링 hello 원래 이벤트가 다음 itemCount의 75%를 삭제 하는 경우 = = 4 hello 유지 레코드-즉, 보존 된 모든 레코드에 대해 있었습니다 4 개의 원래 레코드입니다.

적응 샘플링 itemCount toobe 높은 경우 응용 프로그램 사용이 기간 동안 발생 합니다.

이벤트의 hello 원래 수의 적절 한 예측 데이터를 제공 따라서 itemCount를 요약 합니다.

![](./media/app-insights-analytics-tour/510.png)

또한 한 `count()` 집계 (및 count 연산)을 실제로 수행 하려는 경우 toocount hello 그룹의 행 수에 대 한 합니다.

[집계 함수](https://docs.loganalytics.io/learn/tutorials/aggregations.html)의 범위가 있습니다.

## <a name="charting-hello-results"></a>Hello 결과 차트
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

기본적으로 결과는 테이블로 표시됩니다.

![](./media/app-insights-analytics-tour/225.png)

Hello 표 보기 보다 더 잘 수행 수입니다. Hello 세로 막대 옵션으로 hello 차트 뷰에서 hello 결과에 대해 살펴보겠습니다.

![차트를 클릭한 다음 세로 막대 차트를 선택하고 x 및 y축을 할당](./media/app-insights-analytics-tour/230.png)

되지만 (보시 hello 테이블 디스플레이에서) 시간별 hello 결과 정렬 하지 않은, hello 차트 표시에는 항상 올바른 순서로 datetime 표시 합니다.


## <a name="timecharts"></a>시간 차트
각 시간에 발생한 이벤트 수 표시:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Hello 차트 표시 옵션을 선택 합니다.

![시간 차트](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>여러 계열
Hello에서 여러 개의 식을 `summarize` 절 여러 열을 만듭니다.

Hello에서 여러 개의 식을 `by` 절 값의 각 조합에 대해 하나씩 여러 개의 행을 만듭니다.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![시간 및 위치별 요청 테이블](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>차원으로 차트를 분할
문자열 열과 hello 문자열에 숫자 열이 있는 테이블 차트 수 있으면 사용된 toosplit hello 숫자 데이터를 별도 일련의 점입니다. 여러 개의 문자열 열 이면 hello 판별자로 어떤 열 toouse를 선택할 수 있습니다.

![분석 차트 분할](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>반송률

부울 tooa 문자열 toouse 변환 판별자로:

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

### <a name="display-multiple-metrics"></a>여러 메트릭 표시
또한 toohello 타임 스탬프에 둘 이상의 숫자 열이 있는 테이블, 차트 어떠한 조합의 표시할 수 있습니다.

![분석 차트 분할](./media/app-insights-analytics-tour/110.png)

**분할하지 않음**을 선택해야 여러 숫자 열을 선택할 수 있습니다. 분할할 수 없습니다 hello에서 문자열 열에 따라 같은 시간으로 여러 개의 숫자 열을 표시 합니다.

## <a name="daily-average-cycle"></a>일일 평균 주기
Hello 평균 하루를 통해 사용량 달라질?

개수 요청 1 일, 모듈로 hello 시간별 시간으로 범주화 합니다.

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
> 현재 있는지 tooconvert 시간 기간 toodatetimes 순서 toodisplay에서 꺾은선형 차트를 확인 합니다.
>
>

## <a name="compare-multiple-daily-series"></a>여러 개의 일일 계열 비교
어떻게는 사용 시간의 경과 따라 hello 하루 중 다른 국가에서?

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

## <a name="plot-a-distribution"></a>분포 출력
서로 다른 길이의 세션이 몇 개 있습니까?

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

hello 마지막 줄은 필요한 tooconvert toodatetime입니다. 현재는 차트의 hello x 축 날짜/시간 경우에 스칼라도 표시 됩니다.

hello `where` 절 제외 원 샷 세션 (sessionDuration = = 0) 및 집합 hello hello x 축의 길이입니다.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[백분위수](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
서로 다른 세션 백분위수를 다루는 기간 범위는 무엇입니까?

쿼리를 위에 hello를 사용 하 여 하지만 hello 마지막 줄을 바꿉니다.

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

또한 hello 상한값 hello 절 순서 tooget 수치 요청이 둘 이상 있는 모든 세션을 포함 하 여 해결 하는 위치에서 제거:

![result](./media/app-insights-analytics-tour/180.png)

확인할 수 있는 사항:

* 세션의 5%가 3분 34초 미만의 기간을 가지고 있음;
* 세션의 50%가 36분 미만 동안 지속
* 세션의 5%가 7일보다 오래 지속

각 국가 대 한 별도 분석 tooget 연산자 요약 둘 다를 통해 개별적으로 toobring hello client_CountryOrRegion 열은:

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

## <a name="join"></a>Join
요청 및 예외를 비롯 하 여 액세스 tooseveral 테이블 했습니다.

toofind hello 예외 관련된 tooa 요청 실패 응답을 반환 하는 hello 테이블에 참여할 수 있습니다 `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


것이 좋습니다 toouse `project` tooselect 정당한 hello 열을 수행 하기 전에 필요한 hello 조인 합니다.
Hello에 동일한 절 hello 타임 스탬프 열의 이름을 변경 합니다.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): 결과 tooa 변수 할당

사용 하 여 `let` tooseparate hello 이전 식의 hello 부분입니다. hello 결과가 변경 되지 않습니다.

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> Hello 분석 클라이언트에서 hello 쿼리의 hello 부분 사이 빈 줄을 넣지 마세요. 해당 내용을 모두 tooexecute 있는지를 확인 합니다.
>

사용 하 여 `toscalar` tooconvert 단일 테이블 셀 tooa 값:

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


### <a name="functions"></a>함수

사용 하 여 *Let* toodefine 함수:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>중첩된 개체에 액세스
중첩된 개체에 쉽게 액세스할 수 있습니다. 예를 들어 hello 예외 스트림 다음과 같이 구조화 된 개체를 확인할 수 있습니다.

![result](./media/app-insights-analytics-tour/520.png)

에 관심이 hello 속성을 선택 하 여 평면화를 할 수 있습니다.

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Toocast hello 결과 toohello 적절 한 형식을 사용 해야 하는 참고 합니다.


## <a name="custom-properties-and-measurements"></a>사용자 지정 속성 및 측정
응용 프로그램에 연결 되 면 [사용자 지정 차원 (속성) 및 사용자 지정 측정](app-insights-api-custom-events-metrics.md#properties) tooevents, 다음에 해당 오류가 표시 hello `customDimensions` 및 `customMeasurements` 개체입니다.

예를 들어 앱이 다음을 포함한 경우입니다.

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract 분석에서 이러한 값:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify 특정 유형의 사용자 지정 차원 인지 여부.

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>대시보드
모든 가장 중요 한 차트와 테이블 함께 순서 toobring에서 결과 tooa 대시보드를 고정할 수 있습니다.

* [Azure 공유 대시보드](app-insights-dashboards.md#share-dashboards): hello 고정 아이콘을 클릭 합니다. 이렇게 하려면 공유 대시보드가 있어야 합니다. Hello Azure 포털에서에서 열기 또는 대시보드를 만들 하 고 공유를 클릭 합니다.
* [Power BI 대시보드](app-insights-export-power-bi.md): 내보내기, Power BI 쿼리를 클릭합니다. 이 대체의 장점은 광범위한 원본의 다른 결과와 함께 쿼리를 표시할 수 있다는 것입니다.

## <a name="combine-with-imported-data"></a>가져온 데이터와 결합

분석 보고서 hello 대시보드에서 멋진 보이지만 tootranslate hello 데이터 tooa를 원하는 경우에 따라 더 많은 양이 양식입니다. 예를 들어, 인증 된 사용자가 별칭으로 hello 원격 분석에서 식별 됩니다. 결과에 자신의 실제 이름을 tooshow를 원할 것입니다. toodo이 hello 별칭 toohello 실제 이름에서 매핑하는 CSV 파일이 필요 합니다.

데이터 파일을 가져오고 (요청, 예외 및 등) hello 표준 테이블 처럼 사용할 수 있습니다. 자체적으로 쿼리하거나 다른 테이블과 조인합니다. 예를 들어 usermap, 라는 테이블이 있고에 열 `realName` 및 `userId`, tootranslate hello를 사용할 수 있습니다 `user_AuthenticatedId` hello 요청 원격 분석에서 필드:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport hello 스키마 블레이드에서 테이블에서 **기타 데이터 소스**, hello 지침 tooadd 새 데이터 원본을 데이터의 샘플을 업로드 하 여 수행 합니다. 그런 다음이 정의 tooupload 테이블을 사용할 수 있습니다.

hello 가져오기 기능은 현재 미리 보기에서 다른 데이터 원본"."에서 "사용자 의견" 링크 처음 되므로 이 toosign toohello 미리 보기 프로그램을 사용 하 고 hello 링크 "새 데이터 소스 추가" 단추는으로 대체 됩니다.


## <a name="tables"></a>테이블
응용 프로그램에서 수신 하는 원격 분석의 hello 스트림이 여러 테이블을 통해 액세스할 수 있습니다. 각 테이블에 대해 사용할 수 있는 속성의 hello 스키마 hello 창의 hello 왼쪽에 표시 됩니다.

### <a name="requests-table"></a>요청 테이블
Count HTTP 요청 tooyour web app 및 페이지 이름으로 세그먼트:

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-count-requests.png)

가장에 실패 하는 hello 요청을 찾습니다.

![이름별로 분할된 요청 수 계산](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>사용자 지정 이벤트 테이블
사용 하는 경우 [의 trackevent ()](app-insights-api-custom-events-metrics.md#trackevent) toosend 사용자 고유의 이벤트를 읽을 수 있습니다이 테이블에서 합니다.

응용 프로그램 코드에 이러한 줄을 포함하는 사례:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

이러한 이벤트의 hello 빈도 표시 합니다.

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

측정값 및 차원을 hello 이벤트에서 추출:

![사용자 지정 이벤트의 표시 속도](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>사용자 지정 메트릭 테이블
사용 중인 경우 [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) toosend 메트릭 값을 직접 hello에서 그 결과 확인할 수 있습니다 **customMetrics** 스트림 합니다. 예:  

![Application Insights 분석의 사용자 지정 메트릭](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> [메트릭 탐색기](app-insights-metrics-explorer.md), 연결 된 tooany 유형의 원격 분석 메트릭 사용 하 여 보낸 함께 hello 메트릭 블레이드에 함께 표시 하는 모든 사용자 지정 측정 `TrackMetric()`합니다. 분석에서 사용자 지정 측정은 여전히 하지만 연결 toowhichever 유형의 원격 분석 자신의 스트림의 TrackMetric 전송한 메트릭을 표시 하는 동안 (이벤트 또는 요청, 및 등)에 수행 되었습니다.
>
>

### <a name="performance-counters-table"></a>성능 카운터 테이블
[성능 카운터](app-insights-performance-counters.md)는 CPU, 메모리, 네트워크 사용률 등 앱에 대한 기본 시스템 메트릭을 보여 줍니다. Hello SDK toosend 추가 카운터를 사용자 지정 카운터를 포함 하 여 구성할 수 있습니다.

hello **performanceCounters** 스키마는 hello 노출 `category`, `counter` 이름 및 `instance` 각 성능 카운터의 이름입니다. 카운터 인스턴스 이름이 해당 toosome 성능 카운터만 되며 일반적으로 hello 프로세스 toowhich hello 수의 hello 이름을 연결 됨을 나타냅니다. 각 응용 프로그램에 대 한 hello 원격 분석에서 해당 응용 프로그램에 대 한 hello 카운터에만 표시 됩니다. 예를 들어 toosee 어떤 카운터를 사용할 수 있습니다.

![Application Insights 분석의 성능 카운터](./media/app-insights-analytics-tour/analytics-performance-counters.png)

hello 통해 사용 가능한 메모리의 차트 tooget 기간 선택:

![Application Insights 분석의 메모리 시간 차트](./media/app-insights-analytics-tour/analytics-available-memory.png)

마찬가지로 다른 원격 분석 **performanceCounters** 열도 `cloud_RoleInstance` 앱 실행 되 고 있는 hello 호스트 컴퓨터의 hello id를 나타내는입니다. 예를 들어 toocompare hello 응용 프로그램의 성능을 hello 서로 다른 컴퓨터에서:

![Application Insights 분석에서 역할 인스턴스에 의해 분할된 성능](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>예외 테이블
[앱에서 보고된 예외](app-insights-asp-net-exceptions.md)는 이 테이블에서 사용할 수 있습니다.

toofind hello hello 예외가 발생 했을 때 앱을 처리 하는 HTTP 요청, operation_Id에 조인 합니다.

![Operation_Id에 요청을 사용하여 예외를 조인](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>브라우저 타이밍 테이블
`browserTimings`은 사용자의 브라우저에서 수집된 페이지 로드 데이터를 보여 줍니다.

[클라이언트 쪽 원격 분석을 위한 응용 프로그램 설정](app-insights-javascript.md) 의 순서로 toosee 이러한 메트릭을 합니다.

hello 스키마에는 [hello 길이의 hello 페이지 로드 프로세스의 여러 단계를 나타내는 메트릭](app-insights-javascript.md#page-load-performance)합니다. (사용자가 페이지를 읽을 시간의 hello 길이 나타냅니다 하지 않습니다.)  

서로 다른 페이지의 hello popularities를 표시 하 고 각 페이지에 대 한 시간 로드:

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>가용성 결과 테이블
`availabilityResults`표시의 결과 hello 프로그램 [웹 테스트](app-insights-monitor-web-app-availability.md)합니다. 각 테스트 위치에서 테스트가 실행될 때마다 개별적으로 보고됩니다.

![Analytics에서 페이지 로드 시간](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>종속성 테이블
호출의 결과 포함 tooTrackDependency() 호출 toodatabases 및 REST Api 및 기타 앱이 한다고 합니다. 또한 hello 브라우저에서 AJAX 호출을 포함 합니다.

Hello 브라우저에서 AJAX 호출:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

종속성 호출 hello 서버에서:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

서버 쪽 종속성 결과 항상 표시 `success==False` hello Application Insights 에이전트는 설치 되지 않습니다. 그러나 hello 다른 데이터 올바릅니다.

### <a name="traces-table"></a>추적 테이블
Tracktrace ()를 사용 하 여 앱에서 보낸 hello 원격 분석을 포함 또는 [다른 로깅 프레임 워크](app-insights-asp-net-trace-logs.md)합니다.

## <a name="video"></a>비디오 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

고급 쿼리:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>다음 단계
* [분석 언어 참조](app-insights-analytics-reference.md)
* [SQL-사용자의 치트 시트](https://aka.ms/sql-analytics) hello 가장 일반적인 구문으로 변환 합니다.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
