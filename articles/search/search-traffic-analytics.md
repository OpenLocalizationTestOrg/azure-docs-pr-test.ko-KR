---
title: "Azure Search을 위한 검색 트래픽 분석 | Microsoft Docs"
description: "Microsoft Azure에서 Azure 검색을 위한 검색 트래픽 분석 및 클라우드 호스트된 검색 서비스를 사용하여 사용자와 데이터를 이해할 수 있습니다."
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
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="0b748-103">검색 트래픽 분석이란</span><span class="sxs-lookup"><span data-stu-id="0b748-103">What is search traffic analytics</span></span>
<span data-ttu-id="0b748-104">검색 트래픽 분석은 검색 서비스에 대한 피드백 루프를 구현하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="0b748-105">이 패턴은 필요한 데이터 및 여러 플랫폼에서 서비스를 모니터링할 수 있는 업계 선두 제품인 Application Insights를 사용하여 필요한 데이터를 수집하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="0b748-106">검색 트래픽 분석은 검색 서비스에 대한 고급 정보를 제공하고 사용자와 사용자 동작을 이해할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="0b748-107">사용자가 선택하는 항목에 대한 데이터를 확보하면 검색 환경을 더욱 개선하는 의사 결정을 내릴 수 있으며, 결과가 예상과 다를 때 백오프가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="0b748-108">Azure Search는 Azure Application Insights와 Power BI를 통합하여 심층 모니터링 및 추적이 가능한 원격 분석 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="0b748-109">Azure Search와의 상호 작용은 API를 통해서만 가능하므로 개발자가 이 페이지의 지침에 따라 검색을 사용하여 원격 분석을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="0b748-110">관련 검색 데이터 식별</span><span class="sxs-lookup"><span data-stu-id="0b748-110">Identify the relevant search data</span></span>

