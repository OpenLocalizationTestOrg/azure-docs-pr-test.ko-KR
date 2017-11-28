---
title: "aaa \"는 인덱스 (REST API-Azure 검색) 쿼리하여 | \"Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성 하 고 검색 매개 변수 toofilter 및 정렬 검색 결과 사용 합니다."
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
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="55e87-103">Hello REST API를 사용 하 여 Azure 검색 인덱스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="55e87-104">개요</span><span class="sxs-lookup"><span data-stu-id="55e87-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="55e87-105">포털</span><span class="sxs-lookup"><span data-stu-id="55e87-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="55e87-106">.NET</span><span class="sxs-lookup"><span data-stu-id="55e87-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="55e87-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="55e87-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="55e87-108">이 문서에서는 방법을 사용 하 여 인덱스 tooquery hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="55e87-109">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들고](search-what-is-an-index.md) [데이터로 채워야](search-what-is-data-import.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="55e87-110">배경 정보는 [Azure Search에서 전체 텍스트 검색의 작동 방식](search-lucene-query-architecture.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e87-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="55e87-111">Azure 검색 서비스의 쿼리 API 키 식별</span><span class="sxs-lookup"><span data-stu-id="55e87-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="55e87-112">Hello Azure 검색 REST API에 대해 모든 검색 작업의 핵심 구성 요소는 hello *api 키* 프로 비전 하는 hello 서비스에 대해 생성 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="55e87-113">유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="55e87-114">toofind toohello에 로그인 하려면 서비스의 api 키 [Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="55e87-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="55e87-115">Tooyour Azure 검색 서비스 블레이드로 이동</span><span class="sxs-lookup"><span data-stu-id="55e87-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="55e87-116">Hello "키" 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="55e87-117">서비스에는 *관리자 키* 및 *쿼리 키*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="55e87-118">기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="55e87-119">두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="55e87-120">프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="55e87-121">Hello 인덱스는 쿼리를 위해 쿼리 키 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="55e87-122">쿼리에 대 한 관리자 키도 사용할 수 있지만이 더 잘 hello를 다음과 같이 응용 프로그램 코드의 쿼리 키를 사용 해야 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="55e87-123">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="55e87-123">Formulate your query</span></span>
<span data-ttu-id="55e87-124">두 가지 너무[hello REST API를 사용 하 여 인덱스를 검색할](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="55e87-125">한 가지 방법은 tooissue HTTP POST 요청 쿼리 매개 변수를 hello 요청 본문의 JSON 개체에 정의 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="55e87-126">다른 방법으로 hello hello 요청 URL 내에서 쿼리 매개 변수를 정의 되어 있는 tooissue HTTP GET 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="55e87-127">게시물에 더 [제한을 완화](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello 크기의 GET 보다 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="55e87-128">따라서 GET을 사용하는 것이 보다 편리한 특별한 경우가 아니라면 게시를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="55e87-129">POST 및 GET, 해야 tooprovide 프로그램 *서비스 이름*, *인덱스 이름*, 및 적절 한 hello *API 버전* (hello 현재 API 버전은 `2016-09-01` hello 시 이 문서를 게시 하는)는 hello에 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="55e87-130">Hello에 대 한 GET, *쿼리 문자열* hello에 hello URL의 끝 hello 쿼리 매개 변수가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="55e87-131">Hello URL 형식에 대 한 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="55e87-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="55e87-132">hello는 POST 동일 hello는 대 한 하지만 hello 쿼리 문자열 매개 변수에서 api 버전만 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="55e87-133">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="55e87-133">Example Queries</span></span>
<span data-ttu-id="55e87-134">다음은 "호텔"이라는 인덱스에 대한 몇 가지 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="55e87-135">이러한 쿼리는 가져오기 및 게시 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="55e87-136">Hello 용어 '예산' hello 전체 인덱스 검색 하 고만 hello 반환 `hotelName` 필드:</span><span class="sxs-lookup"><span data-stu-id="55e87-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="55e87-137">적용 된 필터 toohello 인덱스 toofind 호텔 매일 밤 마다 $150 보다 저렴 하 고 hello 반환 `hotelId` 및 `description`:</span><span class="sxs-lookup"><span data-stu-id="55e87-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="55e87-138">검색 hello 전체 인덱스, 특정 필드에 따라 순서 (`lastRenovationDate`) hello 맨 위의 두 결과 가져오고 상태만 표시 내림차순으로 `hotelName` 및 `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="55e87-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="55e87-139">HTTP 요청 제출</span><span class="sxs-lookup"><span data-stu-id="55e87-139">Submit your HTTP request</span></span>
<span data-ttu-id="55e87-140">쿼리를 HTTP 요청 URL(가져오기의 경우) 또는 본문(게시의 경우)의 일부로 작성했으므로 요청 헤더를 정의하고 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="55e87-141">요청 및 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="55e87-141">Request and Request Headers</span></span>
<span data-ttu-id="55e87-142">가져오기에 두 개의 요청 헤더 또는 게시에 세 개의 요청 헤더를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="55e87-143">hello `api-key` 헤더 단계에서 찾은 I 위의 toohello 쿼리 키를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="55e87-144">Hello로 관리자 키를 사용할 수도 있습니다 `api-key` tooindexes 읽기 전용 액세스 및 문서 배타적으로 부여 하는 대로 쿼리 키를 사용 하는 헤더가 없지만 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="55e87-145">hello `Accept` 헤더 너무 설정 되어 있어야`application/json`합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="55e87-146">POST, hello `Content-Type` 헤더 너무 설정 해야`application/json`합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="55e87-147">인덱스에 대해 HTTP GET 요청 toosearch hello "호텔" hello hello 용어 "motel"에 대 한 검색 하는 간단한 쿼리를 사용 하 여 Azure 검색 REST API를 사용 하 여 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="55e87-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="55e87-148">다음 동일 hello은 쿼리 예에서는 HTTP POST를 사용 하 여이 시간:</span><span class="sxs-lookup"><span data-stu-id="55e87-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="55e87-149">성공적인 쿼리 요청은 상태 코드 됩니다 `200 OK` hello 검색 결과가 hello 응답 본문에서 JSON으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="55e87-150">어떤 hello 호텔"hello" 인덱스에 있는 샘플 데이터 hello 채워집니다 가정할 때, 쿼리 모양 위에 hello에 대 한 결과 다음과 같습니다 [데이터 가져오기를 사용 하 여 Azure 검색 REST API hello](search-import-data-rest-api.md) (JSON 쉽도록 서식이 지정 된 해당 hello 참고).</span><span class="sxs-lookup"><span data-stu-id="55e87-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="55e87-151">toolearn을 방문 하세요 hello "응답" 섹션의 [문서 검색](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e87-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="55e87-152">오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e87-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
