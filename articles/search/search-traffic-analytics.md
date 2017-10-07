---
title: "Azure 검색 트래픽 분석 aaaSearch | Microsoft Docs"
description: "Azure 검색에서는 toounlock insights 사용자 및 데이터에 대 한 Microsoft Azure에서 호스팅되는 클라우드 검색 서비스에 대 한 검색 트래픽 분석을 사용 합니다."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a>검색 트래픽 분석이란
검색 트래픽 분석은 검색 서비스에 대한 피드백 루프를 구현하기 위한 패턴입니다. 이 패턴에서는 hello 필요한 데이터 서비스 하 고 어떻게 toocollect Application Insights로 모니터링에 대 한 업계 선두를 사용 하 여 여러 플랫폼을 설명 합니다.

검색 트래픽 분석은 검색 서비스에 대한 고급 정보를 제공하고 사용자와 사용자 동작을 이해할 수 있게 해줍니다. 사용자의 선택에 대 한 데이터를 having, 검색 환경 및 hello 결과 예상 되지 하는 경우 해제 tooback 더욱 향상 시킬 수 toomake 결정 되어 있습니다.

Azure 검색에서는 Azure Application Insights 및 Power BI tooprovide 세부적으로 모니터링 및 추적을 통합 하는 원격 분석 솔루션을 제공 합니다. Api를 통해 Azure 검색의 상호 작용 이기 때문에이 페이지에 hello 지침에 따라 검색을 사용 하 여 hello 개발자가 hello 원격 분석을 구현 합니다.

## <a name="identify-hello-relevant-search-data"></a>Hello 관련 검색 데이터를 식별 합니다.

toohave 유용한 검색 메트릭을 것이 필요한 toolog hello 검색 응용 프로그램의 hello 사용자 로부터 일부 신호를 보냅니다. 이러한 신호 관련 tootheir 필요한 지 판단 하 고 사용자가에 관심이 있는 콘텐츠를 나타냅니다.

검색 트래픽 분석에는 다음 두 신호가 필요합니다.

1. 사용자가 생성한 검색 이벤트: 사용자가 시작한 검색 쿼리만 흥미를 끕니다. 추가 콘텐츠 또는 내부 정보를 검색 사용 된 요청의 toopopulate 패싯 중요 하지 않은 되 고 기울이기 고 바이어스 결과.

2. 사용자가 생성 클릭 이벤트: tooa 사용자 검색 쿼리에서 반환 된 특정 검색 결과 선택 하 여이 문서에는 클릭, 이라고 합니다. 클릭은 일반적으로 문서가 특정 검색 쿼리와 관련된 결과라는 의미입니다.

상관 관계 id 사용 하 여 검색 하 고 클릭 이벤트를 연결 하 여 응용 프로그램에 있는 사용자의 가능한 tooanalyze hello 동작 것 합니다. 이러한 검색 insights 불가능 한 tooobtain 검색 트래픽 로그만 포함 됩니다.

## <a name="how-tooimplement-search-traffic-analytics"></a>Tooimplement은 트래픽 분석을 검색 하는 방법

hello 사용자 상호 작용 하는 대로 섹션 hello 검색 응용 프로그램에서 수집 해야 hello 앞에서 언급 한 hello 신호입니다. Application Insights는 확장 가능한 모니터링 솔루션으로, 여러 플랫폼에 사용할 수 있으며 유연한 계측 옵션을 제공합니다. Application Insights의 사용을 사용 하면 보다 쉽게 데이터의 Azure 검색 toomake hello 분석에서 만든 hello Power BI를 검색 하는 보고서를 활용할 수 있습니다.