<span data-ttu-id="0b748-111">유용한 검색 메트릭을 확보하려면 검색 응용 프로그램의 사용자로부터 일부 신호를 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="0b748-112">이러한 신호는 사용자가 관심을 보이고 자신의 요구 사항에 관련이 있다고 생각하는 콘텐츠를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="0b748-113">검색 트래픽 분석에는 다음 두 신호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="0b748-114">사용자가 생성한 검색 이벤트: 사용자가 시작한 검색 쿼리만 흥미를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="0b748-115">패싯, 추가 콘텐츠 또는 내부 정보를 채우는 데 사용되는 검색 요청은 중요하지 않으며 결과를 왜곡하고 편견을 갖게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="0b748-116">사용자가 생성한 클릭 이벤트: 이 문서를 클릭함으로써 우리는 검색 쿼리에서 반환된 특정 검색 결과를 선택하는 사용자를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="0b748-117">클릭은 일반적으로 문서가 특정 검색 쿼리와 관련된 결과라는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="0b748-118">상관 관계 id를 사용하여 검색 이벤트와 클릭 이벤트를 연결하면 응용 프로그램에서 사용자의 동작을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="0b748-119">검색 트래픽 로그만으로는 이처럼 검색 관련 고급 정보를 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="0b748-120">검색 트래픽 분석을 구현하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b748-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="0b748-121">사용자는 검색 응용 프로그램과 상호 작용하므로 검색 응용 프로그램에서 이전 섹션에 언급된 신호를 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="0b748-122">Application Insights는 확장 가능한 모니터링 솔루션으로, 여러 플랫폼에 사용할 수 있으며 유연한 계측 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="0b748-123">Application Insights를 사용하면 Azure Search에서 작성하는 Power BI 검색 보고서를 활용하여 보다 쉽게 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="0b748-124">Azure Search 서비스의 [포털](https://portal.azure.com) 페이지에 있는 검색 트래픽 분석 블레이드는 이 원격 분석 패턴을 따르는 치트 시트를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="0b748-125">또한 한 장소에서 Application Insights 리소스를 선택하거나 만들고, 필요한 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![검색 트래픽 분석 지침][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="0b748-127">1. Application Insights 리소스 선택</span><span class="sxs-lookup"><span data-stu-id="0b748-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="0b748-128">사용할 Application Insights 리소스를 선택하거나 리소스가 없는 경우 직접 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="0b748-129">이미 사용 중인 리소스를 사용하여 필요한 사용자 지정 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="0b748-130">새 Application Insights 리소스를 만들 때 모든 응용 프로그램 유형은 이 시나리오에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="0b748-131">사용 중인 플랫폼에 가장 적합한 것을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="0b748-132">응용 프로그램의 원격 분석 클라이언트를 만들기 위한 계측 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="0b748-133">Application Insights 포털 대시보드에서 가져올 수도 있고, 검색 트래픽 분석 페이지에서 가져온 후 사용할 인스턴스를 선택해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="0b748-134">2. 응용 프로그램 계측</span><span class="sxs-lookup"><span data-stu-id="0b748-134">2. Instrument your application</span></span>

<span data-ttu-id="0b748-135">이 단계에서는 위의 단계에서 만든 Application Insights 리소스를 사용하여 사용자 고유의 검색 응용 프로그램을 계측합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="0b748-136">이 프로세스에는 다음과 같은 네 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-136">There are four steps to this process:</span></span>

<span data-ttu-id="0b748-137">**I. 원격 분석 클라이언트 만들기** Application Insights 리소스에 이벤트를 전송하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="0b748-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="0b748-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="0b748-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0b748-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="0b748-140">다른 언어 및 플랫폼은 전체 [목록](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b748-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="0b748-141">**II. 상관 관계에 대한 검색 ID 요청** 검색 요청과 클릭 간에 상관 관계를 지정하려면 이러한 두 이벤트를 관련 짓는 상관 관계 id가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="0b748-142">사용자가 헤더를 사용하여 Search Id를 요청하면 Azure Search가 Search Id를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="0b748-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="0b748-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="0b748-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0b748-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="0b748-145">**III. 로그 검색 이벤트**</span><span class="sxs-lookup"><span data-stu-id="0b748-145">**III. Log Search events**</span></span>

<span data-ttu-id="0b748-146">사용자는 검색 요청을 실행할 때마다 Application Insights 사용자 지정 이벤트에서 다음 스키마로 해당 검색 요청을 검색 이벤트로 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="0b748-147">**ServiceName**: (문자열) 검색 서비스 이름 **SearchId**: (guid) 검색 쿼리의 고유 식별자(검색 응답에 제공) **IndexName**: (문자열) 쿼리할 검색 서비스 인덱스 **QueryTerms**: (문자열) 사용자가 입력한 검색 용어 **ResultCount**: (정수) 반환된 문서 수(검색 응답에 제공) **ScoringProfile**: (문자열) 사용된 점수 매기기 프로필(있는 경우)의 이름</span><span class="sxs-lookup"><span data-stu-id="0b748-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="0b748-148">검색 쿼리에 $count=true를 추가하여 사용자가 생성한 쿼리 수를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="0b748-149">자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b748-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="0b748-150">사용자가 생성한 검색 쿼리만 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="0b748-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="0b748-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="0b748-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0b748-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="0b748-153">**IV. 클릭 이벤트 기록**</span><span class="sxs-lookup"><span data-stu-id="0b748-153">**IV. Log Click events**</span></span>

<span data-ttu-id="0b748-154">사용자가 문서를 클릭할 때마다 검색 분석을 위해 신호를 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="0b748-155">Application Insights 사용자 지정 이벤트를 사용하여 다음 스키마로 이러한 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="0b748-156">**ServiceName**: (문자열) 검색 서비스 이름 **SearchId**: (guid) 관련 검색 쿼리의 고유 식별자 **DocId**: (문자열) 문서 식별자 **Position**: (정수) 검색 결과 페이지의 문서 순위</span><span class="sxs-lookup"><span data-stu-id="0b748-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="0b748-157">위치는 응용 프로그램의 카디널 순서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="0b748-158">이 숫자가 항상 같다면 이 숫자를 자유롭게 설정하여 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="0b748-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="0b748-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="0b748-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="0b748-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="0b748-161">3. Power BI Desktop으로 분석</span><span class="sxs-lookup"><span data-stu-id="0b748-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="0b748-162">앱을 계측하고 응용 프로그램이 Application Insights에 올바르게 연결되었는지 확인했으면 Power BI Desktop용 Azure Search에서 작성한 미리 정의된 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="0b748-163">이 템플릿에는 보다 많은 정보를 기반으로 검색 성능 및 관련성을 개선하는 합리적 결정을 내릴 수 있도록 각종 차트와 테이블이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="0b748-164">Power BI Desktop 템플릿을 인스턴스화하려면 Application Insights에 대한 세 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="0b748-165">이 데이터는 사용할 리소스를 선택할 때 검색 트래픽 분석 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![검색 트래픽 분석 블레이드의 Application Insights 데이터][2]

<span data-ttu-id="0b748-167">Power BI Desktop 템플릿에 포함된 메트릭:</span><span class="sxs-lookup"><span data-stu-id="0b748-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="0b748-168">CTR(클릭률): 특정 문서를 클릭한 사용자와 총 검색 수의 비율.</span><span class="sxs-lookup"><span data-stu-id="0b748-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="0b748-169">클릭 없이 검색: 클릭을 등록하지 않는 상위 쿼리를 일컫는 용어</span><span class="sxs-lookup"><span data-stu-id="0b748-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="0b748-170">최다 클릭 문서: 최근 24시간, 7일 및 30일 동안 ID별로 클릭 횟수가 가장 많은 문서.</span><span class="sxs-lookup"><span data-stu-id="0b748-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="0b748-171">인기 용어-문서 쌍: 같은 문서를 클릭하는 결과로 이어진 용어이며 클릭 수를 기준으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="0b748-172">시간 대비 클릭: 검색 쿼리 이후 시간 별로 버킷 구성된 클릭</span><span class="sxs-lookup"><span data-stu-id="0b748-172">Time to click: clicks bucketed by time since the search query</span></span>

![Application Insights에서 읽기 위한 Power BI 템플릿][3]


## <a name="next-steps"></a><span data-ttu-id="0b748-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b748-174">Next Steps</span></span>
<span data-ttu-id="0b748-175">검색 응용 프로그램을 계측하여 검색 서비스에 대한 강력하고 통찰력 있는 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="0b748-176">Application Insights에 대한 추가 정보는 [여기](https://go.microsoft.com/fwlink/?linkid=842905)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b748-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="0b748-177">Application Insights [가격 책정 페이지](https://azure.microsoft.com/pricing/details/application-insights/)를 방문하여 다양한 서비스 계층에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0b748-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="0b748-178">놀라운 보고서 만들기에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0b748-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="0b748-179">자세한 내용은 [Power BI Desktop 시작](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b748-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
