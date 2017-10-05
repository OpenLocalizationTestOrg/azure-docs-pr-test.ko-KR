---
title: "인덱스 쿼리(REST API - Azure Search) | Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성하고 검색 매개 변수를 사용하여 검색 결과를 필터링하고 정렬합니다."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 49062bec233ad35cd457f9665fa94c1855343582
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="ee2bb-103">REST API를 사용하여 Azure 검색 인덱스 쿼리</span><span class="sxs-lookup"><span data-stu-id="ee2bb-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="ee2bb-104">개요</span><span class="sxs-lookup"><span data-stu-id="ee2bb-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="ee2bb-105">포털</span><span class="sxs-lookup"><span data-stu-id="ee2bb-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="ee2bb-106">.NET</span><span class="sxs-lookup"><span data-stu-id="ee2bb-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="ee2bb-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="ee2bb-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="ee2bb-108">이 문서에서는 [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)를 사용하여 인덱스를 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="ee2bb-109">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들고](search-what-is-an-index.md) [데이터로 채워야](search-what-is-data-import.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="ee2bb-110">배경 정보는 [Azure Search에서 전체 텍스트 검색의 작동 방식](search-lucene-query-architecture.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="ee2bb-111">Azure 검색 서비스의 쿼리 API 키 식별</span><span class="sxs-lookup"><span data-stu-id="ee2bb-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="ee2bb-112">Azure 검색 REST API에 대한 모든 검색 작업의 주요 구성 요소는 프로비전한 서비스에 대해 생성한 *API 키* 입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-112">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="ee2bb-113">유효한 키가 있다면 요청을 기반으로 요청을 보내는 응용 프로그램과 이를 처리하는 서비스 사이에 신뢰가 쌓입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="ee2bb-114">[Azure Portal](https://portal.azure.com/)에 로그인하면 서비스의 API 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="ee2bb-115">Azure 검색 서비스의 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="ee2bb-116">[키] 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-116">Click the "Keys" icon</span></span>

<span data-ttu-id="ee2bb-117">서비스에는 *관리자 키* 및 *쿼리 키*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="ee2bb-118">기본 및 보조 *관리 키* 는 서비스를 관리하며 인덱스, 인덱서 및 데이터 원본을 만들고 삭제하는 기능을 비롯한 모든 작업에 전체 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="ee2bb-119">두 개의 키가 있으므로 기본 키를 다시 생성하려는 경우 보조 키를 사용하여 계속할 수 있고 반대도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="ee2bb-120">*쿼리 키* 는 인덱스 및 문서에 대한 읽기 전용 액세스를 부여하며 일반적으로 검색 요청을 실행하는 클라이언트 응용 프로그램에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="ee2bb-121">인덱스를 쿼리하기 위해 쿼리 키 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-121">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="ee2bb-122">또한 쿼리에 관리 키를 사용할 수 있지만 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege)에 따라 응용 프로그램 코드에 쿼리 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="ee2bb-123">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="ee2bb-123">Formulate your query</span></span>
<span data-ttu-id="ee2bb-124">[REST API를 사용하여 인덱스를 검색](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-124">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="ee2bb-125">한 가지 방법은 쿼리 매개 변수가 요청 본문의 JSON 개체에 정의된 HTTP POST 요청을 발급하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-125">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="ee2bb-126">다른 방법은 쿼리 매개 변수가 요청 URL 내에 정의된 HTTP GET 요청을 발급하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-126">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="ee2bb-127">쿼리 매개 변수의 크기에 있어 POST는 GET보다 더 [큰 제한](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="ee2bb-128">따라서 GET을 사용하는 것이 보다 편리한 특별한 경우가 아니라면 게시를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="ee2bb-129">게시 및 가져오기 모두의 경우 요청 URL에서 *서비스 이름*, *인덱스 이름* 및 적절한 *API 버전*을 제공해야 합니다(이 문서를 게시할 때 현재 API 버전은 `2016-09-01`임).</span><span class="sxs-lookup"><span data-stu-id="ee2bb-129">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="ee2bb-130">GET의 경우 URL 끝의 *쿼리 문자열*은 쿼리 매개 변수를 제공하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-130">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="ee2bb-131">URL 형식은 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-131">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="ee2bb-132">게시에 대한 형식이 동일하지만 쿼리 문자열 매개 변수에서 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-132">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="ee2bb-133">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="ee2bb-133">Example Queries</span></span>
<span data-ttu-id="ee2bb-134">다음은 "호텔"이라는 인덱스에 대한 몇 가지 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="ee2bb-135">이러한 쿼리는 가져오기 및 게시 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="ee2bb-136">전체 인덱스에서 용어 '예산'을 검색하고 `hotelName` 필드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-136">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="ee2bb-137">인덱스에 필터를 적용하여 하루에 150 달러가 저렴한 호텔을 찾고 `hotelId` 및 `description`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-137">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="ee2bb-138">전체 인덱스를 검색하고, 특정 필드(`lastRenovationDate`)를 내림차순으로 정렬하며, 상위 두 개의 결과를 가지고, `hotelName` 및 `lastRenovationDate`를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-138">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="ee2bb-139">HTTP 요청 제출</span><span class="sxs-lookup"><span data-stu-id="ee2bb-139">Submit your HTTP request</span></span>
<span data-ttu-id="ee2bb-140">쿼리를 HTTP 요청 URL(가져오기의 경우) 또는 본문(게시의 경우)의 일부로 작성했으므로 요청 헤더를 정의하고 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="ee2bb-141">요청 및 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ee2bb-141">Request and Request Headers</span></span>
<span data-ttu-id="ee2bb-142">가져오기에 두 개의 요청 헤더 또는 게시에 세 개의 요청 헤더를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="ee2bb-143">위의 I 단계에서 찾은 쿼리 키로 `api-key` 헤더를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-143">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="ee2bb-144">또한 관리자 키를 `api-key` 헤더로 사용할 수 있지만, 인덱스와 문서에 대한 읽기 전용 액세스 권한을 단독으로 부여하기 때문에 쿼리 키를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-144">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="ee2bb-145">`Accept` 헤더를 `application/json`으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-145">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="ee2bb-146">게시의 경우에만 `Content-Type` 헤더를 `application/json`으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-146">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="ee2bb-147">"모텔"이라는 용어를 검색하는 간단한 쿼리를 통해 Azure Search REST API를 사용하는 "호텔" 인덱스를 검색하는 HTTP GET 요청에 대해서는 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-147">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="ee2bb-148">이번에는 HTTP 게시를 사용하는 동일한 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-148">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="ee2bb-149">성공적인 쿼리 요청은 `200 OK` 인 상태 코드를 발생시키고 검색 결과는 응답 본문에서 JSON 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-149">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="ee2bb-150">다음은 위의 쿼리 모양에 대한 결과이며 "호텔" 인덱스가 [REST API를 사용하여 Azure 검색에서 데이터 가져오기](search-import-data-rest-api.md) 의 샘플 데이터로 채워진다고 가정합니다(명확하게 하기 위해 JSON 형식을 지정함).</span><span class="sxs-lookup"><span data-stu-id="ee2bb-150">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="ee2bb-151">자세한 내용은 [문서 검색](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)의 "응답" 섹션을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-151">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="ee2bb-152">오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee2bb-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
