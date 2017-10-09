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
# <a name="using-analytics-in-application-insights"></a>Application Insights에서 Analytics 사용
[분석](app-insights-analytics.md) 의 hello 강력한 검색 기능은 [Application Insights](app-insights-overview.md)합니다. 다음 페이지에서는 Log Analytics 쿼리 언어에 대해 설명합니다.

* **[Hello 소개 비디오를 시청](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**합니다.
* **[시뮬레이션된 데이터에 분석 드라이브를 테스트](https://analytics.applicationinsights.io/demo)**  경우 응용 프로그램 데이터 tooApplication Insights를 아직 전송 되지 않습니다.

## <a name="open-analytics"></a>Analytics 열기
Application Insights의 앱 홈 리소스에서 Analytics를 클릭합니다.

![portal.azure.com을 열고 Application Insights 리소스를 열고 Analytics를 클릭합니다.](./media/app-insights-analytics-using/001.png)

hello 인라인 자습서 수행할 수 있는 작업에 대 한 몇 가지 아이디어를 제공 합니다.

[보다 광범위한 둘러보기는 여기](app-insights-analytics-tour.md)서 제공됩니다.

## <a name="query-your-telemetry"></a>원격 분석 쿼리
### <a name="write-a-query"></a>쿼리 작성
![스키마 표시](./media/app-insights-analytics-using/150.png)

Hello 왼쪽에 나열 된 hello 테이블의 이름을 hello로 시작 (또는 hello [범위](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) 또는 [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) 연산자). 사용 하 여 `|` 의 파이프라인 a toocreate [연산자](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html)합니다. 

IntelliSense 메시지 hello 연산자 및 사용할 수 있는 hello 식 요소와 함께 표시 합니다. Hello 정보 아이콘을 클릭 (또는 CTRL + 스페이스바를 눌러) tooget 방법의 예제 및 자세한 설명과 toouse 각 요소입니다.

Hello 참조 [분석 언어 자습서](app-insights-analytics-tour.md) 및 [언어 참조](app-insights-analytics-reference.md)합니다.

### <a name="run-a-query"></a>쿼리 실행
![쿼리 실행](./media/app-insights-analytics-using/130.png)

1. 쿼리에서는 단일 줄 바꿈을 사용할 수 있습니다.
2. 내부 또는 toorun hello 쿼리 hello 끝나기 전에 hello 커서를 놓습니다.
3. 쿼리 hello 시간 범위를 확인 합니다. 쿼리에 고유한 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 절을 포함하여 재정의하거나 변경할 수 있습니다.
3. Go toorun hello 쿼리를 클릭 합니다.
4. 쿼리에 빈 줄을 넣으면 안 됩니다. 빈 줄로 구분하여 하나의 쿼리 탭에서 분리된 여러 개의 쿼리를 유지할 수 있습니다. Hello 커서 변수가 있는 hello 쿼리만 실행 됩니다.

### <a name="save-a-query"></a>쿼리 저장
![쿼리 저장](./media/app-insights-analytics-using/140.png)

1. Hello 현재 쿼리 파일을 저장 합니다.
2. 저장된 쿼리 파일을 엽니다.
3. 새 쿼리 파일을 만듭니다.

## <a name="see-hello-details"></a>Hello 세부 정보를 참조 하십시오.
전체 속성 목록이 hello 결과 toosee에 있는 모든 행을 확장 합니다. 모든 속성은 구조화 된 값-예를 들어, 사용자 지정 차원 또는 예외가 나열 hello 스택 추가로 확장할 수 있습니다.

![행 확장](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>첫 번째 hello 결과 정렬
있습니다 수 정렬, 필터링, 페이지를 매기는, 및를 쿼리에서 반환 된 hello 결과 그룹화 합니다.

> [!NOTE]
> 정렬, 그룹화 및 필터링 hello 브라우저에서 쿼리를 다시 실행 하지 않습니다. 마지막 사용자 쿼리에 의해 반환 된 hello 결과 다시 정렬할 경우. 
> 
> tooperform hello 결과가 반환 되 면 먼저 hello 서버에서 이러한 작업 hello와 함께 쿼리를 작성 [정렬](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [요약](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 및 [여기서](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 연산자입니다.
> 
> 

Hello 열 때와 마찬가지로 toosee를 끌 열 머리글 toorearrange 및 기본 형식 및 열 크기 조정 테두리를 끌어 합니다.

![열 정렬](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>항목 정렬 및 필터
열의 hello 헤드를 클릭 하 여 결과 정렬 합니다. Toosort hello 다른 방법으로 다시 클릭 하 고 클릭 세 번째로 toorevert toohello 원래 순서 지정 하 여 쿼리에서 반환 합니다.

검색 필터 아이콘 toonarrow hello를 사용 합니다.

![열 정렬 및 필터링](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>항목 그룹화
toosort 둘 이상의 열으로 그룹화를 사용 합니다. 먼저,를 사용 하도록 설정 하 여 hello 테이블 위에 hello 공간으로 열 머리글을 끕니다.

![그룹](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>일부 결과가 누락되었나요?

예상 되는 모든 hello 결과 표시 되지 않으면 생각 되 면 몇 가지 가능한 이유가 있습니다.

* **시간 범위 필터**. 기본적으로만 결과가 표시 되며 hello에서 지난 24 시간입니다. Hello 원본 테이블에서 검색 된 결과의 hello 범위를 제한 하는 자동 필터가 있습니다. 

    그러나 hello 시간 범위를 변경할 수 있습니다 hello 드롭다운 메뉴를 사용 하 여 필터입니다.

    사용자 고유의 포함 하 여 hello 자동 범위를 재정의할 수 있습니다 [ `where  ... timestamp ...` 절](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 쿼리로 합니다. 예:

    `requests | where timestamp > ago('2d')`

* **결과 제한**. Hello 포털에서 반환 된 hello 결과에 약 10, 000 행의 제한이 있습니다. 경고는 hello 제한을 초과할 경우를 보여 줍니다. 이렇게 되 면 hello 테이블에 결과 정렬 표시 되지 않습니다 항상 하면 모든 hello 실제 첫 번째 또는 마지막 결과. 

    것 좋습니다 tooavoid 적중 hello 제한 합니다. Hello 시간 범위 필터를 사용 하 여 또는 같은 연산자를 사용 합니다.

  * [top 100 by timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

10,000개가 넘는 행을 원하는 경우 [연속 내보내기](app-insights-export-telemetry.md)를 대신 사용하는 것이 좋습니다. Analytics는 원시 데이터를 검색하기 위한 것이 아니라 분석용으로 설계되었습니다.

## <a name="diagrams"></a>다이어그램
원하는 다이어그램의 hello 유형을 선택 합니다.

![다이어그램 유형 선택](./media/app-insights-analytics-using/230.png)

Hello 오른쪽 형식의 여러 열이 있으면 hello x 및 y 축을 기준으로 차원 toosplit hello 결과의 열을 선택할 수 있습니다.

기본적으로 결과 테이블로 처음 표시 하 고 hello 다이어그램을 수동으로 선택 합니다. Hello를 사용할 수 있지만 [지시문 렌더링](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) 쿼리 tooselect 다이어그램의 hello 끝에 있습니다.

### <a name="analytics-diagnostics"></a>분석 진단


급증 또는 단계 데이터에 있는 경우는 timechart에서 강조 표시 된 hello 선 위의 점을 발생할 수 있습니다. 이 분석 진단 hello 갑자기 변화를 필터링 하는 속성의 조합에 식별에 있음을 나타냅니다. Hello 지점 tooget hello 필터 및 toosee hello에 대 한 필터링 된 버전에서 자세히를 클릭 합니다. 이 변경 내용 발생된 hello를 확인할 수 있습니다. 

[진단 분석에 대해 자세히 알아보기](app-insights-analytics-diagnostics.md)


![분석 진단](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Pin toodashboard
다이어그램이 나 테이블 tooone 고정할 수 있는 프로그램 [대시보드를 공유](app-insights-dashboards.md) -hello pin 클릭 합니다. (너무 해야[앱 가격 책정 패키지 업그레이드](app-insights-pricing.md) tooturn이이 기능을 합니다.) 

![Hello pin을 클릭 합니다.](./media/app-insights-analytics-using/pin-01.png)

이 때 hello 성능 또는 웹 서비스의 사용을 모니터링할 대시보드 toohelp 종합적으로 포함할 수 있습니다 hello와 함께 매우 복잡 한 분석 기타 메트릭을 것을 의미 합니다. 

4 개 이하의 열 있으면 테이블 toohello 대시보드에 고정할 수 있습니다. Hello 상위 7 개의 행만 표시 됩니다.

### <a name="dashboard-refresh"></a>대시보드 새로 고침
hello 차트 고정 toohello 대시보드는 대략 시간 마다 hello 쿼리를 다시 실행 하 여 자동으로 새로 고쳐집니다. Hello 새로 고침 단추를 클릭할 수도 있습니다.

### <a name="automatic-simplifications"></a>자동 단순화

특정 가정을 tooa 대시보드에 고정 하면 적용된 tooa 차트 됩니다.

**시간 제한을:** 쿼리는 자동으로 제한 toohello 지난 14 일입니다. hello 효과 hello 동일한 쿼리에 포함 하는 경우 `where timestamp > ago(14d)`합니다.

**Bin 개수 제한:** 개별 저장소 (일반적으로 가로 막대형 차트의 경우) 덜 채워진된 bin는 자동으로 그룹화 되어 단일 "기타" hello 많이 포함 하는 차트를 표시 하는 경우 범주화 합니다. 예를 들어 다음 쿼리는

    requests | summarize count_search = count() by client_CountryOrRegion

분석에서 다음과 같이 표시됩니다.

![길게 늘어지는 차트](./media/app-insights-analytics-using/pin-07.png)

하지만 tooa 대시보드 고정 때 다음과 같이 보입니다.

![제한된 막대가 있는 차트](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>TooExcel 내보내기
쿼리를 실행한 후 .csv 파일을 다운로드할 수 있습니다. **Excel로 내보내기**를 클릭합니다.

## <a name="export-toopower-bi"></a>내보내기 tooPower BI
쿼리에서 hello 커서를 놓고 선택 **내보내기, Power BI**합니다.

![BI 분석 tooPower에서 내보내기](./media/app-insights-analytics-using/240.png)

Power BI에서 hello 쿼리를 실행 합니다. 일정에 따라 toorefresh 것 설정할 수 있습니다.

Power BI를 사용하여 다양한 원본에서 데이터를 결합하는 대시보드를 만들 수 있습니다.

[내보내기 tooPower BI에 대 한 자세한 정보](app-insights-export-power-bi.md)

## <a name="deep-link"></a>딥 링크

아래 링크 받기 **내보내기, 공유 링크** tooanother 사용자를 보낼 수 있습니다. Hello 사용자에 게 제공 [액세스 tooyour 리소스 그룹](app-insights-resources-roles-access-control.md), hello 쿼리 hello 분석 UI에서에서 열립니다.

(Hello 링크 hello 쿼리 텍스트 뒤에 표시 "? q =", gzip 압축 및 base 64 인코딩. Toousers 제공 하는 코드 toogenerate 딥 링크를 작성할 수 있습니다. 그러나 hello 코드에서 분석 방법은 toorun hello를 사용 하는 것을 권장 [REST API](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automation

사용 하 여 hello [데이터 액세스 REST API](https://dev.applicationinsights.io/) toorun 분석 쿼리 합니다. [예](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count)(PowerShell 사용):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

Hello 분석 UI, 달리 hello REST API 추가 되지 않습니다 자동으로 타임 스탬프 제한 tooyour 쿼리. 사용자 고유의 where 절, 거 대 한 응답을 얻기 tooavoid tooadd를 기억 합니다.



## <a name="import-data"></a>데이터 가져오기

CSV 파일에서 데이터를 가져올 수 있습니다. 일반적인 사용법은 tooimport 정적 데이터 원격 분석에서 테이블 가입할 수입니다. 

예를 들어 인증 된 사용자는 원격 분석에서 별칭 또는 난독 처리 된 id에서 지정 하는 경우 별칭 tooreal 이름을 매핑하는 테이블을 가져올 수 있습니다. 조인을 hello 요청 원격 분석을 수행 하면 hello 분석 보고서의 실제 이름으로 사용자를 식별할 수 있습니다.

### <a name="define-your-data-schema"></a>데이터 스키마 정의

1. **설정**(왼쪽 위), **데이터 원본**을 차례로 클릭합니다. 
2. Hello 지침을 진행 하 여 데이터 원본에 추가 합니다. toosupply 10 개 이상의 행을 포함 하는 hello 데이터 샘플을 요청 합니다. 그런 다음 hello 스키마를 수정합니다.

그런 다음 하 여 데이터 원본에 정의 합니다. tooimport 개별 테이블을 사용 합니다.

### <a name="import-a-table"></a>테이블 가져오기

1. Hello 목록에서 데이터 원본 정을 엽니다.
2. "업로드 하세요."를 클릭 하 고 hello 명령 tooupload hello 테이블을 따릅니다. 여기에 호출 tooa REST API, 따라서 쉽게 tooautomate 합니다. 

이제 Analytics 쿼리에서 테이블을 사용할 수 있습니다. Analytics에 표시됩니다. 

### <a name="use-hello-table"></a>Hello 테이블 사용

`usermap`이라는 데이터 원본 정의가 있고 여기에 `realName` 및 `user_AuthenticatedId`라는 두 개의 필드가 있다고 가정해 보겠습니다. hello `requests` 테이블에도 라는 필드가 `user_AuthenticatedId`쉽게 toojoin 것 이므로, 해당:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
hello 요청의 결과 테이블에는 추가 열 `realName`합니다.

### <a name="import-from-logstash"></a>LogStash에서 가져오기

사용 하는 경우 [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), 분석 tooquery 로그를 사용할 수 있습니다. 사용 하 여 hello [데이터 분석에 파이프 하는 플러그 인](https://github.com/Microsoft/logstash-output-application-insights)합니다. 

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

