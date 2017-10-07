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
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="02260-103">검색 트래픽 분석이란</span><span class="sxs-lookup"><span data-stu-id="02260-103">What is search traffic analytics</span></span>
<span data-ttu-id="02260-104">검색 트래픽 분석은 검색 서비스에 대한 피드백 루프를 구현하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="02260-105">이 패턴에서는 hello 필요한 데이터 서비스 하 고 어떻게 toocollect Application Insights로 모니터링에 대 한 업계 선두를 사용 하 여 여러 플랫폼을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="02260-106">검색 트래픽 분석은 검색 서비스에 대한 고급 정보를 제공하고 사용자와 사용자 동작을 이해할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="02260-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="02260-107">사용자의 선택에 대 한 데이터를 having, 검색 환경 및 hello 결과 예상 되지 하는 경우 해제 tooback 더욱 향상 시킬 수 toomake 결정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="02260-108">Azure 검색에서는 Azure Application Insights 및 Power BI tooprovide 세부적으로 모니터링 및 추적을 통합 하는 원격 분석 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="02260-109">Api를 통해 Azure 검색의 상호 작용 이기 때문에이 페이지에 hello 지침에 따라 검색을 사용 하 여 hello 개발자가 hello 원격 분석을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="02260-110">Hello 관련 검색 데이터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-110">Identify hello relevant search data</span></span>

