---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Azure Search REST API에서 노출된 동의어(미리 보기) 기능에 대한 예비 설명서입니다."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="6ca76-102">Azure Search의 동의어(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="6ca76-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="6ca76-103">검색 엔진의 동의어는 사용자가 실제로 용어를 제공할 필요 없이 쿼리의 범위를 암시적으로 확장하는 동등한 용어를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="6ca76-104">예를 들어 용어 "dog"와 "canine" 및 "puppy"의 동의어 연결을 지정하면 "dog", "canine" 또는 "puppy"를 포함하는 모든 문서는 쿼리의 범위에 속하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="6ca76-105">Azure Search에서 동의어 확장은 쿼리 시에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="6ca76-106">기존 작업을 중단하지 않고 동의어 맵을 서비스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="6ca76-107">인덱스를 다시 빌드할 필요 없이 **synonymMaps** 속성을 필드 정의에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="6ca76-108">자세한 내용은 [인덱스 업데이트](https://docs.microsoft.com/rest/api/searchservice/update-index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ca76-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="6ca76-109">기능 가용성</span><span class="sxs-lookup"><span data-stu-id="6ca76-109">Feature availability</span></span>

<span data-ttu-id="6ca76-110">동의어 기능은 현재 미리 보기에 있으며 최신 미리 보기 api-version(api-version=2016-09-01-Preview)에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="6ca76-111">지금은 Azure Portal 지원이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="6ca76-112">요청 시 API 버전이 지정되므로 동일한 앱에서 일반적으로 사용할 수 있는 (GA) 및 미리 보기 API를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="6ca76-113">그러나 미리 보기 API는 SLA가 적용되지 않으며 기능이 변경될 수 있으므로 프로덕션 응용 프로그램에서 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="6ca76-114">Azure Search에서 동의어를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6ca76-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="6ca76-115">Azure Search에서 동의어 지원은 사용자가 정의하고 서비스에 업로드하는 동의어 맵을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="6ca76-116">이러한 맵은 독립적인 리소스(인덱스 또는 데이터 원본 등)를 구성하며 검색 서비스의 모든 인덱스에서 검색 가능한 필드에 의해 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="6ca76-117">동의어 맵과 인덱스는 독립적으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="6ca76-118">동의어 맵을 정의하고 서비스에 업로드하면 필드 정의에서 **synonymMaps**라는 새 속성을 추가하여 필드에서 동의어 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="6ca76-119">동의어 맵 만들기, 업데이트 및 삭제는 항상 전체 문서 작업이므로 증분식으로 동의어 맵의 일부분을 만들거나 업데이트하거나 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="6ca76-120">단일 항목을 업데이트하는 경우에도 다시 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="6ca76-121">동의어를 검색 응용 프로그램에 통합하는 과정은 다음의 두 단계 프로세스로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="6ca76-122">아래 API를 통해 동의어 맵을 검색 서비스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="6ca76-123">인덱스 정의에서 동의어 맵을 사용하도록 검색 가능한 필드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="6ca76-124">SynonymMaps 리소스 API</span><span class="sxs-lookup"><span data-stu-id="6ca76-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="6ca76-125">POST 또는 PUT을 사용하여 서비스 아래에 동의어 맵을 추가하거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="6ca76-126">동의어 맵은 POST 또는 PUT을 통해 서비스에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="6ca76-127">각 규칙은 줄 바꿈 문자('\n')로 구분되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="6ca76-128">무료 서비스에서는 동의어 맵당 최대 5,000개의 규칙을 정의하고 다른 모든 SKU에서는 10,000개의 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="6ca76-129">각 규칙에는 최대 20개의 확장이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="6ca76-130">이 미리 보기에서 동의어 맵은 아래에 설명된 Apache Solr 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="6ca76-131">다른 형식의 기존 동의어 사전이 있어 이를 직접 사용하려는 경우 [UserVoice](https://feedback.azure.com/forums/263029-azure-search)에 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="6ca76-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="6ca76-132">다음 예제에서처럼 HTTP POST를 사용하여 새 동의어 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="6ca76-133">또는 PUT을 사용하여 URI에서 동의어 맵 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="6ca76-134">동의어 맵이 없으면 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="6ca76-135">Apache Solr 동의어 형식</span><span class="sxs-lookup"><span data-stu-id="6ca76-135">Apache Solr synonym format</span></span>

<span data-ttu-id="6ca76-136">Solr 형식은 동등하고 명시적인 동의어 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="6ca76-137">매핑 규칙은 이 문서([SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter))에 설명된 Apache Solr의 공개 소스 동의어 필터 사양을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="6ca76-138">다음은 동등한 동의어에 대한 샘플 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="6ca76-139">위의 규칙을 사용하면 검색 쿼리 "USA"가 "USA" 또는 "United States" 또는 "United States of America"로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="6ca76-140">명시적 매핑은 "=>" 화살표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="6ca76-141">지정되면 "=>" 왼쪽에 일치하는 검색 쿼리의 용어 시퀀스는 오른쪽에 대체 항목으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="6ca76-142">아래 규칙이 지정되면 검색 쿼리 "Washington", "Wash"</span><span class="sxs-lookup"><span data-stu-id="6ca76-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="6ca76-143">또는 "WA"가 모두 "WA"로 다시 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="6ca76-144">명시적 매핑은 지정된 방향으로만 적용돠며 이 경우 "WA" 쿼리를 "Washington"으로 다시 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="6ca76-145">서비스 아래 동의어 맵을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="6ca76-146">서비스 아래 동의어 맵을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="6ca76-147">서비스 아래 동의어 맵을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="6ca76-148">인덱스 정의에서 동의어 맵을 사용하도록 검색 가능한 필드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="6ca76-149">새 필드 속성 **synonymMaps**는 검색 가능한 필드에 사용할 동의어 맵을 지정하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="6ca76-150">동의어 맵은 서비스 수준 리소스이며 서비스 아래 인덱스의 모든 필드에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="6ca76-151">**synonymMaps**은 'Edm.String' 또는 'Collection(Edm.String)' 형식의 검색 가능한 필드에 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="6ca76-152">이 미리 보기에서는 필드당 하나의 동의어 맵만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="6ca76-153">여러 동의어 맵을 사용하려면 [UserVoice](https://feedback.azure.com/forums/263029-azure-search)에 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="6ca76-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="6ca76-154">동의어가 다른 검색 기능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="6ca76-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="6ca76-155">동의어 기능은 OR 연산자와 함께 동의어를 사용하여 원래 쿼리를 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="6ca76-156">따라서 강조 표시된 적중 항목 및 점수 매기기 프로필에서는 원래 용어 및 동의어를 같은 것으로 취급합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="6ca76-157">동의어 기능은 검색 쿼리에 적용되고 필터 또는 패싯에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="6ca76-158">마찬가지로 제안은 원래 용어만을 기반으로 하며 동의어 일치는 응답에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="6ca76-159">동의어 확장은 와일드카드 검색 용어에는 적용되지 않으며 접두사, 유사 용어 및 정규식 용어는 확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="6ca76-160">동의어 맵 빌드에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="6ca76-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="6ca76-161">간결하고 잘 설계된 동의어 맵은 가능한 일치 항목의 철저한 목록보다 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="6ca76-162">쿼리가 많은 동의어로 확장되는 경우 지나치게 크거나 복잡한 사전은 구문 분석하는 데 오래 걸리며 쿼리 대기 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="6ca76-163">사용할 용어를 추측하지 않고 [검색 트래픽 분석 보고서](search-traffic-analytics.md)를 통해 실제 용어를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="6ca76-164">예비 연습 및 유효성 검사 연습 모두에서 이 보고서를 설정 후 사용하여 동의어 일치의 이점이 되는 용어를 정확하게 결정한 다음 동의어 맵이 더 나은 결과를 산출하는지에 대한 유효성 검증으로 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="6ca76-165">미리 정의된 보고서에서 타일 "가장 일반적인 검색 쿼리" 및 "결과가 0인 검색 쿼리"는 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="6ca76-166">검색 응용 프로그램에 대한 여러 동의어 맵(예: 응용 프로그램이 다국어 고객 기반을 지원하는 언어별 맵)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="6ca76-167">현재 필드에서는 그중 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="6ca76-168">언제든지 필드의 synonymMaps 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ca76-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ca76-169">Next Steps</span></span>

- <span data-ttu-id="6ca76-170">개발(비프로덕션) 환경에 기존 인덱스가 있는 경우 작은 사전을 사용하여 동의어 추가를 통해 점수 매기기 프로필, 강조 표시된 적중 항목 및 제안 사항을 비롯한 검색 환경을 변경하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="6ca76-171">[검색 트래픽 분석을 사용하도록 설정](search-traffic-analytics.md)하고 미리 정의된 Power BI 보고서를 사용하여 가장 많이 사용되는 용어 및 제로 문서를 반환하는 용어를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="6ca76-172">이러한 통찰력을 바탕으로 인덱스에 있는 문서로 해석되어야 하는 비생산적인 쿼리에 대한 동의어를 포함하도록 사전을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ca76-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
