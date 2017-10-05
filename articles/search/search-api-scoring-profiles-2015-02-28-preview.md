---
title: "점수 매기기 프로필(Azure 검색 REST API 버전 2015-02-28-Preview) | Microsoft Docs"
description: "Azure 검색은 사용자가 정의한 점수 매기기 프로필을 기초로 순위의 결과를 조정할 수 있도록 하는 호스팅되는 클라우드 검색 서비스입니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: a67637d149a84313270c03d21acf8a9c1870be05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="c21c6-103">점수 매기기 프로필(Azure 검색 REST API 버전 2015-02-28-Preview)</span><span class="sxs-lookup"><span data-stu-id="c21c6-103">Scoring Profiles (Azure Search REST API Version 2015-02-28-Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="c21c6-104">이 문서에서는 [2015-02-28-Preview](search-api-2015-02-28-preview.md)에서 제공되는 점수 매기기 프로필을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-104">This article describes scoring profiles in the [2015-02-28-Preview](search-api-2015-02-28-preview.md).</span></span> <span data-ttu-id="c21c6-105">현재 [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx)에 문서화된 `2016-09-01` 버전과 여기에 설명된 `2015-02-28-Preview` 버전 간에 차이는 없지만 이 문서에서는 전체 API를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-105">Currently there is no difference between the `2016-09-01` version documented on [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) and the `2015-02-28-Preview` version described here, but we offer this document anyway in order to provide document coverage across the entire API.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="c21c6-106">개요</span><span class="sxs-lookup"><span data-stu-id="c21c6-106">Overview</span></span>
<span data-ttu-id="c21c6-107">점수 매기기는 검색 결과에 반환된 모든 항목의 검색 점수를 계산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-107">Scoring refers to the computation of a search score for every item returned in search results.</span></span> <span data-ttu-id="c21c6-108">점수는 현재 검색 작업의 컨텍스트에서 항목의 관련성을 나타내는 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-108">The score is an indicator of an item's relevance in the context of the current search operation.</span></span> <span data-ttu-id="c21c6-109">점수가 높을수록 항목의 관련성도 높습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-109">The higher the score, the more relevant the item.</span></span> <span data-ttu-id="c21c6-110">검색 결과에서 항목은 각 항목에 대해 계산된 검색 점수를 기준으로 높은 순위부터 낮은 순위로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-110">In search results, items are rank ordered from high to low, based on the search score calculated for each item.</span></span>

<span data-ttu-id="c21c6-111">Azure 검색에서는 점수를 계산할 때 기본 점수 매기기 기능을 사용하지만 점수 매기기 프로필을 통해 계산을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-111">Azure Search uses default scoring to compute an initial score, but you can customize the calculation through a scoring profile.</span></span> <span data-ttu-id="c21c6-112">점수 매기기 프로필을 사용하면 검색 결과에서 항목의 순위를 보다 강력하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-112">Scoring profiles give you greater control over the ranking of items in search results.</span></span> <span data-ttu-id="c21c6-113">예를 들어 잠재 수익을 기준으로 하여 특정 항목을 상승시키거나, 새 항목을 프로모션하거나, 너무 오랫동안 재고에 포함되어 있던 항목을 상승시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-113">For example, you might want to boost items based on their revenue potential, promote newer items, or perhaps boost items that have been in inventory too long.</span></span>

<span data-ttu-id="c21c6-114">점수 매기기 프로필은 필드, 함수 및 매개 변수로 구성된 인덱스 정의의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-114">A scoring profile is part of the index definition, composed of fields, functions, and parameters.</span></span>

<span data-ttu-id="c21c6-115">점수 매기기 프로필을 대략적으로 파악할 수 있도록 아래 예제에서는 'geo'라는 간단한 프로필을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-115">To give you an idea of what a scoring profile looks like, the following example shows a simple profile named 'geo'.</span></span> <span data-ttu-id="c21c6-116">이 프로필은 `hotelName` 필드에 검색 용어가 포함된 항목을 상승시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-116">This one boosts items that have the search term in the `hotelName` field.</span></span> <span data-ttu-id="c21c6-117">또한 `distance` 함수를 사용하여 현재 위치에서 10km 이내에 있는 항목의 순위를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-117">It also uses the `distance` function to favor items that are within ten kilometers of the current location.</span></span> <span data-ttu-id="c21c6-118">'inn'이라는 용어를 검색하는 경우 'inn'이 호텔 이름의 일부분이라면 이름에 'inn'이 포함된 호텔이 들어 있는 문서가 검색 결과에서 더 높은 순위로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-118">If someone searches on the term 'inn', and 'inn' happens to be part of the hotel name, documents that include hotels with 'inn' will appear higher in the search results.</span></span>

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

<span data-ttu-id="c21c6-119">이 점수 매기기 프로필을 사용하는 경우 쿼리 문자열에서 프로필을 지정하도록 쿼리가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-119">To use this scoring profile, your query is formulated to specify the profile on the query string.</span></span> <span data-ttu-id="c21c6-120">아래 쿼리에서 요청의 쿼리 매개 변수 `scoringProfile=geo` 에 주목합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-120">In the query below, notice the query parameter, `scoringProfile=geo` in the request.</span></span>

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