<span data-ttu-id="02260-111">toohave 유용한 검색 메트릭을 것이 필요한 toolog hello 검색 응용 프로그램의 hello 사용자 로부터 일부 신호를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02260-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="02260-112">이러한 신호 관련 tootheir 필요한 지 판단 하 고 사용자가에 관심이 있는 콘텐츠를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="02260-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="02260-113">검색 트래픽 분석에는 다음 두 신호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="02260-114">사용자가 생성한 검색 이벤트: 사용자가 시작한 검색 쿼리만 흥미를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="02260-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="02260-115">추가 콘텐츠 또는 내부 정보를 검색 사용 된 요청의 toopopulate 패싯 중요 하지 않은 되 고 기울이기 고 바이어스 결과.</span><span class="sxs-lookup"><span data-stu-id="02260-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="02260-116">사용자가 생성 클릭 이벤트: tooa 사용자 검색 쿼리에서 반환 된 특정 검색 결과 선택 하 여이 문서에는 클릭, 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="02260-117">클릭은 일반적으로 문서가 특정 검색 쿼리와 관련된 결과라는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="02260-118">상관 관계 id 사용 하 여 검색 하 고 클릭 이벤트를 연결 하 여 응용 프로그램에 있는 사용자의 가능한 tooanalyze hello 동작 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="02260-119">이러한 검색 insights 불가능 한 tooobtain 검색 트래픽 로그만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02260-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="02260-120">Tooimplement은 트래픽 분석을 검색 하는 방법</span><span class="sxs-lookup"><span data-stu-id="02260-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="02260-121">hello 사용자 상호 작용 하는 대로 섹션 hello 검색 응용 프로그램에서 수집 해야 hello 앞에서 언급 한 hello 신호입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="02260-122">Application Insights는 확장 가능한 모니터링 솔루션으로, 여러 플랫폼에 사용할 수 있으며 유연한 계측 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="02260-123">Application Insights의 사용을 사용 하면 보다 쉽게 데이터의 Azure 검색 toomake hello 분석에서 만든 hello Power BI를 검색 하는 보고서를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="02260-124">Hello에 [포털](https://portal.azure.com) hello 검색 트래픽 분석 블레이드는 Azure 검색 서비스에 대 한 페이지에는 다음이 원격 분석 패턴에 대 한 보고 치트 시트 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="02260-125">있습니다 선택 또는 Application Insights 리소스를 만들고 수도 모두 한 곳에에서 hello 필요한 데이터를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02260-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![검색 트래픽 분석 지침][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="02260-127">1. Application Insights 리소스 선택</span><span class="sxs-lookup"><span data-stu-id="02260-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="02260-128">Application Insights 리소스 toouse tooselect 필요 하거나 없는 이미 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02260-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="02260-129">리소스를 이미 사용 하 여 toolog hello에 필요한 사용자 지정 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="02260-130">새 Application Insights 리소스를 만들 때 모든 응용 프로그램 유형은 이 시나리오에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="02260-131">사용 하는 hello 플랫폼에 가장 잘 맞는 hello 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="02260-132">응용 프로그램에 대 한 원격 분석 클라이언트 hello를 만들기 위한 hello 계측 키를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="02260-133">Hello Application Insights 포털 dashboard에서 가져올 수 있습니다 또는 표시할 수 있습니다 hello 검색 트래픽 분석 페이지에서 원하는 toouse hello 인스턴스를 선택 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="02260-134">2. 응용 프로그램 계측</span><span class="sxs-lookup"><span data-stu-id="02260-134">2. Instrument your application</span></span>

<span data-ttu-id="02260-135">이 단계는 여기서 있습니다 직접 검색 응용 프로그램 계측, 위의 단계에서 만든된 프로그램 hello hello Application Insights 리소스를 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="02260-136">Toothis 프로세스는 4 단계:</span><span class="sxs-lookup"><span data-stu-id="02260-136">There are four steps toothis process:</span></span>

<span data-ttu-id="02260-137">**I. 원격 분석 클라이언트 만들기** 이벤트 toohello Application Insights 리소스를 전송 하는 hello 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="02260-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="02260-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="02260-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="02260-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="02260-140">다른 언어 및 플랫폼에서 참조에 대 한 전체 hello [목록](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="02260-141">**II. 요청 상관 관계에 대 한 검색 ID** toocorrelate 검색 필요한 toohave 이러한 두 이벤트와 관련 된 상관 관계 id는 번의 클릭으로 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="02260-142">사용자가 헤더를 사용하여 Search Id를 요청하면 Azure Search가 Search Id를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="02260-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="02260-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="02260-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="02260-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="02260-145">**III. 로그 검색 이벤트**</span><span class="sxs-lookup"><span data-stu-id="02260-145">**III. Log Search events**</span></span>

<span data-ttu-id="02260-146">사용자가 검색 요청을 실행할 때마다 로그인 해야 하는 검색 이벤트로 Application Insights 사용자 지정 이벤트에 스키마를 다음과 같은 hello로:</span><span class="sxs-lookup"><span data-stu-id="02260-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="02260-147">**ServiceName**: 검색 서비스 이름 (string) **SearchId**: hello 검색 쿼리의 고유 식별자 (guid) (hello 검색 응답에서 제공) **IndexName**: 검색 서비스 인덱스 (string) 쿼리할 toobe **QueryTerms**: hello 사용자가 입력 한 (string) 검색어 **된 resultcount가**: 반환 된 문서 수 (int) (hello 검색 응답 한 형태로)  **ScoringProfile**: hello 있는 경우 프로필을 사용 하는 점수 매기기의 이름 (string)</span><span class="sxs-lookup"><span data-stu-id="02260-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="02260-148">요청 수 = true tooyour 검색 쿼리 $count을 추가 하 여 사용자가 생성 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="02260-149">자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02260-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="02260-150">사용자가 생성 되는 tooonly 로그 검색 쿼리를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="02260-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="02260-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="02260-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="02260-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="02260-153">**IV. 클릭 이벤트 기록**</span><span class="sxs-lookup"><span data-stu-id="02260-153">**IV. Log Click events**</span></span>

<span data-ttu-id="02260-154">사용자가 문서를 클릭할 때마다 검색 분석을 위해 신호를 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="02260-155">스키마를 따르는 hello Application Insights 사용자 지정 이벤트 toolog 이러한 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="02260-156">**ServiceName**: 검색 서비스 이름 (string) **SearchId**: hello 검색과 관련 된 쿼리의 고유 식별자 (guid) **DocId**: (string) 문서 식별자 **위치** : hello 검색에 대 한 hello 문서의 (int) 순위 결과 페이지</span><span class="sxs-lookup"><span data-stu-id="02260-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="02260-157">위치는 응용 프로그램에서 카디널 toohello 순서를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="02260-158">동일한 비교를 위해 tooallow 항상 hello에 것 만큼이 숫자가 무료 tooset 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02260-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="02260-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="02260-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="02260-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="02260-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="02260-161">3. Power BI Desktop으로 분석</span><span class="sxs-lookup"><span data-stu-id="02260-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="02260-162">응용 프로그램을 계측 하 고 응용 프로그램은 연결 된 올바르게 tooApplication Insights 확인 후에 Power BI desktop에 대 한 Azure 검색에서 만든 미리 정의 된 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="02260-163">이 템플릿에 차트 및 포함 하는 데 도움이 되는 테이블 검색 성능과 관련성 더욱 합리적인된 의사 결정 tooimprove를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="02260-164">tooinstantiate hello Power BI 데스크톱 템플릿, Application Insights에 대 한 정보 세 가지 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="02260-165">Hello 리소스 toouse를 선택 하면 hello 검색 트래픽 분석 페이지에서이 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Hello 검색 트래픽 분석 블레이드에서 응용 프로그램 인 사이트 데이터][2]

<span data-ttu-id="02260-167">메트릭 hello Power BI 데스크톱 템플릿에 포함:</span><span class="sxs-lookup"><span data-stu-id="02260-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="02260-168">속도 (CTR)를 통해 클릭: 총 검색의 특정 문서 toohello 번호를 클릭 하는 사용자의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="02260-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="02260-169">클릭 없이 검색: 클릭을 등록하지 않는 상위 쿼리를 일컫는 용어</span><span class="sxs-lookup"><span data-stu-id="02260-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="02260-170">문서를 클릭 하면 가장: 가장 최근 24 시간, 7 일 및 30 일 동안 hello에 ID로 문서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="02260-171">인기 있는 용어 문서 쌍: 번의 클릭으로 hello 같은 문서를 클릭 하면 발생 하는 용어를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="02260-172">시간 tooclick: hello 검색 쿼리 날짜 기준 버킷 팅 클릭</span><span class="sxs-lookup"><span data-stu-id="02260-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Application Insights에서 읽기 위한 Power BI 템플릿][3]


## <a name="next-steps"></a><span data-ttu-id="02260-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02260-174">Next Steps</span></span>
<span data-ttu-id="02260-175">검색 응용 프로그램 tooget 강력 하 고 통찰력 데이터 검색 서비스에 대 한 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="02260-176">Application Insights에 대한 추가 정보는 [여기](https://go.microsoft.com/fwlink/?linkid=842905)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02260-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="02260-177">Application Insights를 방문 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/application-insights/) toolearn의 각 서비스 계층에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="02260-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="02260-178">놀라운 보고서 만들기에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="02260-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="02260-179">자세한 내용은 [Power BI Desktop 시작](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02260-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
