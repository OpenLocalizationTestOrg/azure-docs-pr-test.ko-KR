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
# <a name="analytics-in-application-insights"></a>Application Insights의 분석
[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다. 다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다. 

* **[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.
* **[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.
* **[SQL-사용자의 치트 시트](https://aka.ms/sql-analytics)**  hello 가장 일반적인 구문으로 변환 합니다.
* **[언어 참조](app-insights-analytics-reference.md)**  모든 toouse hello 로그 분석 쿼리 언어의 강력한 기능을 hello 하는 방법에 대해 알아봅니다.


## <a name="queries-in-analytics"></a>분석의 쿼리
일반적인 쿼리는 *원본* 테이블이며 그 뒤에 `|`로 구분된 일련의 *연산자*가 있습니다. 

예를 들어 살펴보겠습니다 Hyderabad의 hello 시민 하루 중 시간과 웹 앱을 시도 하십시오. 및 we're 발생 하는 동안의 tootheir HTTP 요청을 반환 하는 어떤 결과 코드 확인해 보겠습니다. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

그룹화 시간별 hello hello hello를 통해 지난 7 일 고유 클라이언트 IP 주소를 계산 합니다. 

> [!NOTE]
> hello 이전 24 시간 동안, 외부 tooget 결과 'timestamp'를 명시적으로 쿼리에 포함 하거나 hello 시간 범위 드롭다운 메뉴를 사용 하십시오.
>

차트 프레젠테이션, toostack hello 결과 서로 다른 응답 코드에서 선택 막대 hello로 hello 결과 표시 해 보겠습니다.

![막대형 차트, X축 및 Y축 그리고 구분을 차례로 선택합니다.](./media/app-insights-analytics/020.png)

이 앱은 하이데라바드에서 점심 시간 및 취침 시간에 가장 인기 있는 것 같습니다. (또한 이러한 500개 코드를 조사해야 합니다.)

또한 강력한 통계 작업이 있습니다.

![통계 쿼리의 결과](./media/app-insights-analytics/025.png)

hello 언어는 많은 매력적인 기능:


* [필터링](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 합니다.
* [조인](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) - 요청을 페이지 뷰, 종속성 호출, 예외 및 로그 추적과 상호 연결합니다.
* 강력한 통계 [집계](https://docs.loganalytics.io/learn/tutorials/aggregations.html)기능이 있습니다.
* SQL 디버깅, 만큼 강력한 하지만 복잡 한 쿼리에 훨씬 더 쉽게: 중첩 문 대신 파이프 하면에서 하나의 기본 작업 toohello hello 데이터 다음입니다.
* 즉각적이고 강력하게 시각화합니다.
* [Pin tooAzure 대시보드 차트](app-insights-analytics-using.md#pin-to-dashboard)합니다.
* [내보내기 쿼리 tooPower BI](app-insights-analytics-using.md#export-to-power-bi)합니다.
* 한 [REST API](https://dev.applicationinsights.io/) 사용할 수 있는 toorun 쿼리 프로그래밍 방식으로, 예를 들어 Powershell에서 합니다.


## <a name="connect-tooyour-application-insights-data"></a>Tooyour Application Insights 데이터에 연결
Application Insights의 앱 [개요 블레이드](app-insights-dashboards.md) 에서 분석을 엽니다. 

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics/001.png)


## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>쿼리 예제

이러한 연습 tooillustrate hello 전원을 분석을 사용 하 여 시도해 보십시오.

 *  [요청 기간의 급증 및 단계별 증가 자동 진단](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [시계열 분석으로 성능 저하 분석](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [autocluster 및 diffpatterns로 응용 프로그램 오류 분석](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [시계열 분석으로 고급 셰이프 검색](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [슬라이딩 창 작업 tooanalyze 응용 프로그램 사용 현황 (롤링 MAU/DAU 등)를 사용 하 여](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [디버그 로그 분석을 기준으로 서비스 중단 검색](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) 및 관련 블로그 게시물([여기](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics))
 *  [간단한 디버그 로그를 사용하여 응용 프로그램 성능 프로파일링](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/))
 *  [간단한 디버그 로그를 사용 하 여 코드 흐름의 각 단계에 대 한 hello 기간 측정](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) 와 일치 하는 블로그 게시물 [여기](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [간단한 디버그 로그를 사용하여 동시성 분석](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) 및 관련 블로그 게시물([여기](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/))



## <a name="next-steps"></a>다음 단계
* Hello로 시작 하는 것이 좋습니다 [언어 자습서](app-insights-analytics-tour.md)합니다. 
* [분석 사용](app-insights-analytics-using.md)에 대해 자세히 알아보기 
* [언어 참조](app-insights-analytics-reference.md) 
