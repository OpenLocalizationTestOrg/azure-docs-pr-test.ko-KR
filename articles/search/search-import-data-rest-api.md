---
title: "aaa \"(REST API-Azure 검색) 데이터 업로드 | \"Microsoft Docs"
description: "Tooupload 데이터 tooan 인덱스에서 사용 하 여 Azure 검색 REST API를 hello 하는 방법에 대해 알아봅니다."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="8d791-103">REST API를 hello 업로드 데이터 tooAzure 사용 하 여 검색</span><span class="sxs-lookup"><span data-stu-id="8d791-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="8d791-104">개요</span><span class="sxs-lookup"><span data-stu-id="8d791-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="8d791-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8d791-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="8d791-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8d791-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="8d791-107">이 문서에서는 보여 어떻게 toouse hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport 데이터를 Azure 검색 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="8d791-108">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들어야](search-what-is-an-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="8d791-109">Hello REST API를 사용 하 여 인덱스로 순서 toopush 문서는 HTTP POST 요청 tooyour 인덱스의 URL 끝점을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="8d791-110">hello HTTP 요청 본문은 hello 문서 toobe 추가, 수정 또는 삭제를 포함 하는 JSON 개체의 hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="8d791-111">Azure 검색 서비스의 관리 API 키 식별</span><span class="sxs-lookup"><span data-stu-id="8d791-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="8d791-112">Hello REST API를 사용 하 여 서비스에 대해 HTTP 요청을 발급 하는 경우 *각* hello api 키 hello를 프로 비전 할 검색 서비스에 대해 생성 된 API 요청에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="8d791-113">유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="8d791-114">toofind toohello에 로그인 하려면 서비스의 api 키 [Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="8d791-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="8d791-115">Tooyour Azure 검색 서비스 블레이드로 이동</span><span class="sxs-lookup"><span data-stu-id="8d791-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="8d791-116">Hello에 "키" 아이콘을 클릭</span><span class="sxs-lookup"><span data-stu-id="8d791-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="8d791-117">서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="8d791-118">기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="8d791-119">두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="8d791-120">프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="8d791-121">인덱스에 데이터를 가져올 hello 용도로 사용할 수 있습니다 프로그램 주 또는 보조 관리자 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="8d791-122">인덱싱 동작 toouse 결정</span><span class="sxs-lookup"><span data-stu-id="8d791-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="8d791-123">Hello REST API를 사용할 때 JSON 요청 본문 tooyour Azure 검색 인덱스의 끝점 URL 인 HTTP POST 요청 발급할 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="8d791-124">HTTP 요청 본문에 hello JSON 개체는 단일 JSON 배열에 포함 됩니다 tooadd tooyour 인덱스 원하는 문서를 나타내는 JSON 개체가 포함 된 "value" 라는, 업데이트 또는 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="8d791-125">JSON 배열의 각 개체에 hello "value" 인덱싱된 문서 toobe를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="8d791-126">이러한 각 개체 hello 문서 키를 포함 하 고 원하는 hello 인덱싱 동작 (업로드, 병합, 삭제 등)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="8d791-127">Hello 아래의 선택한 작업 중 어느 것을 따라 특정 필드만 각 문서에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="8d791-128">설명</span><span class="sxs-lookup"><span data-stu-id="8d791-128">Description</span></span> | <span data-ttu-id="8d791-129">각 문서에 대해 필요한 필드</span><span class="sxs-lookup"><span data-stu-id="8d791-129">Necessary fields for each document</span></span> | <span data-ttu-id="8d791-130">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8d791-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="8d791-131">`upload` 동작은 비슷한 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="8d791-132">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="8d791-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="8d791-133">기존 문서를 업데이트/교체 hello 요청에 지정 되지 않은 모든 필드 갖게 되며 해당 필드가 너무 설정`null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="8d791-134">Hello 필드 tooa null이 아닌 값을 이전에 설정 된 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="8d791-135">업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="8d791-136">Hello 문서 hello 인덱스에 없는 경우 hello 병합 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="8d791-137">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="8d791-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="8d791-138">병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="8d791-139">여기에는 `Collection(Edm.String)`형식 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="8d791-140">예를 들어 경우 hello 문서는 필드가 `tags` 값으로 `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` 에 대 한 `tags`, hello의 최종 값 hello `tags` 필드가 `["economy", "pool"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="8d791-141">`["budget", "economy", "pool"]`이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="8d791-142">이 작업 처럼 동작 `merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="8d791-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="8d791-143">처럼 동작 하는 hello 문서가 없는 경우 `upload` 새 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="8d791-144">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="8d791-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="8d791-145">Hello 인덱스에서 hello 지정 된 문서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="8d791-146">키만</span><span class="sxs-lookup"><span data-stu-id="8d791-146">key only</span></span> |<span data-ttu-id="8d791-147">Hello 키 필드를 무시 것과 다른 모든 필드 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="8d791-148">문서에서 개별 필드 tooremove 사용 `merge` 대신 하 고 간단 하 게 hello 필드를 명시적으로 설정 toonull 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="8d791-149">HTTP 요청 및 요청 본문 생성</span><span class="sxs-lookup"><span data-stu-id="8d791-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="8d791-150">인덱스 작업에 대 한 hello 필요한 필드 값을 수집 했으므로 준비 tooconstruct hello 실제 HTTP 요청와 JSON 데이터를 요청 본문 tooimport 하세요.</span><span class="sxs-lookup"><span data-stu-id="8d791-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="8d791-151">요청 및 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="8d791-151">Request and Request Headers</span></span>
<span data-ttu-id="8d791-152">Hello URL에 해야 tooprovide 프로그램 서비스 이름, 인덱스 이름 ("호텔"이 경우에서)으로 hello 적절 한 API 버전 (hello 현재 API 버전은 `2016-09-01` 게시 하는이 문서는 hello 시)입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="8d791-153">Toodefine hello 해야 `Content-Type` 및 `api-key` 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="8d791-154">후자의 hello에 대 한 서비스의 관리자 키 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="8d791-155">요청 본문</span><span class="sxs-lookup"><span data-stu-id="8d791-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="8d791-156">이 경우 `upload`, `mergeOrUpload` 및 `delete`를 검색 작업으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="8d791-157">이 예제 "호텔" 인덱스는 문서 수로 채워진다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="8d791-158">어떻게 없는 toospecify hello 가능한 문서 필드를 모두 사용 하는 경우 유의 `mergeOrUpload` 어떻게 hello 문서 키만 지정 하 고 (`hotelId`) 사용 하는 경우 `delete`합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="8d791-159">또한, 이때 인덱싱 단일 요청에서 too1000 문서 (또는 16MB)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="8d791-160">HTTP 응답 코드 이해</span><span class="sxs-lookup"><span data-stu-id="8d791-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="8d791-161">200</span><span class="sxs-lookup"><span data-stu-id="8d791-161">200</span></span>
<span data-ttu-id="8d791-162">성공적인 인덱싱 요청을 제출한 후에 `200 OK`라는 상태 코드로 HTTP 응답을 받게됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="8d791-163">hello hello HTTP 응답의 JSON 본문은 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-163">hello JSON body of hello HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="8d791-164">207</span><span class="sxs-lookup"><span data-stu-id="8d791-164">207</span></span>
<span data-ttu-id="8d791-165">하나 이상의 항목이 성공적으로 인덱싱되지 않은 경우 상태 코드인 `207` 이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="8d791-166">hello hello HTTP 응답의 JSON 본문에는 hello 실패 한 문서에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="8d791-167">종종 즉, 해당 hello 부하에서 검색 서비스에 도달 함를 요청 하는 인덱스가 됩니다 tooreturn 지점 `503` 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="8d791-168">이 경우 다시 시도하기 전에 클라이언트 코드를 백오프하고 대기하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="8d791-169">이렇게 하면 hello 시스템 되므로 이후 요청이 성공할 hello 가능성이 증가 일부 시간 toorecover 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="8d791-170">사용자의 요청을 즉시 다시 시도 제한을 hello 상황을 연장만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="8d791-171">429</span><span class="sxs-lookup"><span data-stu-id="8d791-171">429</span></span>
<span data-ttu-id="8d791-172">상태 코드 `429` hello 인덱스 당 문서 수에 할당량이 초과 하는 경우 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="8d791-173">503</span><span class="sxs-lookup"><span data-stu-id="8d791-173">503</span></span>
<span data-ttu-id="8d791-174">상태 코드 `503` 경우 none hello 항목 hello 요청에 성공적으로 인덱싱된 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="8d791-175">이 오류 hello 시스템 사용량이 많아 지금 요청을 처리할 수 없습니다을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="8d791-176">이 경우 다시 시도하기 전에 클라이언트 코드를 백오프하고 대기하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="8d791-177">이렇게 하면 hello 시스템 되므로 이후 요청이 성공할 hello 가능성이 증가 일부 시간 toorecover 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="8d791-178">사용자의 요청을 즉시 다시 시도 제한을 hello 상황을 연장만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="8d791-179">문서 동작 및 성공/오류 응답에 대한 자세한 내용은 [문서 추가, 업데이트 또는 삭제](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d791-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="8d791-180">오류가 발생한 경우 반환될 수 있는 기타 HTTP 상태 코드에 대한 자세한 내용은 [HTTP 상태 코드(Azure 검색)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d791-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d791-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d791-181">Next steps</span></span>
<span data-ttu-id="8d791-182">Azure 검색 인덱스를 채울 후 준비 toostart 문서에 대 한 쿼리 toosearch 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d791-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="8d791-183">세부 정보는 [Azure 검색 인덱스 쿼리](search-query-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d791-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