Hello에 [포털](https://portal.azure.com) hello 검색 트래픽 분석 블레이드는 Azure 검색 서비스에 대 한 페이지에는 다음이 원격 분석 패턴에 대 한 보고 치트 시트 포함 되어 있습니다. 있습니다 선택 또는 Application Insights 리소스를 만들고 수도 모두 한 곳에에서 hello 필요한 데이터를 참조 하십시오.

![검색 트래픽 분석 지침][1]

### <a name="1-select-an-application-insights-resource"></a>1. Application Insights 리소스 선택

Application Insights 리소스 toouse tooselect 필요 하거나 없는 이미 경우 새로 만듭니다. 리소스를 이미 사용 하 여 toolog hello에 필요한 사용자 지정 이벤트를 사용할 수 있습니다.

새 Application Insights 리소스를 만들 때 모든 응용 프로그램 유형은 이 시나리오에 유효합니다. 사용 하는 hello 플랫폼에 가장 잘 맞는 hello 하나를 선택 합니다.

응용 프로그램에 대 한 원격 분석 클라이언트 hello를 만들기 위한 hello 계측 키를 필요 합니다. Hello Application Insights 포털 dashboard에서 가져올 수 있습니다 또는 표시할 수 있습니다 hello 검색 트래픽 분석 페이지에서 원하는 toouse hello 인스턴스를 선택 하 합니다.

### <a name="2-instrument-your-application"></a>2. 응용 프로그램 계측

이 단계는 여기서 있습니다 직접 검색 응용 프로그램 계측, 위의 단계에서 만든된 프로그램 hello hello Application Insights 리소스를 사용 하 여입니다. Toothis 프로세스는 4 단계:

**I. 원격 분석 클라이언트 만들기** 이벤트 toohello Application Insights 리소스를 전송 하는 hello 개체입니다.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

다른 언어 및 플랫폼에서 참조에 대 한 전체 hello [목록](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)합니다.

**II. 요청 상관 관계에 대 한 검색 ID** toocorrelate 검색 필요한 toohave 이러한 두 이벤트와 관련 된 상관 관계 id는 번의 클릭으로 요청 합니다. 사용자가 헤더를 사용하여 Search Id를 요청하면 Azure Search가 Search Id를 제공합니다.

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. 로그 검색 이벤트**

사용자가 검색 요청을 실행할 때마다 로그인 해야 하는 검색 이벤트로 Application Insights 사용자 지정 이벤트에 스키마를 다음과 같은 hello로:

**ServiceName**: 검색 서비스 이름 (string) **SearchId**: hello 검색 쿼리의 고유 식별자 (guid) (hello 검색 응답에서 제공) **IndexName**: 검색 서비스 인덱스 (string) 쿼리할 toobe **QueryTerms**: hello 사용자가 입력 한 (string) 검색어 **된 resultcount가**: 반환 된 문서 수 (int) (hello 검색 응답 한 형태로)  **ScoringProfile**: hello 있는 경우 프로필을 사용 하는 점수 매기기의 이름 (string)

> [!NOTE]
> 요청 수 = true tooyour 검색 쿼리 $count을 추가 하 여 사용자가 생성 쿼리 합니다. 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)를 참조하세요.
>

> [!NOTE]
> 사용자가 생성 되는 tooonly 로그 검색 쿼리를 기억 합니다.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. 클릭 이벤트 기록**

사용자가 문서를 클릭할 때마다 검색 분석을 위해 신호를 기록해야 합니다. 스키마를 따르는 hello Application Insights 사용자 지정 이벤트 toolog 이러한 이벤트를 사용 합니다.

**ServiceName**: 검색 서비스 이름 (string) **SearchId**: hello 검색과 관련 된 쿼리의 고유 식별자 (guid) **DocId**: (string) 문서 식별자 **위치** : hello 검색에 대 한 hello 문서의 (int) 순위 결과 페이지

> [!NOTE]
> 위치는 응용 프로그램에서 카디널 toohello 순서를 의미합니다. 동일한 비교를 위해 tooallow 항상 hello에 것 만큼이 숫자가 무료 tooset 됩니다.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Power BI Desktop으로 분석

응용 프로그램을 계측 하 고 응용 프로그램은 연결 된 올바르게 tooApplication Insights 확인 후에 Power BI desktop에 대 한 Azure 검색에서 만든 미리 정의 된 서식 파일을 사용할 수 있습니다.
이 템플릿에 차트 및 포함 하는 데 도움이 되는 테이블 검색 성능과 관련성 더욱 합리적인된 의사 결정 tooimprove를 확인 합니다.

tooinstantiate hello Power BI 데스크톱 템플릿, Application Insights에 대 한 정보 세 가지 정보가 필요 합니다. Hello 리소스 toouse를 선택 하면 hello 검색 트래픽 분석 페이지에서이 데이터를 확인할 수 있습니다.

![Hello 검색 트래픽 분석 블레이드에서 응용 프로그램 인 사이트 데이터][2]

메트릭 hello Power BI 데스크톱 템플릿에 포함:

*   속도 (CTR)를 통해 클릭: 총 검색의 특정 문서 toohello 번호를 클릭 하는 사용자의 비율입니다.
*   클릭 없이 검색: 클릭을 등록하지 않는 상위 쿼리를 일컫는 용어
*   문서를 클릭 하면 가장: 가장 최근 24 시간, 7 일 및 30 일 동안 hello에 ID로 문서를 클릭 합니다.
*   인기 있는 용어 문서 쌍: 번의 클릭으로 hello 같은 문서를 클릭 하면 발생 하는 용어를 정렬 합니다.
*   시간 tooclick: hello 검색 쿼리 날짜 기준 버킷 팅 클릭

![Application Insights에서 읽기 위한 Power BI 템플릿][3]


## <a name="next-steps"></a>다음 단계
검색 응용 프로그램 tooget 강력 하 고 통찰력 데이터 검색 서비스에 대 한 지시 합니다.

Application Insights에 대한 추가 정보는 [여기](https://go.microsoft.com/fwlink/?linkid=842905)서 찾을 수 있습니다. Application Insights를 방문 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/application-insights/) toolearn의 각 서비스 계층에 대 한 자세한 합니다.

놀라운 보고서 만들기에 대해 자세히 알아보세요. 자세한 내용은 [Power BI Desktop 시작](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)을 참조하세요.

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