<span data-ttu-id="c21c6-121">이 쿼리는 용어 'inn'을 검색하고 현재 위치를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-121">This query searches on the term 'inn' and passes in the current location.</span></span> <span data-ttu-id="c21c6-122">이 쿼리에는 `scoringParameter`등의 다른 매개 변수도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-122">Note that this query includes other parameters, such as `scoringParameter`.</span></span> <span data-ttu-id="c21c6-123">쿼리 매개 변수에 대해서는 [문서 검색(Azure 검색 API)](search-api-2015-02-28-preview.md#SearchDocs)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-123">Query parameters are described in [Search Documents (Azure Search API)](search-api-2015-02-28-preview.md#SearchDocs).</span></span>

<span data-ttu-id="c21c6-124">점수 매기기 프로필에 대한 자세한 예제를 검토하려면 [예제](#example) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-124">Click [Example](#example) to review a more detailed example of a scoring profile.</span></span>

## <a name="what-is-default-scoring"></a><span data-ttu-id="c21c6-125">기본 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="c21c6-125">What is default scoring?</span></span>
<span data-ttu-id="c21c6-126">점수 매기기에서는 순위를 기준으로 정렬된 결과 집합의 각 항목에 대한 검색 점수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-126">Scoring computes a search score for each item in a rank ordered result set.</span></span> <span data-ttu-id="c21c6-127">검색 결과 집합의 모든 항목에는 검색 점수가 할당된 다음 점수가 가장 높은 항목부터 가장 낮은 항목으로 순위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-127">Every item in a search result set is assigned a search score, then ranked highest to lowest.</span></span> <span data-ttu-id="c21c6-128">그리고 점수가 높은 항목이 응용 프로그램에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-128">Items with the higher scores are returned to the application.</span></span> <span data-ttu-id="c21c6-129">기본적으로는 상위 50개 항목이 반환되지만 `$top` 매개 변수를 사용하여 반환되는 항목 수를 늘리거나 줄일 수 있습니다(단일 응답에서 최대 1,000개의 항목 반환 가능).</span><span class="sxs-lookup"><span data-stu-id="c21c6-129">By default, the top 50 are returned, but you can use the `$top` parameter to return a smaller or larger number of items (up to 1000 in a single response).</span></span>

<span data-ttu-id="c21c6-130">기본적으로 검색 점수는 쿼리와 데이터의 통계 속성에 따라 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-130">By default, a search score is computed based on statistical properties of the data and the query.</span></span> <span data-ttu-id="c21c6-131">Azure 검색에서는 `searchMode`에 따라 쿼리 문자열의 검색 용어를 일부 또는 모두 포함하는 문서를 찾은 다음 검색 용어가 많이 포함된 문서에 높은 점수를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-131">Azure Search finds documents that include the search terms in the query string (some or all, depending on `searchMode`), favoring documents that contain many instances of the search term.</span></span> <span data-ttu-id="c21c6-132">해당 용어가 데이터 모음에는 거의 없지만 해당 문서 내에서는 자주 나오는 경우 검색 점수가 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-132">The search score goes up even higher if the term is rare across the data corpus, but common within the document.</span></span> <span data-ttu-id="c21c6-133">이와 같은 관련성 계산 방식의 기준을 TF-IDF(용어 빈도와 문서 빈도 반비례)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-133">The basis for this approach to computing relevance is known as TF-IDF or (term frequency-inverse document frequency).</span></span>

<span data-ttu-id="c21c6-134">사용자 지정 정렬이 적용되지 않는다고 가정할 때 결과는 검색 점수를 기준으로 순위가 지정된 다음 호출 응용 프로그램으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-134">Assuming there is no custom sorting, results are then ranked by search score before they are returned to the calling application.</span></span> <span data-ttu-id="c21c6-135">`$top` 을 지정하지 않으면 검색 점수가 가장 높은 항목 50개가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-135">If `$top` is not specified, 50 items having the highest search score are returned.</span></span>

<span data-ttu-id="c21c6-136">전체 결과 집합에서 검색 점수 값이 반복될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-136">Search score values can be repeated throughout a result set.</span></span> <span data-ttu-id="c21c6-137">예를 들어 점수가 1.2인 항목이 10개, 1.0인 항목이 20개, 0.5인 항목이 20개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-137">For example, you might have 10 items with a score of 1.2, 20 items with a score of 1.0, and 20 items with a score of 0.5.</span></span> <span data-ttu-id="c21c6-138">여러 적중 항목의 검색 점수가 같은 경우 동일 점수의 항목 순서는 정의되지 않았으므로 항목이 안정적으로 정렬되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-138">When multiple hits have the same search score, the ordering of same scored items is not defined, and is not stable.</span></span> <span data-ttu-id="c21c6-139">따라서 쿼리를 다시 실행하면 항목 위치가 바뀌어 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-139">Run the query again, and you might see items shift position.</span></span> <span data-ttu-id="c21c6-140">즉, 두 항목의 점수가 같은 경우 어떤 항목이 먼저 표시되는지 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-140">Given two items with an identical score, there is no guarantee which one appears first.</span></span>

## <a name="when-to-use-custom-scoring"></a><span data-ttu-id="c21c6-141">사용자 지정 점수 매기기를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="c21c6-141">When to use custom scoring</span></span>
<span data-ttu-id="c21c6-142">기본 순위 지정 동작으로 비즈니스 목표를 충족할 수 없을 때는 점수 매기기 프로필을 하나 이상 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-142">You should create one or more scoring profiles when the default ranking behavior doesn’t go far enough in meeting your business objectives.</span></span> <span data-ttu-id="c21c6-143">새로 추가하는 항목의 검색 관련성을 높게 설정하려는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-143">For example, you might decide that search relevance should favor newly added items.</span></span> <span data-ttu-id="c21c6-144">이익률을 포함하는 필드나 잠재 수익을 나타내는 다른 필드의 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-144">Likewise, you might have a field that contains profit margin, or some other field indicating revenue potential.</span></span> <span data-ttu-id="c21c6-145">업무상 이점을 제공하는 적중 항목을 상승시키는 것이 점수 매기기 프로필의 사용 결정 시 중요한 요인으로 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-145">Boosting hits that bring benefits to your business can be an important factor in deciding to use scoring profiles.</span></span>

<span data-ttu-id="c21c6-146">또한 관련성 기반 순서 지정도 점수 매기기 프로필을 통해 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-146">Relevancy-based ordering is also implemented through scoring profiles.</span></span> <span data-ttu-id="c21c6-147">이전에 사용했던 검색 결과 페이지에서는 가격, 날짜, 등급 또는 관련성을 기준으로 결과를 정렬했다면,</span><span class="sxs-lookup"><span data-stu-id="c21c6-147">Consider search results pages you’ve used in the past that let you sort by price, date, rating, or relevance.</span></span> <span data-ttu-id="c21c6-148">Azure 검색에서는 점수 매기기 프로필을 통해 '관련성' 옵션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-148">In Azure Search, scoring profiles drive the 'relevance' option.</span></span> <span data-ttu-id="c21c6-149">관련성의 정의는 제공하려는 검색 환경의 유형과 비즈니스 목표를 통해 직접 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-149">The definition of relevance is controlled by you, predicated on business objectives and the type of search experience you want to deliver.</span></span>

<a name="example"></a>

## <a name="example"></a><span data-ttu-id="c21c6-150">예</span><span class="sxs-lookup"><span data-stu-id="c21c6-150">Example</span></span>
<span data-ttu-id="c21c6-151">위에서 설명한 것처럼 인덱스 스키마에 정의된 하나 이상의 점수 매기기 프로필을 통해 사용자 지정된 점수 매기기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-151">As noted, customized scoring is implemented through scoring profiles defined in an index schema.</span></span>

<span data-ttu-id="c21c6-152">아래 예제에서는 `boostGenre` 및 `newAndHighlyRated`의 두 점수 매기기 프로필이 포함된 인덱스의 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-152">This example shows the schema of an index with two scoring profiles (`boostGenre`, `newAndHighlyRated`).</span></span> <span data-ttu-id="c21c6-153">쿼리 매개 변수로 두 프로필 중 하나를 포함하는 쿼리를 이 인덱스에 대해 실행하는 경우 해당 프로필을 사용하여 결과 집합의 점수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-153">Any query against this index that includes either profile as a query parameter will use the profile to score the result set.</span></span>

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a><span data-ttu-id="c21c6-154">워크플로</span><span class="sxs-lookup"><span data-stu-id="c21c6-154">Workflow</span></span>
<span data-ttu-id="c21c6-155">사용자 지정 점수 매기기 동작을 구현하려면 인덱스를 정의하는 점수 매기기 프로필을 스키마에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-155">To implement custom scoring behavior, add a scoring profile to the schema that defines the index.</span></span> <span data-ttu-id="c21c6-156">인덱스 하나에 최대 16개의 점수 매기기 프로필을 포함할 수는 있지만([서비스 제한](search-limits-quotas-capacity.md) 참조) 프로필은 어떠한 지정된 쿼리에도 한 번에 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-156">You can have up to 16 scoring profiles within an index (see [Service Limits](search-limits-quotas-capacity.md)), but you can only specify one profile at time in any given query.</span></span>

<span data-ttu-id="c21c6-157">먼저 이 항목에서 제공하는 [템플릿](#bkmk_template) 을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-157">Start with the [Template](#bkmk_template) provided in this topic.</span></span>

<span data-ttu-id="c21c6-158">이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-158">Provide a name.</span></span> <span data-ttu-id="c21c6-159">점수 매기기 프로필은 선택 사항이지만 추가하려는 경우 이름을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-159">Scoring profiles are optional, but if you add one, the name is required.</span></span> <span data-ttu-id="c21c6-160">이름은 필드의 이름 지정 규칙에 따라 문자로 시작해야 하며 특수 문자와 예약어는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-160">Be sure to follow the naming conventions for fields (starts with a letter, avoids special characters and reserved words).</span></span> <span data-ttu-id="c21c6-161">자세한 내용은 [이름 지정 규칙](http://msdn.microsoft.com/library/azure/dn857353.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-161">See [Naming Rules](http://msdn.microsoft.com/library/azure/dn857353.aspx) for more information.</span></span>

<span data-ttu-id="c21c6-162">점수 매기기 프로필의 본문은 가중치가 적용된 필드와 함수에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-162">The body of the scoring profile is constructed from weighted fields and functions.</span></span>

### <a name="weights"></a><span data-ttu-id="c21c6-163">Weights</span><span class="sxs-lookup"><span data-stu-id="c21c6-163">Weights</span></span>
<span data-ttu-id="c21c6-164">점수 매기기 프로필의 `weights` 속성은 필드에 상대적 가중치를 할당하는 이름-값 쌍을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-164">The `weights` property of a scoring profile specifies name-value pairs that assign a relative weight to a field.</span></span> <span data-ttu-id="c21c6-165">[예제](#example)에서는 albumTitle, genre 및 artistName 필드가 각각 1.5, 5 및 2로 상승합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-165">In the [Example](#example), the albumTitle, genre, and artistName fields are boosted 1.5, 5, and 2, respectively.</span></span> <span data-ttu-id="c21c6-166">genre가 다른 필드보다 훨씬 크게 상승하는 이유는,</span><span class="sxs-lookup"><span data-stu-id="c21c6-166">Why is genre boosted so much higher than the others?</span></span> <span data-ttu-id="c21c6-167">`musicstoreindex`에서 'genre'의 경우처럼 비교적 비슷한 데이터를 검색하는 경우 상대 가중치의 편차가 더 커야 할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-167">If search is conducted over data that is somewhat homogeneous (as is the case with 'genre' in the `musicstoreindex`), you might need a larger variance in the relative weights.</span></span> <span data-ttu-id="c21c6-168">예를 들어 `musicstoreindex`에서 'rock'은 장르로도 표시되고 같은 구를 사용하는 장르 설명에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-168">For example, in the `musicstoreindex`, 'rock' appears as both a genre and in identically phrased genre descriptions.</span></span> <span data-ttu-id="c21c6-169">이 경우 장르 설명보다 장르에 더 높은 가중치를 적용하려면 genre 필드에 훨씬 높은 상대 가중치를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-169">If you want genre to outweigh genre description, the genre field will need a much higher relative weight.</span></span>

### <a name="functions"></a><span data-ttu-id="c21c6-170">함수</span><span class="sxs-lookup"><span data-stu-id="c21c6-170">Functions</span></span>
<span data-ttu-id="c21c6-171">함수는 특정 컨텍스트에 대해 추가 계산을 수행해야 하는 경우 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-171">Functions are used when additional calculations are required for specific contexts.</span></span> <span data-ttu-id="c21c6-172">올바른 함수 유형은 `freshness`, `magnitude`, `distance` 및 `tag`입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-172">Valid function types are `freshness`, `magnitude`, `distance` and `tag`.</span></span> <span data-ttu-id="c21c6-173">각 함수에는 고유한 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-173">Each function has parameters that are unique to it.</span></span>

* <span data-ttu-id="c21c6-174">`freshness` 을(를) 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-174">`freshness` should be used when you want to boost by how new or old an item is.</span></span> <span data-ttu-id="c21c6-175">이 함수는 datetime 필드(`Edm.DataTimeOffset`)에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-175">This function can only be used with datetime fields (`Edm.DataTimeOffset`).</span></span> <span data-ttu-id="c21c6-176">`boostingDuration` 특성은 freshness 함수에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-176">Note the `boostingDuration` attribute is used only with the freshness function.</span></span>
* <span data-ttu-id="c21c6-177">숫자 값의 크기를 기준으로 상승시키려면 `magnitude`을(를) 사용해야 합니다</span><span class="sxs-lookup"><span data-stu-id="c21c6-177">`magnitude` should be used when you want to boost based on how high or low a numeric value is.</span></span> <span data-ttu-id="c21c6-178">이 함수를 사용해야 하는 시나리오에는 이익률, 최고 가격, 최저 가격 또는 다운로드 수를 기준으로 상승시키는 경우가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-178">Scenarios that call for this function include boosting by profit margin, highest price, lowest price, or a count of downloads.</span></span> <span data-ttu-id="c21c6-179">반전 패턴을 사용하려면(예: 높은 가격의 항목보다 낮은 가격의 항목을 상승시키는 경우) 범위를 상위에서 하위로 반전시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-179">You can reverse the range, high to low, if you want the inverse pattern (for example, to boost lower-priced items more than higher-priced items).</span></span> <span data-ttu-id="c21c6-180">가격 범위가 $100에서 $1 사이인 경우 100에서 `boostingRangeStart`을(를) 설정하고 1에서 `boostingRangeEnd`을(를) 설정하여 낮은 가격의 항목을 상승시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-180">Given a range of prices from $100 to $1, you would set `boostingRangeStart` at 100 and `boostingRangeEnd` at 1 to boost the lower-priced items.</span></span> <span data-ttu-id="c21c6-181">이 함수는 double 및 integer 필드에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-181">This function can only be used with double and integer fields.</span></span>
* <span data-ttu-id="c21c6-182">근접도나 지리적 위치를 기준으로 상승시키려면 `distance`을(를) 사용해야 합니다</span><span class="sxs-lookup"><span data-stu-id="c21c6-182">`distance` should be used when you want to boost by proximity or geographic location.</span></span> <span data-ttu-id="c21c6-183">이 함수는 `Edm.GeographyPoint` 필드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-183">This function can only be used with `Edm.GeographyPoint` fields.</span></span>
* <span data-ttu-id="c21c6-184">`tag` 을(를) 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-184">`tag` should be used when you want to boost by tags in common between documents and search queries.</span></span> <span data-ttu-id="c21c6-185">이 함수는 `Edm.String` 및 `Collection(Edm.String)` 필드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-185">This function can only be used with `Edm.String` and `Collection(Edm.String)` fields.</span></span>

#### <a name="rules-for-using-functions"></a><span data-ttu-id="c21c6-186">함수 사용 규칙</span><span class="sxs-lookup"><span data-stu-id="c21c6-186">Rules for using functions</span></span>
* <span data-ttu-id="c21c6-187">함수 유형(freshness, magnitude, distance, tag)은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-187">Function type (freshness, magnitude, distance, tag) must be lower case.</span></span>
* <span data-ttu-id="c21c6-188">함수는 null 또는 빈 값을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-188">Functions cannot include null or empty values.</span></span> <span data-ttu-id="c21c6-189">특히 fieldname를 포함하는 경우에는 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-189">Specifically, if you include fieldname, you have to set it to something.</span></span>
* <span data-ttu-id="c21c6-190">함수는 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-190">Functions can only be applied to filterable fields.</span></span> <span data-ttu-id="c21c6-191">필터링 가능한 필드에 대한 자세한 내용은 [인덱스 만들기](search-api-2015-02-28-preview.md#CreateIndex) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-191">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) for more information about filterable fields.</span></span>
* <span data-ttu-id="c21c6-192">함수는 인덱스의 필드 컬렉션에 정의된 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-192">Functions can only be applied to fields that are defined in the fields collection of an index.</span></span>

<span data-ttu-id="c21c6-193">인덱스를 정의한 후 인덱스 스키마와 문서를 차례로 업로드하여 인덱스를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-193">After the index is defined, build the index by uploading the index schema, followed by documents.</span></span> <span data-ttu-id="c21c6-194">이러한 작업에 대한 지침은 [인덱스 만들기](search-api-2015-02-28-preview.md#CreateIndex) 및 [문서 추가, 업데이트 또는 삭제](search-api-2015-02-28-preview.md#AddOrUpdateDocuments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-194">See [Create Index](search-api-2015-02-28-preview.md#CreateIndex) and [Add or Update Documents](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) for instructions on these operations.</span></span> <span data-ttu-id="c21c6-195">인덱스가 작성되면 검색 데이터에 사용할 수 있는 점수 매기기 프로필을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-195">Once the index is built, you should have a functional scoring profile that works with your search data.</span></span>

<a name="bkmk_template"></a>

## <a name="template"></a><span data-ttu-id="c21c6-196">템플릿</span><span class="sxs-lookup"><span data-stu-id="c21c6-196">Template</span></span>
<span data-ttu-id="c21c6-197">이 섹션에서는 점수 매기기 프로필의 구문과 템플릿에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-197">This section shows the syntax and template for scoring profiles.</span></span> <span data-ttu-id="c21c6-198">특성 설명은 다음 섹션의 [인덱스 특성 참조](#bkmk_indexref) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-198">Refer to [Index attribute reference](#bkmk_indexref) in the next section for descriptions of the attributes.</span></span>

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies to searchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter to be passed in queries to use as reference location)
              "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a><span data-ttu-id="c21c6-199">점수 매기기 프로필 속성 참조</span><span class="sxs-lookup"><span data-stu-id="c21c6-199">Scoring profile property reference</span></span>
> [!NOTE]
> <span data-ttu-id="c21c6-200">점수 매기기 함수는 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-200">A scoring function can only be applied to fields that are filterable.</span></span>
>
>

| <span data-ttu-id="c21c6-201">속성</span><span class="sxs-lookup"><span data-stu-id="c21c6-201">Property</span></span> | <span data-ttu-id="c21c6-202">설명</span><span class="sxs-lookup"><span data-stu-id="c21c6-202">Description</span></span> |
| --- | --- |
| `name` |<span data-ttu-id="c21c6-203">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-203">Required.</span></span> <span data-ttu-id="c21c6-204">점수 매기기 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-204">This is the name of the scoring profile.</span></span> <span data-ttu-id="c21c6-205">필드와 동일한 이름 지정 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-205">It follows the same naming conventions of a field.</span></span> <span data-ttu-id="c21c6-206">즉, 이름은 문자로 시작해야 하고 마침표, 콜론 또는 @ 기호를 포함할 수 없으며 'azureSearch' 구(대/소문자 구분)로 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-206">It must start with a letter, cannot contain dots, colons or @ symbols, and cannot start with the phrase "azureSearch" (case-sensitive).</span></span> |
| `text` |<span data-ttu-id="c21c6-207">Weights 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-207">Contains the Weights property.</span></span> |
| `weights` |<span data-ttu-id="c21c6-208">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-208">Optional.</span></span> <span data-ttu-id="c21c6-209">필드 이름 및 상대적 가중치를 지정하는 이름-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-209">A name-value pair that specifies a field name and relative weight.</span></span> <span data-ttu-id="c21c6-210">상대적 가중치는 양의 정수 또는 부동 소수점 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-210">Relative weight must be a positive integer or floating-point number.</span></span> <span data-ttu-id="c21c6-211">해당하는 가중치 없이 필드 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-211">You can specify the field name without a corresponding weight.</span></span> <span data-ttu-id="c21c6-212">가중치는 다른 필드를 기준으로 특정 필드의 중요도를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-212">Weights are used to indicate the importance of one field relative to another.</span></span> |
| `functions` |<span data-ttu-id="c21c6-213">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-213">Optional.</span></span> <span data-ttu-id="c21c6-214">점수 매기기 함수는 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-214">Note that a scoring function can only be applied to fields that are filterable.</span></span> |
| `type` |<span data-ttu-id="c21c6-215">점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-215">Required for scoring functions.</span></span> <span data-ttu-id="c21c6-216">사용할 함수의 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-216">Indicates the type of function to use.</span></span> <span data-ttu-id="c21c6-217">유효한 값은 `magnitude`, `freshness`, `distance` 또는 `tag`입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-217">Valid values include `magnitude`, `freshness`, `distance` and `tag`.</span></span> <span data-ttu-id="c21c6-218">각 점수 매기기 프로필에 둘 이상의 함수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-218">You can include more than one function in each scoring profile.</span></span> <span data-ttu-id="c21c6-219">함수 이름은 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-219">The function name must be lower case.</span></span> |
| `boost` |<span data-ttu-id="c21c6-220">점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-220">Required for scoring functions.</span></span> <span data-ttu-id="c21c6-221">원점수의 승수로 사용되는 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-221">A positive number used as multiplier for raw score.</span></span> <span data-ttu-id="c21c6-222">값이 1일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-222">It cannot be equal to 1.</span></span> |
| `fieldName` |<span data-ttu-id="c21c6-223">점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-223">Required for scoring functions.</span></span> <span data-ttu-id="c21c6-224">또한 각 함수 유형에서는 추가적인 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-224">A scoring function can only be applied to fields that are part of the field collection of the index, and that are filterable.</span></span> <span data-ttu-id="c21c6-225">예를 들어 freshness는 datetime 필드에, magnitude는 integer/double 필드에, distance는 location 필드에, tag는 string/string collection 필드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-225">In addition, each function type introduces additional restrictions (freshness is used with datetime fields, magnitude with integer or double fields, distance with location fields and tag with string or string collection fields).</span></span> <span data-ttu-id="c21c6-226">필드는 함수 정의당 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-226">You can only specify a single field per function definition.</span></span> <span data-ttu-id="c21c6-227">예를 들어 같은 프로필에서 magnitude를 두 번 사용하려면 각 필드에 하나씩 두 개의 magnitude 정의를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-227">For example, to use magnitude twice in the same profile, you would need to include two definitions magnitude, one for each field.</span></span> |
| `interpolation` |<span data-ttu-id="c21c6-228">점수 매기기 함수의 필수 항목으로, 점수 매기기 함수는 인덱스 필드 컬렉션의 일부이며 필터링 가능한 필드에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-228">Required for scoring functions.</span></span> <span data-ttu-id="c21c6-229">범위 시작부터 범위 끝까지 점수 상승이 증가하는 기울기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-229">Defines the slope for which the score boosting increases from the start of the range to the end of the range.</span></span> <span data-ttu-id="c21c6-230">유효한 값은 `linear`(기본값), `constant`, `quadratic` 또는 `logarithmic`입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-230">Valid values include `linear` (default), `constant`, `quadratic`, and `logarithmic`.</span></span> <span data-ttu-id="c21c6-231">자세한 내용은 [보간 설정](#bkmk_interpolation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-231">See [Set interpolations](#bkmk_interpolation) for details.</span></span> |
| `magnitude` |<span data-ttu-id="c21c6-232">magnitude 점수 매기기 함수는 숫자 필드의 값 범위를 기준으로 순위를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-232">The magnitude scoring function is used to alter rankings based on the range of values for a numeric field.</span></span> <span data-ttu-id="c21c6-233">이 함수를 사용하는 가장 일반적인 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-233">Some of the most common usage examples of this are:</span></span><ul><li><span data-ttu-id="c21c6-234">별 등급: "별 등급" 필드 내의 값을 기준으로 점수 매기기를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-234">Star ratings: Alter the scoring based on the value within the "Star Rating" field.</span></span> <span data-ttu-id="c21c6-235">관련 항목이 두 개이면 등급이 높은 항목이 먼저 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-235">When two items are relevant, the item with the higher rating will be displayed first.</span></span></li><li><span data-ttu-id="c21c6-236">이익: 소매업체에서 두 개의 관련 문서 중 이익이 더 높은 문서를 상승시키려는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-236">Margin: When two documents are relevant, a retailer may wish to boost documents that have higher margins first.</span></span></li><li><span data-ttu-id="c21c6-237">클릭 횟수: 제품이나 페이지에 대한 클릭 동작을 추적하는 응용 프로그램의 경우 magnitude를 사용하여 가장 많은 트래픽을 받는 항목을 상승시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-237">Click counts: For applications that track click through actions to products or pages, you could use magnitude to boost items that tend to get the most traffic.</span></span></li><li><span data-ttu-id="c21c6-238">다운로드 횟수: 다운로드를 추적하는 응용 프로그램의 경우 magnitude 함수를 사용하면 다운로드 수가 가장 많은 항목을 상승시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-238">Download counts: For applications that track downloads, the magnitude function lets you boost items that have the most downloads.</span></span></li></ul> |
| `magnitude:boostingRangeStart` |<span data-ttu-id="c21c6-239">magnitude의 점수를 매길 범위의 시작 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-239">Sets the start value of the range over which magnitude is scored.</span></span> <span data-ttu-id="c21c6-240">이 값은 정수이거나 부동 소수점 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-240">The value must be an integer or floating-point number.</span></span> <span data-ttu-id="c21c6-241">별 등급 1~4에서 시작 값은 1이고</span><span class="sxs-lookup"><span data-stu-id="c21c6-241">For star ratings of 1 through 4, this would be 1.</span></span> <span data-ttu-id="c21c6-242">50%를 초과하는 이익의 경우에는 시작 값이 50입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-242">For margins over 50%, this would be 50.</span></span> |
| `magnitude:boostingRangeEnd` |<span data-ttu-id="c21c6-243">magnitude의 점수를 매길 범위의 끝 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-243">Sets the end value of the range over which magnitude is scored.</span></span> <span data-ttu-id="c21c6-244">이 값은 정수이거나 부동 소수점 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-244">The value must be an integer or floating-point number.</span></span> <span data-ttu-id="c21c6-245">별 등급 1~4에서 끝 값은 4가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-245">For star ratings of 1 through 4, this would be 4.</span></span> |
| `magnitude:constantBoostBeyondRange` |<span data-ttu-id="c21c6-246">유효한 값은 true 또는 false(기본값)입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-246">Valid values are true or false (default).</span></span> <span data-ttu-id="c21c6-247">값을 true로 설정하면 대상 필드의 값이 범위 상한보다 큰 문서에 완전 상승이 계속해서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-247">When set to true, the full boost will continue to apply to documents that have a value for the target field that’s higher than the upper end of the range.</span></span> <span data-ttu-id="c21c6-248">값을 false로 설정하는 경우에는 대상 필드의 값이 범위를 벗어나는 문서에 이 함수의 상승이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-248">If false, the boost of this function won’t be applied to documents having a value for the target field that falls outside of the range.</span></span> |
| `freshness` |<span data-ttu-id="c21c6-249">freshness 점수 매기기 함수는 DateTimeOffset 필드의 값을 기준으로 항목의 순위 점수를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-249">The freshness scoring function is used to alter ranking scores for items based on values in DateTimeOffset fields.</span></span> <span data-ttu-id="c21c6-250">예를 들어 보다 최근 날짜의 항목에 오래된 날짜의 항목보다 더 높은 순위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-250">For example, an item with a more recent date can be ranked higher than older items.</span></span> <span data-ttu-id="c21c6-251">(참고로 현재 날짜에 더 가까운 항목 같은 미래 날짜를 가진 일정 이벤트 등의 항목을 더 먼 미래의 항목보다 높게 순위를 설정할 수 있습니다.) 현재 서비스 릴리스에서는 범위의 한쪽 끝이 현재 시간으로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-251">(Note that it is also possible to rank items like calendar events with future dates such that items closer to the present can be ranked higher than items further in the future.) In the current service release, one end of the range will be fixed to the current time.</span></span> <span data-ttu-id="c21c6-252">반대쪽은 `boostingDuration`을(를) 기반으로 하는 과거의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-252">The other end is a time in the past based on the `boostingDuration`.</span></span> <span data-ttu-id="c21c6-253">나중에 시간 범위를 늘리려면 음수 `boostingDuration`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-253">To boost a range of times in the future use a negative `boostingDuration`.</span></span> <span data-ttu-id="c21c6-254">상승 기준이 최대 범위에서 최소 범위로 변경되는 비율은 점수 매기기 프로필에 적용되는 보간을 통해 결정됩니다(아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="c21c6-254">The rate at which the boosting changes from a maximum and minimum range is determined by the Interpolation applied to the scoring profile (see the figure below).</span></span> <span data-ttu-id="c21c6-255">적용된 상승 계수의 방향을 바꾸려면 1보다 작은 상승 계수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-255">To reverse the boosting factor applied, choose a boost factor of less than 1.</span></span> |
| `freshness:boostingDuration` |<span data-ttu-id="c21c6-256">특정 문서에 대해 상승을 중지할 만료 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-256">Sets an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="c21c6-257">구문 및 예제는 다음 섹션의 [boostingDuration 설정](#bkmk_boostdur)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-257">See [Set boostingDuration](#bkmk_boostdur) in the following section for syntax and examples.</span></span> |
| `distance` |<span data-ttu-id="c21c6-258">distance 점수 매기기 함수는 참조 지리적 위치와의 거리를 기준으로 문서 점수를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-258">The distance scoring function is used to affect the score of documents based on how close or far they are relative to a reference geographic location.</span></span> <span data-ttu-id="c21c6-259">참조 위치는 매개 변수에서 쿼리의 일부로 lon, lat 인수로 제공됩니다( `scoringParameter` 쿼리 매개 변수 사용).</span><span class="sxs-lookup"><span data-stu-id="c21c6-259">The reference location is given as part of the query in a parameter (using the `scoringParameter` query parameter) as a lon,lat argument.</span></span> |
| `distance:referencePointParameter` |<span data-ttu-id="c21c6-260">참조 위치로 사용하도록 쿼리에 전달할 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-260">A parameter to be passed in queries to use as reference location.</span></span> <span data-ttu-id="c21c6-261">scoringParameter는 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-261">scoringParameter is a query parameter.</span></span> <span data-ttu-id="c21c6-262">쿼리 매개 변수의 설명은 [문서 검색](search-api-2015-02-28-preview.md#SearchDocs) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-262">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `distance:boostingDistance` |<span data-ttu-id="c21c6-263">참조 위치로부터 상승 범위가 종료되는 거리(km)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-263">A number that indicates the distance in kilometers from the reference location where the boosting range ends.</span></span> |
| `tag` |<span data-ttu-id="c21c6-264">tag 점수 매기기 함수는 문서 및 검색 쿼리의 태그를 기반으로 문서 점수에 영향을 주는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-264">The tag scoring function is used to affect the score of documents based on tags in documents and search queries.</span></span> <span data-ttu-id="c21c6-265">검색 쿼리와 공통적인 태그가 있는 문서가 상승됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-265">Documents that have tags in common with the search query will be boosted.</span></span> <span data-ttu-id="c21c6-266">검색 쿼리에 대한 태그는 각 검색 요청에서 점수 매기기 매개 변수로 제공됩니다( `scoringParameter` 쿼리 매개 변수 사용).</span><span class="sxs-lookup"><span data-stu-id="c21c6-266">The tags for the search query is provided as a scoring parameter in each search request(using the `scoringParameter` query parameter).</span></span> |
| `tag:tagsParameter` |<span data-ttu-id="c21c6-267">특정 요청에 대한 태그를 지정하도록 쿼리에 전달할 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-267">A parameter to be passed in queries to specify tags for a particular request.</span></span> <span data-ttu-id="c21c6-268">`scoringParameter` 은(는) 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-268">`scoringParameter` is a query parameter.</span></span> <span data-ttu-id="c21c6-269">쿼리 매개 변수의 설명은 [문서 검색](search-api-2015-02-28-preview.md#SearchDocs) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-269">See [Search Documents](search-api-2015-02-28-preview.md#SearchDocs) for descriptions of query parameters.</span></span> |
| `functionAggregation` |<span data-ttu-id="c21c6-270">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-270">Optional.</span></span> <span data-ttu-id="c21c6-271">함수를 지정할 때만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-271">Applies only when functions are specified.</span></span> <span data-ttu-id="c21c6-272">유효한 값은 `sum`(기본값), `average`, `minimum`, `maximum` 또는 `firstMatching`입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-272">Valid values include: `sum` (default), `average`, `minimum`, `maximum`, and `firstMatching`.</span></span> <span data-ttu-id="c21c6-273">검색 점수는 여러 함수를 비롯한 여러 변수에서 계산되는 단일 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-273">A search score is a single value that is computed from multiple variables, including multiple functions.</span></span> <span data-ttu-id="c21c6-274">이 특성은 모든 함수의 상승이 단일 집계 상승으로 결합된 다음 기본 문서 점수에 적용되는 방식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-274">This attributes indicates how the boosts of all the functions are combined into a single aggregate boost that is then applied to the base document score.</span></span> <span data-ttu-id="c21c6-275">기본 점수는 문서 및 검색 쿼리에서 계산되는 tf-idf 값을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-275">The base score is based on the tf-idf value computed from the document and the search query.</span></span> |
| `defaultScoringProfile` |<span data-ttu-id="c21c6-276">검색 요청을 실행할 때 점수 매기기 프로필이 지정되어 있지 않으면 기본 점수 매기기(tf-idf만)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-276">When executing a search request, if no scoring profile is specified, then default scoring is used (tf-idf only).</span></span> <span data-ttu-id="c21c6-277">여기서 기본 점수 매기기 프로필 이름을 설정할 수 있으며 그러는 경우 Azure 검색은 검색 요청에 특정 프로필이 지정되어 있지 않으면 해당 프로필을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-277">A default scoring profile name can be set here, causing Azure Search to use that profile when no specific profile is given in the search request.</span></span> |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a><span data-ttu-id="c21c6-278">보간 설정</span><span class="sxs-lookup"><span data-stu-id="c21c6-278">Set interpolations</span></span>
<span data-ttu-id="c21c6-279">보간을 사용하면 범위 시작부터 범위 끝까지 점수 상승이 증가하는 기울기를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-279">Interpolations allow you to define the slope for which the score boosting increases from the start of the range to the end of the range.</span></span> <span data-ttu-id="c21c6-280">다음과 같은 보간을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-280">The following interpolations can be used:</span></span>

* <span data-ttu-id="c21c6-281">`Linear`: max 및 min 범위 내의 항목에 대해 항목에 적용되는 상승의 값이 지속적으로 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-281">`Linear`: For items that are within the max and min range, the boost applied to the item will be done in a constantly decreasing amount.</span></span> <span data-ttu-id="c21c6-282">Linear는 점수 매기기 프로필의 기본 보간입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-282">Linear is the default interpolation for a scoring profile.</span></span>
* <span data-ttu-id="c21c6-283">`Constant`시작 범위와 끝 범위 내의 항목에 대해 일정한 상승이 순위 결과에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-283">`Constant`: For items that are within the start and ending range, a constant boost will be applied to the rank results.</span></span>
* <span data-ttu-id="c21c6-284">`Quadratic`: 상승 값이 일정하게 감소하는 Linear 보간과는 달리 Quadratic 보간에서는 처음에 값이 조금씩 감소했다가 끝 범위가 가까워지면 값이 훨씬 큰 간격으로 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-284">`Quadratic`: In comparison to a Linear interpolation that has a constantly decreasing boost, Quadratic will initially decrease at smaller pace and then as it approaches the end range, it decreases at a much higher interval.</span></span> <span data-ttu-id="c21c6-285">이 보간 옵션은 tag 점수 매기기 함수에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-285">This interpolation option is not allowed in tag scoring functions.</span></span>
* <span data-ttu-id="c21c6-286">`Logarithmic`: 상승 값이 일정하게 감소하는 Linear 보간과는 달리 Logarithmic 보간에서는 처음에 값이 크게 감소했다가 끝 범위가 가까워질수록 값이 훨씬 작은 간격으로 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-286">`Logarithmic`: In comparison to a Linear interpolation that has a constantly decreasing boost, Logarithmic will initially decrease at higher pace and then as it approaches the end range, it decreases at a much smaller interval.</span></span> <span data-ttu-id="c21c6-287">이 보간 옵션은 tag 점수 매기기 함수에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-287">This interpolation option is not allowed in tag scoring functions.</span></span>

<span data-ttu-id="c21c6-288"><a name="Figure1"></a> ![][1]</span><span class="sxs-lookup"><span data-stu-id="c21c6-288"><a name="Figure1"></a> ![][1]</span></span>

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a><span data-ttu-id="c21c6-289">boostingDuration 설정</span><span class="sxs-lookup"><span data-stu-id="c21c6-289">Set boostingDuration</span></span>
<span data-ttu-id="c21c6-290">`boostingDuration` 은 freshness 함수의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-290">`boostingDuration` is an attribute of the freshness function.</span></span> <span data-ttu-id="c21c6-291">이 특성을 사용하여 특정 문서에 대해 상승이 중지되는 만료 기간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-291">You use it to set an expiration period after which boosting will stop for a particular document.</span></span> <span data-ttu-id="c21c6-292">예를 들어 프로모션 기간 10일 동안 특정 제품 라인이나 브랜드를 상승시키려는 경우 해당 문서에 대해 10일의 기간을 "P10D"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-292">For example, to boost a product line or brand for a 10-day promotional period, you would specify the 10-day period as "P10D" for those documents.</span></span> <span data-ttu-id="c21c6-293">또는 다음 주에 예정된 이벤트를 더 중요시하려면 "-P7D"를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-293">Or to boost upcoming events in the next week specify "-P7D".</span></span>

<span data-ttu-id="c21c6-294">`boostingDuration` 의 형식은 XSD "dayTimeDuration" 값(ISO 8601 기간 값의 제한된 하위 집합)으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-294">`boostingDuration` must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an ISO 8601 duration value).</span></span> <span data-ttu-id="c21c6-295">해당 패턴은 `[-]P[nD][T[nH][nM][nS]]`입니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-295">The pattern for this is: `[-]P[nD][T[nH][nM][nS]]`.</span></span>

<span data-ttu-id="c21c6-296">다음 표에 여러 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c21c6-296">The following table provides several examples.</span></span>

| <span data-ttu-id="c21c6-297">기간</span><span class="sxs-lookup"><span data-stu-id="c21c6-297">Duration</span></span> | <span data-ttu-id="c21c6-298">boostingDuration</span><span class="sxs-lookup"><span data-stu-id="c21c6-298">boostingDuration</span></span> |
| --- | --- |
| <span data-ttu-id="c21c6-299">1일</span><span class="sxs-lookup"><span data-stu-id="c21c6-299">1 day</span></span> |<span data-ttu-id="c21c6-300">"P1D"</span><span class="sxs-lookup"><span data-stu-id="c21c6-300">"P1D"</span></span> |
| <span data-ttu-id="c21c6-301">2일 12시간</span><span class="sxs-lookup"><span data-stu-id="c21c6-301">2 days and 12 hours</span></span> |<span data-ttu-id="c21c6-302">"P2DT12H"</span><span class="sxs-lookup"><span data-stu-id="c21c6-302">"P2DT12H"</span></span> |
| <span data-ttu-id="c21c6-303">15분</span><span class="sxs-lookup"><span data-stu-id="c21c6-303">15 minutes</span></span> |<span data-ttu-id="c21c6-304">"PT15M"</span><span class="sxs-lookup"><span data-stu-id="c21c6-304">"PT15M"</span></span> |
| <span data-ttu-id="c21c6-305">30일, 5시간, 10분, 6.334초</span><span class="sxs-lookup"><span data-stu-id="c21c6-305">30 days, 5 hours, 10 minutes, and 6.334 seconds</span></span> |<span data-ttu-id="c21c6-306">"P30DT5H10M6.334S"</span><span class="sxs-lookup"><span data-stu-id="c21c6-306">"P30DT5H10M6.334S"</span></span> |

<span data-ttu-id="c21c6-307">더 많은 예제를 보려면 [XML 스키마: Datatypes(W3.org 웹 사이트)](http://www.w3.org/TR/xmlschema11-2/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c21c6-307">For more examples, see [XML Schema: Datatypes (W3.org web site)](http://www.w3.org/TR/xmlschema11-2/).</span></span>

<span data-ttu-id="c21c6-308">**참고 항목**
MSDN의 [Azure Search 서비스 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)</span><span class="sxs-lookup"><span data-stu-id="c21c6-308">**See Also**
[Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN</span></span> <br/><span data-ttu-id="c21c6-309">
MSDN의 [인덱스 만들기(Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx)</span><span class="sxs-lookup"><span data-stu-id="c21c6-309">
[Create Index (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) on MSDN</span></span><br/><span data-ttu-id="c21c6-310">
MSDN의 [검색 인덱스에 점수 매기기 프로필 추가](http://msdn.microsoft.com/library/azure/dn798928.aspx)</span><span class="sxs-lookup"><span data-stu-id="c21c6-310">
[Add a scoring profile to a search index](http://msdn.microsoft.com/library/azure/dn798928.aspx) on MSDN</span></span><br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
