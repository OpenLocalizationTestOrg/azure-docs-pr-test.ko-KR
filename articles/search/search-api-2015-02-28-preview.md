---
title: "검색 서비스 REST API 버전 2015-02-28-preview aaaAzure | Microsoft Docs"
description: "Azure 검색 서비스 REST API 버전 2015-02-28-Preview에는 자연어 분석기 및 moreLikeThis 검색과 같은 실험적 기능이 포함되어 있습니다."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="3b1c9-103">Azure 검색 서비스 REST API: 버전 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="3b1c9-104">이 문서에 대 한 hello 참조 설명서는 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-105">이 미리 보기는 현재 일반 공급 버전 hello 확장 [api 버전 2015-02-28 =](https://msdn.microsoft.com/library/dn798935.aspx), hello 같은 실험적 기능을 제공 하 여:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="3b1c9-106">`moreLikeThis`쿼리 매개 변수 hello [문서 검색](#SearchDocs) API입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="3b1c9-107">다른 문서를 관련 tooanother 특정 문서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="3b1c9-108">몇 가지 추가 부분의 hello `2015-02-28-Preview` REST API에 별도로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="3b1c9-109">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-109">These include:</span></span>

* [<span data-ttu-id="3b1c9-110">점수 매기기 프로필</span><span class="sxs-lookup"><span data-stu-id="3b1c9-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="3b1c9-111">인덱서</span><span class="sxs-lookup"><span data-stu-id="3b1c9-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="3b1c9-112">Azure 검색 서비스는 여러 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="3b1c9-113">너무를 참조 하십시오[검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="3b1c9-114">이 문서의 API</span><span class="sxs-lookup"><span data-stu-id="3b1c9-114">APIs in this document</span></span>
<span data-ttu-id="3b1c9-115">Azure 검색 서비스 API는 API 작업을 위한 두 URL 구문, 즉 simple 및 OData(자세한 내용은 [OData(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) 를 참조하세요).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="3b1c9-116">hello 다음 목록은 hello 간단한 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="3b1c9-117">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-118">인덱스 업데이트</span><span class="sxs-lookup"><span data-stu-id="3b1c9-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-119">인덱스 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-120">인덱스 나열</span><span class="sxs-lookup"><span data-stu-id="3b1c9-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-121">인덱스 통계 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-122">테스트 분석기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-123">인덱스 삭제</span><span class="sxs-lookup"><span data-stu-id="3b1c9-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-124">인덱스 내에서 데이터 추가, 삭제 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="3b1c9-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-125">문서 검색</span><span class="sxs-lookup"><span data-stu-id="3b1c9-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-126">문서 조회</span><span class="sxs-lookup"><span data-stu-id="3b1c9-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="3b1c9-127">문서 수 계산</span><span class="sxs-lookup"><span data-stu-id="3b1c9-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="3b1c9-128">제안</span><span class="sxs-lookup"><span data-stu-id="3b1c9-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="3b1c9-129">인덱스 작업</span><span class="sxs-lookup"><span data-stu-id="3b1c9-129">Index Operations</span></span>
<span data-ttu-id="3b1c9-130">Azure 검색 서비스에서 간단한 HTTP 요청(POST, GET, PUT, DELETE)을 통해 지정된 인덱스 리소스에 대해 인덱스를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="3b1c9-131">인덱스 toocreate를 처음 게시 하면 hello 인덱스 스키마를 설명 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="3b1c9-132">hello 스키마 hello index, 해당 데이터 형식 및 수 수 사용 방법 (예를 들어 전체 텍스트 검색, 필터, 정렬 또는 패싯)의 hello 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="3b1c9-133">또한 점수 매기기 프로필, 확인 기 및 기타 특성 tooconfigure hello hello 인덱스의 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="3b1c9-134">hello 다음 예에서는 hello 설명 필드 두 언어로 정의 된 호텔 정보 검색에 사용 되는 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="3b1c9-135">Hello 필드 사용량 특성을 제어 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="3b1c9-136">예를 들어 hello `hotelId` hello 문서 키로 사용 됩니다 (`"key": true`) 및 전체 텍스트 검색에서 제외 되었습니다 (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="3b1c9-137">Hello 인덱스를 만든 후에 hello 인덱스를 채울 문서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="3b1c9-138">이 작업을 수행하는 다음 단계는 [문서 추가 또는 업데이트](#AddOrUpdateDocuments) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="3b1c9-139">Azure 검색의 한 비디오 지침은 tooindexing, 참조 hello [Azure 검색에 대 한 채널 9의 Cloud Cover 에피소드](http://go.microsoft.com/fwlink/p/?LinkId=511509)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="3b1c9-140">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-140">Create Index</span></span>
<span data-ttu-id="3b1c9-141">인덱스는 hello 기본 방법은 구성 하 고 Azure 검색에서 문서를 검색, 비슷한 toohow 테이블은 데이터베이스에서 레코드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="3b1c9-142">각 인덱스에 모든 toohello 인덱스 스키마 (필드 이름, 데이터 형식 및 속성)을 준수 하지만 기타 검색 동작을 정의 하는 추가 구문 (확인 기, 점수 매기기 프로필 및 CORS 옵션)도 지정 하는 문서 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="3b1c9-143">HTTP POST 또는 PUT 요청을 사용하여 Azure 검색 서비스 내에서 새 인덱스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="3b1c9-144">hello hello 요청 본문은 hello 인덱스 및 구성 정보를 지정 하는 JSON 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3b1c9-145">또는 PUT을 사용 하 여 하 고 hello URI에서 hello 인덱스 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="3b1c9-146">Hello 인덱스가 없는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="3b1c9-147">인덱스를 만들면 hello 문서 저장 및 검색 작업에 사용의 hello 구조를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="3b1c9-148">채우는 hello 인덱스는 별도 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="3b1c9-149">이 단계에는 [인덱서](https://msdn.microsoft.com/library/azure/mt183328.aspx)(지원되는 데이터 원본에 사용 가능)를 사용하거나 [문서 추가, 업데이트 또는 삭제](https://msdn.microsoft.com/library/azure/dn798930.aspx) 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="3b1c9-150">hello 반전 된 인덱스는 hello 문서를 게시 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="3b1c9-151">**참고**: 가격 책정 계층으로 사용할 수 있는 인덱스의 최대 수 hello 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="3b1c9-152">hello 무료 서비스 too3 인덱스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="3b1c9-153">표준 서비스에서는 검색 서비스당 인덱스 50개를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="3b1c9-154">자세한 내용은 [한도 및 제약 조건](http://msdn.microsoft.com/library/azure/dn798934.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="3b1c9-155">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-155">**Request**</span></span>

<span data-ttu-id="3b1c9-156">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3b1c9-157">hello **Create Index** POST 또는 PUT 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="3b1c9-158">POST를 사용할 때는 hello 인덱스 스키마 정의와 함께 hello 요청 본문에 인덱스 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="3b1c9-159">PUT을 사용 hello 인덱스 이름은 hello URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="3b1c9-160">Hello 인덱스가 존재 하지 않는 경우 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="3b1c9-161">이미 있는 경우 업데이트 된 toohello 새 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="3b1c9-162">hello 인덱스 이름은 소문자 여야, 문자 또는 숫자로 시작, 없습니다 슬래시나 마침표를을 있어야 128 자 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="3b1c9-163">Hello 인덱스 이름은 문자 또는 숫자로 시작 된 후 hello 나머지 hello 이름 포함할 수 있습니다는 문자, 숫자 및 대시만 hello 대시를 연속 되지 않은 상태로.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="3b1c9-164">hello `api-version` 가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-164">hello `api-version` is required.</span></span> <span data-ttu-id="3b1c9-165">사용 가능한 버전 목록은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="3b1c9-166">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-166">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-167">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-168">`Content-Type`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-168">`Content-Type`: Required.</span></span> <span data-ttu-id="3b1c9-169">너무 설정 합니다.`application/json`</span><span class="sxs-lookup"><span data-stu-id="3b1c9-169">Set this too`application/json`</span></span>
* <span data-ttu-id="3b1c9-170">`api-key`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-170">`api-key`: Required.</span></span> <span data-ttu-id="3b1c9-171">hello `api-key` 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3b1c9-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="3b1c9-172">hello 요청 tooyour 검색 서비스를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-173">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-174">hello **Create Index** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-175">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-176">두 hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-177">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-178"><a name="RequestData"></a>
**요청 본문 구문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="3b1c9-179">이 인덱스에 공급할 문서 내의 데이터 필드의 hello 목록을 포함 하는 스키마 정의 포함 하는 hello hello 요청 본문, 점수 매기기 프로필 하는 선택적인 목록 뿐만 아니라 데이터 형식, 특성을 포함 하는 문서에 사용 되는 tooscore 됩니다. 쿼리 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="3b1c9-180">POST 요청에 대 한 이름을 지정 해야 hello 인덱스 hello 요청 본문에 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="3b1c9-181">있습니다 하나의 키 필드는 hello 인덱스의 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="3b1c9-182">문자열 필드 toobe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-182">It has toobe a string field.</span></span> <span data-ttu-id="3b1c9-183">이 필드는 hello hello 인덱스 내에 저장 된 각 문서에 대 한 고유 식별자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="3b1c9-184">인덱스의 주요 부분 hello hello 다음과를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="3b1c9-185">`fields` : 이름, 데이터 형식 및 해당 필드에 대해 허용되는 작업을 정의하는 속성을 포함하여 이 인덱스에 공급할 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="3b1c9-186">`suggesters` : 자동 완성 또는 미리 입력 쿼리에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="3b1c9-187">`scoringProfiles` : 사용자 지정 검색 점수 순위에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="3b1c9-188">자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="3b1c9-189">`analyzers``charFilters`, `tokenizers`, `tokenFilters` toodefine 인덱싱/검색 가능한 토큰으로 문서/쿼리는 구분 하는 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="3b1c9-190">자세한 내용은 [Azure 검색의 분석](https://aka.ms//azsanalysis) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="3b1c9-191">`defaultScoringProfile`toooverwrite hello 기본 점수 매기기 동작을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="3b1c9-192">`corsOptions`인덱스에 대 한 tooallow 크로스-원본 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="3b1c9-193">hello hello 요청 페이로드 구조를 지정 하는 것에 대 한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="3b1c9-194">이 항목에서 샘플 요청이 추가로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="3b1c9-195">**인덱스 특성**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-195">**Index Attributes**</span></span>

<span data-ttu-id="3b1c9-196">hello 다음 특성을 설정할 인덱스를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="3b1c9-197">점수 매기기 및 점수 매기기 프로필에 대한 자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="3b1c9-198">`name`세트 hello hello 필드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="3b1c9-199">`type`세트 hello hello 필드에 대 한 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="3b1c9-200">`searchable`-표시 hello 필드 전체 텍스트 검색 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="3b1c9-201">이렇게 표시된 필드의 경우 인덱싱 중에 단어 분리 등의 분석이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="3b1c9-202">설정 하는 경우는 `searchable` "sunny day"와 같은 필드 tooa 값을 내부적으로 됩니다 "sunny"와 "일" hello 개별 토큰으로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="3b1c9-203">따라서 이러한 용어에 대한 전체 텍스트 검색을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="3b1c9-204">형식이 `Edm.String` 또는 `Collection(Edm.String)`인 필드는 기본적으로 `searchable`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="3b1c9-205">다른 형식의 필드는 `searchable`로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="3b1c9-206">**참고**: `searchable` 필드 Azure 검색은 전체 텍스트 검색에 대 한 hello 필드 값의 추가 토큰화 된 버전을 저장 하므로 인덱스에서 추가적인 공간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="3b1c9-207">Toosave 공간에 원하는 인덱스 하 고 검색에 포함 하는 필드 toobe 필요 하지 않은 설정, `searchable` 너무`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="3b1c9-208">`filterable`-에서 참조 하는 hello 필드 toobe 허용 `$filter` 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="3b1c9-209">`filterable`은(는) 문자열 처리 방법에서 `searchable`와(과) 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="3b1c9-210">형식이 `Edm.String` 또는 `Collection(Edm.String)`이며 `filterable`인 필드의 경우 단어 분리가 수행되지 않으므로 정확하게 일치하는 항목만 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="3b1c9-211">예를 들어, 이러한 필드를 설정 하면 `f` 너무 "sunny day" `$filter=f eq 'sunny'` 일치 하는 항목을 찾을 수 있지만 `$filter=f eq 'sunny day'` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="3b1c9-212">기본적으로 모든 필드는 `filterable` 로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="3b1c9-213">`sortable`-기본적으로 hello 시스템 설정, 결과 정렬 하지만 대부분의 사용자가 hello 문서의 필드에 의해 toosort 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="3b1c9-214">형식이 `Collection(Edm.String)`인 필드는 `sortable`로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="3b1c9-215">기타 모든 필드는 기본적으로 `sortable` 로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="3b1c9-216">`facetable` - 일반적으로 범주별 적중 횟수를 포함하는 검색 결과 표시에 사용됩니다. 디지털 카메라를 검색한 다음 브랜드, 메가픽셀, 가격 등을 기준으로 적중 항목을 표시하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="3b1c9-217">형식이 `Edm.GeographyPoint`인 필드에는 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="3b1c9-218">기타 모든 필드는 기본적으로 `facetable` 로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="3b1c9-219">**참고**: `filterable`, `sortable` 또는 `facetable`인 `Edm.String` 형식 필드의 최대 길이는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="3b1c9-220">이 이러한 필드는 단일 검색 용어로 처리 되는데 Azure 검색에서 용어의 hello 최대 길이 32KB 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="3b1c9-221">Tooexplicitly 할 toostore 단일 문자열 필드에 이보다 많은 텍스트를 해야 하는 경우 설정 `filterable`, `sortable`, 및 `facetable` 너무`false` 인덱스 정의의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="3b1c9-222">**참고**: 특성이 너무 설정 없음 hello 위의 필드에 있으면`true` (`searchable`, `filterable`, `sortable`, 또는`facetable`) hello 필드는 hello 반전 된 인덱스에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="3b1c9-223">쿼리에서 사용되지는 않지만 검색 결과에는 필요한 필드의 경우 이 옵션을 사용하면 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="3b1c9-224">이러한 필드를 제외 하 고 hello 인덱스에서 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="3b1c9-225">`key`-부호 hello 필드 hello 인덱스 내의 문서에 대 한 고유 식별자를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="3b1c9-226">Hello로 정확히 하나의 필드를 선택 해야 합니다. `key` 필드가 형식 이어야 합니다 `Edm.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="3b1c9-227">키 필드는 hello 통해 직접 문서를 사용 하는 toolook 수 [조회 API](#LookupAPI)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="3b1c9-228">`retrievable`-Hello 필드는 검색 결과에 반환 될 수 있는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="3b1c9-229">정렬 또는 점수 매기기 메커니즘은 필터로 toouse 필드 (예를 들어, 여백)을 원하는 하지만 hello 필드 toobe 표시 toohello 최종 사용자를 원하지 않는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="3b1c9-230">`true` for `key` 로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="3b1c9-231">`analyzer`-설정 검색 시간 및 인덱싱 단계에서 hello 필드에 대 한 hello 분석기 toouse의 이름을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="3b1c9-232">값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3b1c9-233">이 옵션은 `searchable` 필드에만 사용할 수 있으며 `searchAnalyzer` 또는 `indexAnalyzer`와 함께 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="3b1c9-234">Hello 분석기를 선택한 후에 hello 필드에 대 한 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="3b1c9-235">`searchAnalyzer`세트 hello hello 필드에 대 한 검색 시 사용 하는 hello 분석기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="3b1c9-236">값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3b1c9-237">이 옵션은 `searchable` 필드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="3b1c9-238">와 함께 설정 되어야 `indexAnalyzer` hello와 함께 설정할 수 없습니다 및 `analyzer` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="3b1c9-239">이 분석기는 기존 필드에서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="3b1c9-240">`indexAnalyzer`세트 hello hello 필드에 대 한 인덱싱 단계에서 사용 되는 hello 분석기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="3b1c9-241">값 집합을 허용 하는 hello에 대 한 참조 [분석기](https://msdn.microsoft.com/library/mt605304.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3b1c9-242">이 옵션은 `searchable` 필드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="3b1c9-243">와 함께 설정 되어야 `searchAnalyzer` hello와 함께 설정할 수 없습니다 및 `analyzer` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="3b1c9-244">Hello 분석기를 선택한 후에 hello 필드에 대 한 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="3b1c9-245">`suggesters`집합에는 검색 모드 및 제안에 대 한 hello 내용의 hello 소스 필드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="3b1c9-246">자세한 내용은 [확인기](#Suggesters) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="3b1c9-247">`scoringProfiles` - 검색 결과에서 더 위쪽에 표시할 항목을 제어할 수 있는 사용자 지정 점수 매기기 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="3b1c9-248">점수 매기기 프로필은 필드 가중치와 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="3b1c9-249">참조 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 점수 매기기 프로필에서 사용 되는 hello 특성에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="3b1c9-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**언어 지원**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="3b1c9-251">검색 가능 필드에서는 대개 단어 분리, 텍스트 정규화, 용어 필터링 등을 포함하는 분석이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="3b1c9-252">기본적으로 Azure 검색의 검색 가능 필드 hello로 분석 [Apache Lucene 표준 분석기](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) 요소 뒤에 텍스트를 나눕니다 하는["유니코드 텍스트 구분"](http://unicode.org/reports/tr29/) 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="3b1c9-253">또한 표준 분석기 hello 모든 문자 tootheir 소문자 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="3b1c9-254">인덱싱된 문서와 검색 용어는 인덱싱 및 쿼리 처리 중 hello 분석을 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="3b1c9-255">Azure 검색은 다양한 언어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="3b1c9-256">각 언어를 사용하려면 지정된 언어의 특성을 고려할 수 있는 비표준 텍스트 분석기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="3b1c9-257">Azure 검색에서는 다음 두 가지 유형의 분석기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="3b1c9-258">Lucene에서 지원하는 35개의 분석기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="3b1c9-259">Office 및 Bing에서 사용되는 Microsoft 소유 자연어 처리 기술로 지원되는 50개의 분석기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="3b1c9-260">일부 개발자 들이 선호할 수 hello Lucene의 더 친숙 한, 단순, 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="3b1c9-261">Lucene 분석기는 속도가 더 하지만 hello Microsoft 분석기 보조 정리 하는 등의 기능이 고급, 단어 (독일어, 덴마크어, 네덜란드어, 스웨덴어, 노르웨이어, 에스토니아어, 완료, 헝가리어, 슬로바키아어과 같은 언어)에서 decompounding 및 엔터티 인식 (Url 전자 메일, 날짜, 숫자)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="3b1c9-262">가능 하면 한 더 적합할 두 hello Microsoft 및 Lucene 분석기 toodecide의 비교를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="3b1c9-263">***비교 방법***</span><span class="sxs-lookup"><span data-stu-id="3b1c9-263">***How they compare***</span></span>

<span data-ttu-id="3b1c9-264">영어에 대 한 hello Lucene 분석기 hello 표준 분석기를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="3b1c9-265">이 분석기는 단어에서 소유격(후행 's)을 제거하고, [Porter 형태소 분석 알고리즘](http://tartarus.org/~martin/PorterStemmer/)에 따라 형태소 분석을 적용하며, 영어의 [중지 단어](http://en.wikipedia.org/wiki/Stop_words)를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="3b1c9-266">반면 hello Microsoft 분석기 형태소 분석 하는 대신 보조 정리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="3b1c9-267">즉, 어형이 변화되고 불규칙한 단어 형태 관련 검색 결과에서 더 정확한 결과로 처리할 수 있습니다.(자세한 내용은 [Azure 검색 MVA 프레젠테이션](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) 의 모듈 7 보기)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="3b1c9-268">Microsoft 분석기를 사용 하 여 인덱싱 Lucene 동등한 hello 언어에 따라 보다 느린 두 toothree 시간이 평균적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="3b1c9-269">검색 성능은 평균 크기 쿼리에 크게 영향을 받지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="3b1c9-270">***구성***</span><span class="sxs-lookup"><span data-stu-id="3b1c9-270">***Configuration***</span></span>

<span data-ttu-id="3b1c9-271">Hello 인덱스 정의의 각 필드에 대 한 hello를 설정할 수 있습니다 `analyzer` 언어 및 공급 업체를 지정 하는 속성 tooan 분석기 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="3b1c9-272">hello 인덱싱 및 해당 필드에 대 한 검색 하는 경우 동일한 분석기 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="3b1c9-273">예를 들어 영어, 프랑스어, 스페인어 호텔 설명 나란히 hello에 존재 하는 대 한 개별 필드가 점이 같은 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="3b1c9-274">사용 하 여 hello ['searchFields' 쿼리 매개 변수](#SearchQueryParameters) toospecify 쿼리에 대해 어떤 언어별 필드 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="3b1c9-275">Hello를 포함 하는 쿼리 예제를 검토할 수 있습니다 `analyzer` 속성 [문서 검색](#SearchDocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="3b1c9-276">***분석기 목록***</span><span class="sxs-lookup"><span data-stu-id="3b1c9-276">***Analyzer list***</span></span>

<span data-ttu-id="3b1c9-277">아래에 Microsoft 및 Lucene 분석기 이름과 함께 지원 되는 언어의 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="3b1c9-278">언어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-278">Language</span></span></th>
        <th><span data-ttu-id="3b1c9-279">Microsoft 분석기 이름</span><span class="sxs-lookup"><span data-stu-id="3b1c9-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="3b1c9-280">Lucene 분석기 이름</span><span class="sxs-lookup"><span data-stu-id="3b1c9-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-281">아랍어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-281">Arabic</span></span></td>
        <td><span data-ttu-id="3b1c9-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-284">아르메니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="3b1c9-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-286">벵골어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-286">Bangla</span></span></td>
        <td><span data-ttu-id="3b1c9-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="3b1c9-288">바스크어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="3b1c9-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="3b1c9-290">불가리아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="3b1c9-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="3b1c9-293">카탈로니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-293">Catalan</span></span></td>
        <td><span data-ttu-id="3b1c9-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-296">중국어 간체</span><span class="sxs-lookup"><span data-stu-id="3b1c9-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="3b1c9-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-299">중국어 번체</span><span class="sxs-lookup"><span data-stu-id="3b1c9-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="3b1c9-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="3b1c9-302">크로아티아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-302">Croatian</span></span></td>
        <td><span data-ttu-id="3b1c9-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-304">체코어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-304">Czech</span></span></td>
        <td><span data-ttu-id="3b1c9-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3b1c9-307">덴마크어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-307">Danish</span></span></td>
        <td><span data-ttu-id="3b1c9-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3b1c9-310">네덜란드어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-310">Dutch</span></span></td>
        <td><span data-ttu-id="3b1c9-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="3b1c9-313">영어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-313">English</span></span></td>        
        <td><span data-ttu-id="3b1c9-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-316">에스토니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-316">Estonian</span></span></td>
        <td><span data-ttu-id="3b1c9-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-318">핀란드어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-318">Finnish</span></span></td>
        <td><span data-ttu-id="3b1c9-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3b1c9-321">프랑스어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-321">French</span></span></td>
        <td><span data-ttu-id="3b1c9-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-324">갈리시아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="3b1c9-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-326">독일어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-326">German</span></span></td>
        <td><span data-ttu-id="3b1c9-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-329">그리스어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-329">Greek</span></span></td>
        <td><span data-ttu-id="3b1c9-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-332">구자라트어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-332">Gujarati</span></span></td>
        <td><span data-ttu-id="3b1c9-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-334">히브리어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-334">Hebrew</span></span></td>
        <td><span data-ttu-id="3b1c9-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-336">힌디어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-336">Hindi</span></span></td>
        <td><span data-ttu-id="3b1c9-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-339">헝가리어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="3b1c9-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-342">아이슬란드어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-342">Icelandic</span></span></td>
        <td><span data-ttu-id="3b1c9-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-344">인도네시아어(공용어)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="3b1c9-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-347">아일랜드어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="3b1c9-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-349">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-349">Italian</span></span></td>
        <td><span data-ttu-id="3b1c9-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-352">일본어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-352">Japanese</span></span></td>
        <td><span data-ttu-id="3b1c9-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-355">카나다어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-355">Kannada</span></span></td>
        <td><span data-ttu-id="3b1c9-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-357">한국어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-357">Korean</span></span></td>
        <td><span data-ttu-id="3b1c9-358">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-360">라트비아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-360">Latvian</span></span></td>        
        <td><span data-ttu-id="3b1c9-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-363">리투아니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="3b1c9-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-365">말라얄람어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-365">Malayalam</span></span></td>
        <td><span data-ttu-id="3b1c9-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-367">말레이어(라틴 문자)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="3b1c9-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-369">마라티어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-369">Marathi</span></span></td>
        <td><span data-ttu-id="3b1c9-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-371">노르웨이어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-371">Norwegian</span></span></td>
        <td><span data-ttu-id="3b1c9-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="3b1c9-374">페르시아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="3b1c9-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-376">폴란드어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-376">Polish</span></span></td>
        <td><span data-ttu-id="3b1c9-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-379">포르투갈어(브라질)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="3b1c9-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-382">포르투갈어(포르투갈)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="3b1c9-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="3b1c9-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-385">펀잡어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-385">Punjabi</span></span></td>
        <td><span data-ttu-id="3b1c9-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-387">루마니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-387">Romanian</span></span></td>
        <td><span data-ttu-id="3b1c9-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-390">러시아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-390">Russian</span></span></td>
        <td><span data-ttu-id="3b1c9-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-393">세르비아어(키릴자모)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="3b1c9-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-395">세르비아어(라틴 문자)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="3b1c9-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-397">슬로바키아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-397">Slovak</span></span></td>
        <td><span data-ttu-id="3b1c9-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-399">슬로베니아어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-399">Slovenian</span></span></td>
        <td><span data-ttu-id="3b1c9-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-401">스페인어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-401">Spanish</span></span></td>
        <td><span data-ttu-id="3b1c9-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-404">스웨덴어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-404">Swedish</span></span></td>
        <td><span data-ttu-id="3b1c9-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="3b1c9-407">타밀어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-407">Tamil</span></span></td>
        <td><span data-ttu-id="3b1c9-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-409">텔루구어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-409">Telugu</span></span></td>
        <td><span data-ttu-id="3b1c9-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-411">태국어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-411">Thai</span></span></td>
        <td><span data-ttu-id="3b1c9-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-414">터키어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-414">Turkish</span></span></td>
        <td><span data-ttu-id="3b1c9-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="3b1c9-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-417">우크라이나어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="3b1c9-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-419">우르두어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-419">Urdu</span></span></td>
        <td><span data-ttu-id="3b1c9-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-421">베트남어</span><span class="sxs-lookup"><span data-stu-id="3b1c9-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="3b1c9-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3b1c9-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="3b1c9-423">Azure 검색에서는 추가적으로 언어에 관계없는 분석기 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="3b1c9-424">표준 ASCII 접기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="3b1c9-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="3b1c9-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="3b1c9-426">유니코드 텍스트 구분(표준 토크나이저)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="3b1c9-427">ASCII 접기 필터-유니코드 문자를 해당 ASCII 문자로 toohello 처음 127 ASCII 문자 집합에 속하지 않는 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="3b1c9-428">분음 부호(악센트)를 제거하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="3b1c9-429">이름에 <i>lucene</i> 주석이 포함된 모든 분석기는 [Apache Lucene 언어 분석기](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html)를 통해 구동됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="3b1c9-430">Hello ASCII 접기 필터에 대 한 자세한 정보를 찾을 수 [여기](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="3b1c9-431">**확인기**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-431">**Suggesters**</span></span>

<span data-ttu-id="3b1c9-432">A `suggester` 검색에서 자동 완성 사용 되는 toosupport 인덱스의 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="3b1c9-433">일반적으로 부분 검색 문자열이 toohello 보내집니다 [제안 API](#Suggestions) hello 사용자가 검색 쿼리를 입력 하 고 hello API는 제안된 구 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="3b1c9-434">Hello 인덱스에서 정의 하는 확인 기 필드는 사용 되는 toobuild hello 미리 입력 검색 용어를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="3b1c9-435">구성 세부 정보는 [확인기](#Suggesters) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="3b1c9-436">**점수 매기기 프로필**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-436">**Scoring profiles**</span></span>

<span data-ttu-id="3b1c9-437">A `scoringProfile` 사용자 지정 점수 매기기 동작을 제어할 수 있는 상위 hello 검색 결과에 표시 되는 항목을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="3b1c9-438">점수 매기기 프로필은 필드 가중치와 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="3b1c9-439">toouse hello 쿼리 문자열에서 이름으로 프로필을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="3b1c9-440">점수 매기기 프로필 기본 결과 집합에 있는 모든 항목에 대 한 검색 점수 hello 장면 toocompute 뒤 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="3b1c9-441">Hello 내부 명명 되지 않은 점수 매기기 프로필을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="3b1c9-442">또는 설정할 `defaultScoringProfile` toouse hello 쿼리 문자열에서 사용자 지정 프로필을 지정 하지 않으면 때마다 호출 됩니다. hello 기본값으로 사용자 지정 프로필.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="3b1c9-443">참조 [tooa 검색 인덱스 (Azure 검색 서비스 REST API) 프로필 추가 점수 매기기](search-api-scoring-profiles-2015-02-28-preview.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="3b1c9-444">**CORS 옵션**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-444">**CORS Options**</span></span>

<span data-ttu-id="3b1c9-445">클라이언트 쪽 Javascript hello 브라우저 모든 교차 원본 요청 하면 이후 기본적으로 Api를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="3b1c9-446">CORS (크로스-원본 자원 공유)를 사용 하도록 설정 하 여 hello 설정 `corsOptions` 특성 tooallow 크로스-원본 쿼리가 tooyour 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="3b1c9-447">보안상 쿼리 API에서만 CORS가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="3b1c9-448">CORS에 대해 hello 다음 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="3b1c9-449">`allowedOrigins`(필수): 액세스 tooyour 인덱스 부여 되는 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="3b1c9-450">이 허용 된 tooquery 인덱스 (올바른 API 키 hello를 제공 한다고 가정할 경우)이 원본에서 제공 하는 모든 Javascript 코드 수 있다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="3b1c9-451">각 원본은 일반적으로 hello 폼의 `protocol://fully-qualified-domain-name:port` hello 포트는 생략 되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="3b1c9-452">자세한 내용은 [이 문서](http://go.microsoft.com/fwlink/?LinkId=330822) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="3b1c9-453">Tooallow 액세스 tooall origin 포함 `*` hello에 단일 항목으로 `allowedOrigins` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="3b1c9-454">**프로덕션 검색 서비스에서는 이러한 방식을 사용하지 않는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="3b1c9-455">개발 또는 디버깅용으로는 이 기능이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="3b1c9-456">`maxAgeInSeconds`(선택 사항): 브라우저에서는이 값 toodetermine hello 기간 (초) toocache CORS 실행 전 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="3b1c9-457">이 값은 음수가 아닌 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-457">This must be a non-negative integer.</span></span> <span data-ttu-id="3b1c9-458">이 값은 더 나은 성능은 hello hello 더 큰 하지만 hello 긴 좋아지지만 CORS 정책 변경 내용 tootake 효과입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="3b1c9-459">이 값을 설정하지 않으면 기본 기간인 5분이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="3b1c9-460"><a name="CreateUpdateIndexExample"></a>
**요청 본문 예제**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="3b1c9-461">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-461">**Response**</span></span>

<span data-ttu-id="3b1c9-462">요청이 성공적으로 실행되면 “201 생성됨”이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="3b1c9-463">기본적으로 hello 응답 본문에는 생성 된 hello 인덱스 정의 대 한 JSON hello를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="3b1c9-464">경우 hello `Prefer` 요청 헤더가 너무 설정 되어`return=minimal`, hello 응답 본문은 비어 있게 및 hello 성공 상태 코드 됩니다 "204 콘텐츠 없음" 대신 "201 생성 됨"입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="3b1c9-465">PUT 또는 POST 사용된 toocreate hello 인덱스 했는지 여부에 관계 없이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="3b1c9-466">**설명**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-466">**Remarks**</span></span>

<span data-ttu-id="3b1c9-467">현재는 인덱스 스키마 업데이트가 제한적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="3b1c9-468">필드 형식을 변경하는 등 인덱싱을 다시 수행해야 하는 모든 스키마 업데이트는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="3b1c9-469">기존 필드를 변경 하거나 삭제할 수 없습니다, 없지만 새 필드는 언제 든 지 기존 인덱스 tooan 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="3b1c9-470">새 필드를 추가 하는 경우 모든 기존 문서 hello 인덱스에서 해당 필드에 대해 null 값을 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="3b1c9-471">새 문서 toohello 인덱스 추가 될 때까지 추가 저장 공간이 없는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="3b1c9-472">확인기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-472">Suggesters</span></span>
<span data-ttu-id="3b1c9-473">Azure 검색의 hello 제안 기능은는 검색 상자에 입력 하는 응답 toopartial 문자열 입력에 잠재적 검색 용어 목록을 제공 하는 미리 입력 또는 자동 완성 쿼리 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="3b1c9-474">상용 웹 검색 엔진 사용 시 쿼리 제안을 보았을 것입니다. Bing에 ".NET"를 입력하면 ".NET 4.5", ".NET Framework 3.5" 등에 대한 용어 목록이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="3b1c9-475">Hello 검색 서비스 REST API를 사용할 때 사용자 지정 Azure 검색 응용 프로그램에서 제안을 구현 hello 다음을 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="3b1c9-476">추가 하 여 제안을 사용 하도록 설정 된 **확인 기** 제공 hello 이름, 검색 모드 및 필드 목록이을 미리 입력 하려면 인덱스에 생성이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="3b1c9-477">예를 들어 "시애틀"에 발생 합니다 "sea"라는 부분 검색 문자열을 입력 하 여 원본 필드로 "cityName"을 지정 하면 "Seaside" 및 "Seatac" (세 개 모두가 실제 도시 이름임)으로 제공 쿼리 제안 toohello 사용자.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="3b1c9-478">Hello를 호출 하 여 제안을 호출 [제안 API](#Suggestions) 응용 프로그램 코드에서.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="3b1c9-479">일반적으로 hello 사용자가 검색 쿼리를 입력 하 고이 API는 제안된 구 집합을 반환 하는 동안 부분 검색 문자열이 toohello 서비스에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="3b1c9-480">이 문서에서는 설명 방법을 tooconfigure는 **확인 기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="3b1c9-481">Hello도 검토 해야 [제안 API](#Suggestions) 는 확인 기 사용 되는 방법에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="3b1c9-482">**사용 현황**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-482">**Usage**</span></span>

<span data-ttu-id="3b1c9-483">`Suggesters`hello 인덱스에 생성 되 고 사용 되는 경우에 가장 효과적 toosuggest 특정 한 용어나 구보다는 대신에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="3b1c9-484">hello 적합 한 필드는 제목, 이름 및 항목을 식별할 수 있는 비교적 짧은 기타 구입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="3b1c9-485">반면 범주/태그 등의 반복 필드나 설명/주석 등의 매우 긴 필드는 확인기를 사용하기에 덜 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="3b1c9-486">Hello 인덱스 정의의 일환으로, 단일 확인 기 toohello를 추가할 수 있습니다 `suggesters` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="3b1c9-487">확인 기를 정의 하는 속성에는 hello 다음과를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="3b1c9-488">`name`: hello 이름 hello 확인 기입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="3b1c9-489">Hello 확인 기 이름을 hello를 사용 하 여 hello를 호출할 때 `suggest` API입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="3b1c9-490">`searchMode`: 제안 가능한 구를 사용 하는 전략 toosearch hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="3b1c9-491">hello 현재 지원 되는 유일한 모드는 `analyzingInfixMatching`, 구 또는 문장 hello 중간 hello 시작 부분에서 유연 일치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="3b1c9-492">`sourceFields`: 제안에 대 한 hello 내용의 hello 소스 있는 하나 이상의 필드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="3b1c9-493">형식이 `Edm.String` 및 `Collection(Edm.String)`인 필드만 제안 원본으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="3b1c9-494">또한 사용자 지정 언어 분석기가 설정되지 않은 필드만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="3b1c9-495">**확인기 예제**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-495">**Suggester Example**</span></span>

<span data-ttu-id="3b1c9-496">확인 기는 hello 인덱스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-496">A suggester is part of hello index.</span></span> <span data-ttu-id="3b1c9-497">하나의 확인 기 hello에 존재할 수 `suggesters` hello와 함께 hello 최신 버전의 컬렉션 필드 컬렉션 및 `scoringProfiles`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="3b1c9-498">Azure 검색의 hello 공개 미리 보기 버전을 사용 하는 경우 `suggesters` 했던 이전 부울 속성을 바꿉니다 (`"suggestions": false`) (3 ~ 25 자) 사이의 짧은 문자열에 대 한만 접두사 제안을 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="3b1c9-499">를 대체할 `suggesters`, 지원 또는 필드 콘텐츠의 hello 중간 hello 시작 부분에서 반환 될 확률이 높아집니다 검색 문자열에 일치 하는 용어를 발견 하는 일치 하는 중 위 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="3b1c9-500">Hello 일반 공급 릴리스 이상에서는 이것이 이제 hello 제안 API hello 으로만 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="3b1c9-501">이전 hello `suggestions` 에 도입 된 속성 `api-version=2014-07-31-Preview` toowork 해당 버전에서는 계속 하지만 hello에서는 작동 하지 않습니다 `2015-02-28` 또는 이후 버전의 Azure 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="3b1c9-502">인덱스 업데이트</span><span class="sxs-lookup"><span data-stu-id="3b1c9-502">Update Index</span></span>
<span data-ttu-id="3b1c9-503">HTTP PUT 요청을 사용하여 Azure 검색 내에서 기존 인덱스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="3b1c9-504">새 필드 toohello 기존 스키마 추가, CORS 옵션 수정 및 점수 매기기 프로필 수정 업데이트 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="3b1c9-505">자세한 내용은 [점수 매기기 프로필 추가](https://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="3b1c9-506">Hello 요청 URI에 hello 인덱스 tooupdate의 hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3b1c9-507">**중요:** 인덱스 스키마 업데이트에 대 한 지원은 제한 toooperations hello 검색 인덱스를 다시 작성 하는 설정이 필요 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="3b1c9-508">필드 형식을 변경하는 등 인덱싱을 다시 수행해야 하는 모든 스키마 업데이트는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="3b1c9-509">기존 필드를 변경하거나 삭제할 수는 없지만 언제든지 새 필드를 추가할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="3b1c9-510">hello에 마찬가지 너무`suggesters`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="3b1c9-511">Hello 시간 hello 필드에서 tooa 기가 추가 되지만에서 필드를 제거할 수 없는 새 필드를 추가할 수 `suggesters` 너무 추가할 수 없습니다 기존 필드`suggesters`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="3b1c9-512">새 필드 tooan 인덱스에 추가할 때는 hello 인덱스의 모든 기존 문서는 해당 필드에 대해 null 값을 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="3b1c9-513">새 문서 toohello 인덱스 추가 될 때까지 추가 저장 공간이 없는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="3b1c9-514">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-514">**Request**</span></span>

<span data-ttu-id="3b1c9-515">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3b1c9-516">hello **업데이트 인덱스** HTTP PUT을 사용 하 여 요청을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="3b1c9-517">PUT을 사용 hello 인덱스 이름은 hello URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="3b1c9-518">Hello 인덱스가 존재 하지 않는 경우 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="3b1c9-519">Hello 인덱스가 이미 있으면 업데이트 된 toohello 새 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="3b1c9-520">hello 인덱스 이름은 소문자 여야, 문자 또는 숫자로 시작, 없습니다 슬래시나 마침표를을 있어야 128 자 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="3b1c9-521">Hello 인덱스 이름은 문자 또는 숫자로 시작 된 후 hello 나머지 hello 이름 포함할 수 있습니다는 문자, 숫자 및 대시만 hello 대시를 연속 되지 않은 상태로.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="3b1c9-522">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-523">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-524">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-525">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-525">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-526">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-527">`Content-Type`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-527">`Content-Type`: Required.</span></span> <span data-ttu-id="3b1c9-528">너무 설정 합니다.`application/json`</span><span class="sxs-lookup"><span data-stu-id="3b1c9-528">Set this too`application/json`</span></span>
* <span data-ttu-id="3b1c9-529">`api-key`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-529">`api-key`: Required.</span></span> <span data-ttu-id="3b1c9-530">hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-531">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-532">hello **인덱스 업데이트가** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-533">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-534">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-535">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-536">**요청 본문 구문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-536">**Request Body Syntax**</span></span>

<span data-ttu-id="3b1c9-537">Hello 본문 hello 원래 스키마 정의 포함 해야 기존 인덱스를 업데이트할 때 뿐만 아니라 hello 뿐만 아니라 hello 새 필드를 추가 하는 점수 매기기 프로필, CORS 옵션 및 확인 기 있는 경우 수정.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="3b1c9-538">Hello 점수 매기기 프로필과 CORS 옵션 수정 하지 않는 경우 hello 인덱스를 만들 때에서 hello 원본을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="3b1c9-539">일반적 업데이트에 대 한 최상의 패턴 toouse hello는으로 가져오기 tooretrieve hello 인덱스 정의 수정 하십시오. 다음 PUT으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="3b1c9-540">hello 스키마 구문 편의 위해 인덱스 여기에 재현 되어 toocreate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="3b1c9-541">자세한 내용은 [인덱스 만들기](#CreateIndex) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="3b1c9-542">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-542">**Response**</span></span>

<span data-ttu-id="3b1c9-543">요청이 성공적으로 실행되면 “204 콘텐츠 없음”이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="3b1c9-544">기본적으로 hello 응답 본문은 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-544">By default hello response body will be empty.</span></span> <span data-ttu-id="3b1c9-545">그러나 경우 hello, `Prefer` 요청 헤더가 너무 설정 되어`return=representation`, hello 응답 본문에는 업데이트 된 hello 인덱스 정의 대 한 JSON hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="3b1c9-546">이 경우 hello 성공 상태 코드를 됩니다 "200 확인"입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="3b1c9-547">**사용자 지정 분석기로 인덱스 정의 업데이트**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="3b1c9-548">분석기, 토크나이저, 토큰 필터 또는 문자 필터는 일단 정의한 후에는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="3b1c9-549">새로 추가할 수 있습니다 tooan 기존 인덱스는 경우에 hello `allowIndexDowntime` 플래그가 tootrue hello 인덱스 업데이트 요청에 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="3b1c9-550">이 작업을 오프 라인으로 인덱스 적어도 몇 초로 인덱싱 및 쿼리를 넣는 참고 toofail를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="3b1c9-551">Hello 인덱스의 성능 및 쓰기 가용성은 매우 큰 인덱스에 대 한 hello 인덱스를 업데이트 한 후 몇 분 동안 장애가 있는 사용자의 이상일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="3b1c9-552">인덱스 나열</span><span class="sxs-lookup"><span data-stu-id="3b1c9-552">List Indexes</span></span>
<span data-ttu-id="3b1c9-553">hello **목록 인덱스** 작업 목록을 반환 hello 인덱스의 현재 Azure 검색 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3b1c9-554">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-554">**Request**</span></span>

<span data-ttu-id="3b1c9-555">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3b1c9-556">hello **목록 인덱스** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3b1c9-557">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-558">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-559">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-560">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-560">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-561">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-562">`api-key`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-562">`api-key`: Required.</span></span> <span data-ttu-id="3b1c9-563">hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-564">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-565">hello **목록 인덱스** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-566">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-567">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-568">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-569">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-569">**Request Body**</span></span>

<span data-ttu-id="3b1c9-570">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-570">None.</span></span>

<span data-ttu-id="3b1c9-571">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-571">**Response**</span></span>

<span data-ttu-id="3b1c9-572">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3b1c9-573">아래에는 예제 응답 본문이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="3b1c9-574">참고에 관심이 toojust hello 속성 아래로 hello 응답을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="3b1c9-575">인덱스 이름 목록만 하려는 경우 OData hello를 사용 하는 예를 들어 `$select` 쿼리 옵션:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="3b1c9-576">이 경우 위 예제는 hello hello 응답은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="3b1c9-577">많은 인덱스 검색 서비스에 있는 경우에 유용한 기술 toosave 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="3b1c9-578">인덱스 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-578">Get Index</span></span>
<span data-ttu-id="3b1c9-579">hello **가져올 인덱스** Azure 검색에서 hello 인덱스 정의 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3b1c9-580">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-580">**Request**</span></span>

<span data-ttu-id="3b1c9-581">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-582">hello **가져올 인덱스** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3b1c9-583">hello [인덱스 이름] hello 요청 URI에에서는 인덱스 tooreturn hello 인덱스 컬렉션에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="3b1c9-584">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-585">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-586">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-587">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-587">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-588">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-589">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-590">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-591">hello **가져올 인덱스** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-592">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-593">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-594">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-595">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-595">**Request Body**</span></span>

<span data-ttu-id="3b1c9-596">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-596">None.</span></span>

<span data-ttu-id="3b1c9-597">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-597">**Response**</span></span>

<span data-ttu-id="3b1c9-598">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3b1c9-599">Hello 예제 JSON을 참조에서 [만들고 인덱스를 업데이트할](#CreateUpdateIndexExample) hello 응답 페이로드의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="3b1c9-600">인덱스 삭제</span><span class="sxs-lookup"><span data-stu-id="3b1c9-600">Delete Index</span></span>
<span data-ttu-id="3b1c9-601">hello **인덱스 삭제** 작업 Azure 검색 서비스에서 인덱스 및 관련된 문서를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="3b1c9-602">Hello API 또는 hello 서비스 대시보드에서 hello Azure 포털에서 hello 인덱스 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="3b1c9-603">자세한 내용은 [인덱스 나열](#ListIndexes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3b1c9-604">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-604">**Request**</span></span>

<span data-ttu-id="3b1c9-605">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-606">hello **인덱스 삭제** hello DELETE 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="3b1c9-607">hello [인덱스 이름] hello 요청 URI에에서는 인덱스 toodelete hello 인덱스 컬렉션에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="3b1c9-608">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-609">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-610">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-611">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-611">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-612">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-613">`api-key`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-613">`api-key`: Required.</span></span> <span data-ttu-id="3b1c9-614">hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-615">문자열 값, 고유 tooyour 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3b1c9-616">hello **인덱스 삭제** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-617">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-618">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-619">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-620">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-620">**Request Body**</span></span>

<span data-ttu-id="3b1c9-621">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-621">None.</span></span>

<span data-ttu-id="3b1c9-622">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-622">**Response**</span></span>

<span data-ttu-id="3b1c9-623">상태 코드: 응답에 성공하면 ‘204 콘텐츠 없음’이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="3b1c9-624">인덱스 통계 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-624">Get Index Statistics</span></span>
<span data-ttu-id="3b1c9-625">hello **인덱스 통계 가져오기** 작업 hello 현재 인덱스와 저장소 사용량에 대 한 문서 수를 Azure 검색에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="3b1c9-626">문서 수와 저장소 크기에 대한 통계는 실시간이 아니라 몇 분 간격으로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="3b1c9-627">이 API에서 반환 되는 hello 통계는 최근 인덱싱 작업에 의해 발생 한 변경 내용을 나타내지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="3b1c9-628">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-628">**Request**</span></span>

<span data-ttu-id="3b1c9-629">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="3b1c9-630">hello **인덱스 통계 가져오기** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3b1c9-631">hello 요청 URI의에서 [index name] hello hello 지정 된 인덱스에 대 한 hello 서비스 tooreturn 인덱스 통계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="3b1c9-632">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-633">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-634">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-635">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-635">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-636">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-637">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-638">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-639">hello **인덱스 통계 가져오기** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-640">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-641">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-642">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-643">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-643">**Request Body**</span></span>

<span data-ttu-id="3b1c9-644">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-644">None.</span></span>

<span data-ttu-id="3b1c9-645">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-645">**Response**</span></span>

<span data-ttu-id="3b1c9-646">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3b1c9-647">형식에 따라 hello에 hello 응답 본문은입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="3b1c9-648">테스트 분석기</span><span class="sxs-lookup"><span data-stu-id="3b1c9-648">Test Analyzer</span></span>
<span data-ttu-id="3b1c9-649">hello **분석 API** 분석기를 토큰으로 텍스트를 중단 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3b1c9-650">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-650">**Request**</span></span>

<span data-ttu-id="3b1c9-651">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="3b1c9-652">hello **분석 API** hello POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="3b1c9-653">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-654">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-655">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-656">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-656">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-657">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-658">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-659">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-660">hello **분석 API** 요청에 포함 해야 합니다는 `api-key` (것과 반대로 tooa 쿼리 키)로 tooan 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-661">Hello 인덱스 이름과 hello 서비스 이름 tooconstruct hello 요청 URL 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-662">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-663">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-664">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="3b1c9-665">또는</span><span class="sxs-lookup"><span data-stu-id="3b1c9-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="3b1c9-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` 및 `char_filter_name` hello 인덱스에 대 한 미리 정의 된 또는 사용자 지정 분석기, 토크 나이저, 토큰 필터 및 char 필터의 toobe 유효한 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="3b1c9-667">어휘 분석의 hello 프로세스에 대 한 자세한 참조 toolearn [Azure 검색의 분석](https://aka.ms/azsanalysis)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="3b1c9-668">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-668">**Response**</span></span>

<span data-ttu-id="3b1c9-669">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3b1c9-670">형식에 따라 hello에 hello 응답 본문은입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="3b1c9-671">**분석 API 예제**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-671">**Analyze API example**</span></span>

<span data-ttu-id="3b1c9-672">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="3b1c9-673">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="3b1c9-674">문서 작업</span><span class="sxs-lookup"><span data-stu-id="3b1c9-674">Document Operations</span></span>
<span data-ttu-id="3b1c9-675">Azure 검색에서 인덱스 hello 클라우드에 저장 되 고 toohello 서비스 업로드 하는 JSON 문서를 사용 하 여 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="3b1c9-676">업로드 하는 모든 hello 문서 검색 데이터의 hello 모음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="3b1c9-677">문서에는 필드가 포함되며, 이러한 필드 중 일부는 문서 업로드 시 검색 용어로 토큰화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="3b1c9-678">hello `/docs` hello Azure 검색 API에에서 URL 세그먼트는 인덱스의 문서 hello 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="3b1c9-679">업로드 같은 hello 컬렉션에서 수행 된 모든 작업, 병합, 삭제 또는 문서를 쿼리 수행 하므로 hello Url은 단일 인덱스의 hello 컨텍스트에서 이러한 작업은 항상 시작에 대 한 `/indexes/[index name]/docs` 지정된 된 인덱스 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="3b1c9-680">응용 프로그램 코드 JSON 문서 tooupload tooAzure 검색을 생성 해야 하거나 사용할 수 있습니다는 [인덱서](https://msdn.microsoft.com/library/dn946891.aspx) tooload 이면 hello 데이터 원본이 Azure Cosmos DB 나 Azure SQL 데이터베이스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="3b1c9-681">일반적으로 인덱스는 사용자가 제공하는 단일 데이터 집합에서 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="3b1c9-682">Toosearch 원하는 각 항목에 대 한 문서에 계획 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="3b1c9-683">예를 들어 영화 대여 응용 프로그램은 영화당 문서 하나를, 상점 응용 프로그램은 SKU당 문서 하나를, 온라인 교육 과정 응용 프로그램은 과정당 문서 하나를, 리서치 업체는 리포지토리의 학술 문서당 문서 하나를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="3b1c9-684">문서는 하나 이상의 필드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="3b1c9-685">필드는 Azure 검색에서 검색 용어로 토큰화되는 텍스트를 포함할 수 있으며 필터 또는 점수 매기기 프로필에서 사용할 수 있는 토큰화되지 않는 값 또는 텍스트가 아닌 값도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="3b1c9-686">hello 이름, 데이터 형식 및 각 필드에 대해 지원 되는 검색 기능에 의해 결정 됩니다 hello 인덱스 스키마.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="3b1c9-687">각 인덱스 스키마의 hello 필드 중 하나는 ID로 지정 해야 하며 각 문서 hello 인덱스에서 해당 문서를 고유 하 게 식별 하는 hello ID 필드에 대 한 값 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="3b1c9-688">다른 모든 문서 필드 선택 사항이 며 지정 하지 않으면 기본 tooa null 값 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="3b1c9-689">Hello 검색 인덱스의 공간을 null 값을 사용 하지 않는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="3b1c9-690">문서를 업로드할 수 있습니다, 전에 해야 이미 만든 hello 인덱스 hello 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="3b1c9-691">이 첫 단계에 대한 자세한 내용은 [인덱스 만들기](#CreateIndex) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="3b1c9-692">문서 추가, 업데이트 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="3b1c9-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="3b1c9-693">HTTP POST를 사용하여 지정한 인덱스에서 문서를 업로드, 병합, 병합하거나 업로드 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="3b1c9-694">업데이트의 많은 수에 대 한 문서 (일괄 처리당 문서 too1000) 또는 일괄 처리당 약 16MB를 일괄 처리할 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3b1c9-695">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-695">**Request**</span></span>

<span data-ttu-id="3b1c9-696">모든 서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3b1c9-697">HTTP POST를 사용하여 지정한 인덱스에서 문서를 업로드, 병합, 병합하거나 업로드 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="3b1c9-698">hello 요청 URI [index name]에 포함 됩니다. 인덱스 toopost 문서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="3b1c9-699">한 번에만 문서 tooone 인덱스를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="3b1c9-700">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-701">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-702">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-703">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-703">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-704">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-705">`Content-Type`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-705">`Content-Type`: Required.</span></span> <span data-ttu-id="3b1c9-706">너무 설정 합니다.`application/json`</span><span class="sxs-lookup"><span data-stu-id="3b1c9-706">Set this too`application/json`</span></span>
* <span data-ttu-id="3b1c9-707">`api-key`: 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-707">`api-key`: Required.</span></span> <span data-ttu-id="3b1c9-708">hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-709">문자열 값, 고유 tooyour 서비스 이며</span><span class="sxs-lookup"><span data-stu-id="3b1c9-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3b1c9-710">hello **문서 추가** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3b1c9-711">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-712">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-713">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-714">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-714">**Request Body**</span></span>

<span data-ttu-id="3b1c9-715">hello hello 요청 본문을 포함 하나 또는 자세한 문서 toobe 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="3b1c9-716">고유 키로 문서를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="3b1c9-717">각 문서는 upload, merge, mergeOrupload 또는 delete 작업과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="3b1c9-718">업로드 요청 키/값 쌍의 집합으로 hello 문서 데이터를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="3b1c9-719">문서 키에는 문자, 숫자, 대시("-"), 밑줄("_") 및 등호("=")만 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="3b1c9-720">자세한 내용은 [명명 규칙](https://msdn.microsoft.com/library/azure/dn857353.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="3b1c9-721">**문서 작업**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-721">**Document Actions**</span></span>

* <span data-ttu-id="3b1c9-722">`upload`: 업로드 작업은 유사 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="3b1c9-723">Hello 업데이트 경우에서 모든 필드가 바뀌는 것을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="3b1c9-724">`merge`: 병합 업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="3b1c9-725">Hello 문서가 존재 하지 않는 경우 hello 병합 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="3b1c9-726">병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="3b1c9-727">여기에는 `Collection(Edm.String)`형식 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="3b1c9-728">예를 들어 hello 문서 있으면 필드 값을 가진 "tags" `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` "tags" hello "tags" 필드의 최종 값 hello 됩니다 `["economy", "pool"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="3b1c9-729">`["budget", "economy", "pool"]`이 되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="3b1c9-730">`mergeOrUpload`: 처럼 동작 `merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="3b1c9-731">Hello 문서 존재 하지 않는 경우 처럼 동작 `upload` 새 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="3b1c9-732">`delete`: 삭제 hello 인덱스에서 hello 지정 된 문서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="3b1c9-733">모든 필드에서 지정 하는 참고는 `delete` hello 키 필드 이외의 작업은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="3b1c9-734">문서에서 개별 필드 tooremove 사용 `merge` 대신 하 고 간단 하 게 hello 필드 명시적으로 설정 너무`null`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="3b1c9-735">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-735">**Response**</span></span>

<span data-ttu-id="3b1c9-736">작업 성공 시의 응답에는 상태 코드 200 (OK)가 반환됩니다. 이 응답은 모든 항목이 올바르게 인덱싱되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="3b1c9-737">이 hello로 표시 `status` tootrue hello 뿐만 아니라 모든 항목에 대 한 설정 속성 `statusCode` tooeither 201 (문서에 대 한 새로 업로드 된) 또는 200 (병합 또는 삭제 된 문서)에 대 한 설정 속성:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="3b1c9-738">하나 이상의 항목이 성공적으로 인덱싱되지 않은 경우 상태 코드 207(다중 상태)이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="3b1c9-739">인덱싱되지 않은 된 항목은 hello `status` toofalse 필드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="3b1c9-740">hello `errorMessage` 및 `statusCode` 속성 인덱싱 오류 hello에 대 한 hello 이유를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="3b1c9-741">다음 표에서 hello hello 다양 한 문서별 hello 응답에서 반환 될 수 있는 상태 코드에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="3b1c9-742">임시 오류 상태를 나타내는 다른 동안 hello 요청 자체의 문제를 나타낼 일부 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="3b1c9-743">hello 후자 지연 후에 다시 시도해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="3b1c9-744">상태 코드</span><span class="sxs-lookup"><span data-stu-id="3b1c9-744">Status code</span></span></th>
        <th><span data-ttu-id="3b1c9-745">의미</span><span class="sxs-lookup"><span data-stu-id="3b1c9-745">Meaning</span></span></th>
        <th><span data-ttu-id="3b1c9-746">재시도 가능</span><span class="sxs-lookup"><span data-stu-id="3b1c9-746">Retryable</span></span></th>
        <th><span data-ttu-id="3b1c9-747">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3b1c9-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-748">200</span><span class="sxs-lookup"><span data-stu-id="3b1c9-748">200</span></span></td>
        <td><span data-ttu-id="3b1c9-749">문서가 성공적으로 수정되었거나 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="3b1c9-750">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b1c9-750">n/a</span></span></td>
        <td><span data-ttu-id="3b1c9-751">삭제 작업은 <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="3b1c9-752">즉, 문서 키 hello 인덱스에 없는 경우에 삭제 작업은 해당 키가 있는 발생 합니다는 200 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-753">201</span><span class="sxs-lookup"><span data-stu-id="3b1c9-753">201</span></span></td>
        <td><span data-ttu-id="3b1c9-754">문서를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="3b1c9-755">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b1c9-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-756">400</span><span class="sxs-lookup"><span data-stu-id="3b1c9-756">400</span></span></td>
        <td><span data-ttu-id="3b1c9-757">인덱싱되는 것을 방해 하는 hello 문서에 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="3b1c9-758">아니요</span><span class="sxs-lookup"><span data-stu-id="3b1c9-758">No</span></span></td>
        <td><span data-ttu-id="3b1c9-759">무엇이 잘못 된 hello 문서 hello에 대 한 응답 hello 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-760">404</span><span class="sxs-lookup"><span data-stu-id="3b1c9-760">404</span></span></td>
        <td><span data-ttu-id="3b1c9-761">hello 인덱스에 키를 제공 하는 hello 존재 하지 않아 hello 문서를 병합할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="3b1c9-762">아니요</span><span class="sxs-lookup"><span data-stu-id="3b1c9-762">No</span></span></td>
        <td><span data-ttu-id="3b1c9-763">새 문서를 만들기 때문에 업로드에 이 오류가 발생하지 않으며 <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>이므로 삭제에 오류가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-764">409</span><span class="sxs-lookup"><span data-stu-id="3b1c9-764">409</span></span></td>
        <td><span data-ttu-id="3b1c9-765">Tooindex 문서를 시도할 때 버전 충돌이 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="3b1c9-766">예</span><span class="sxs-lookup"><span data-stu-id="3b1c9-766">Yes</span></span></td>
        <td><span data-ttu-id="3b1c9-767">동시에 두 번 이상 문서 동일 tooindex hello 려 할 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-768">422</span><span class="sxs-lookup"><span data-stu-id="3b1c9-768">422</span></span></td>
        <td><span data-ttu-id="3b1c9-769">hello 인덱스 이므로 일시적으로 사용할 수 없습니다 'hello 'allowIndexDowntime 플래그 집합 too'true로 업데이트 되었습니다 '.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="3b1c9-770">예</span><span class="sxs-lookup"><span data-stu-id="3b1c9-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b1c9-771">503</span><span class="sxs-lookup"><span data-stu-id="3b1c9-771">503</span></span></td>
        <td><span data-ttu-id="3b1c9-772">검색 서비스 tooheavy 부하 가능 인해 일시적으로 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="3b1c9-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="3b1c9-773">예</span><span class="sxs-lookup"><span data-stu-id="3b1c9-773">Yes</span></span></td>
        <td><span data-ttu-id="3b1c9-774">이 경우 다시 시도 하기 전에 대기 해야 할 코드 또는 hello 서비스 사용 불가 연장 될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="3b1c9-775">**참고**: 한 가지 가능한 이유 hello 시스템의 부하가 클라이언트 코드를 207 응답이 자주에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="3b1c9-776">Hello를 확인 하 여이 확인할 수 있습니다 `statusCode` 503에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="3b1c9-777">Hello 대/소문자, 이것이 권장 ***인덱싱 요청 제한***합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="3b1c9-778">그렇지 않은 경우 인덱싱 트래픽이 감소 하지 hello 시스템 503 오류가 발생 한 모든 요청을 거부 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="3b1c9-779">상태 코드 429 hello 인덱스 당 문서 수의 할당량이 초과 되었다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="3b1c9-780">이 경우에는 새 인덱스를 만들거나 업그레이드를 통해 용량 제한을 높여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="3b1c9-781">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="3b1c9-782">문서 검색</span><span class="sxs-lookup"><span data-stu-id="3b1c9-782">Search Documents</span></span>
<span data-ttu-id="3b1c9-783">A **검색** 작업이 GET 또는 POST 요청으로 발생 하 고 일치 하는 문서를 선택 하는 것에 대 한 hello 조건을 제공 하는 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="3b1c9-784">**대신 toouse 게시 하는 경우**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="3b1c9-785">HTTP GET toocall hello를 사용 하는 경우 **검색** API 해야 toobe 인식 hello 요청 URL의 hello 길이 8KB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="3b1c9-786">이 크기는 일반적으로 대부분의 응용 프로그램에서 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-786">This is usually enough for most applications.</span></span> <span data-ttu-id="3b1c9-787">그러나 일부 응용 프로그램은 매우 큰 쿼리 또는 OData 필터 식을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="3b1c9-788">이러한 응용 프로그램의 경우 GET보다 더 많은 필터와 쿼리를 허용할 수 있는 HTTP POST를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="3b1c9-789">POST, 용어 또는 쿼리에서 절 hello 수와 hello을 제한 하 hello 원시 쿼리 POST에 대 한 hello 요청 크기 제한 약 16MB 이므로의 hello 크기가 아니라 요소인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-790">Hello POST 요청 크기 제한의 용량이 클 경우에 검색 쿼리 및 필터 식을 임의의 복잡 한 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="3b1c9-791">검색 쿼리 및 필터 복잡성 제한에 대한 자세한 내용은 [Lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx) 및 [OData 식 구문](https://msdn.microsoft.com/library/dn798921.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="3b1c9-792">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-792">**Request**</span></span>

<span data-ttu-id="3b1c9-793">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-794">hello **검색** hello GET 또는 POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="3b1c9-795">hello 요청 URI는 인덱스 tooquery hello 매개 변수와 일치 하는 모든 문서에 대 한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="3b1c9-796">GET 요청의 경우 hello hello 쿼리 문자열에 대해 매개 변수를 지정 하 고 hello 경우 POST의 본문 hello 요청에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="3b1c9-797">모범 사례로 GET 요청을 만들 때, 기억 너무[URL로 인코드할](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) 특정 쿼리 매개 변수를 호출할 때 REST API를 직접 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="3b1c9-798">**검색** 작업의 경우 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="3b1c9-799">URL 인코딩은 위의 쿼리 매개 변수는 hello에만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="3b1c9-800">실수로 URL로 인코딩할 수 있습니다 (다음의 모든 hello?)는 전체 쿼리 문자열 hello, 요청이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="3b1c9-801">또한 URL 인코딩은 필요한 경우에 REST API를 사용 하 여 직접 가져올 hello를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="3b1c9-802">호출할 때 필요한은 URL 인코딩 없이 **검색** POST를 사용 하 여 hello를 사용 하는 경우 [.NET 클라이언트 라이브러리](https://msdn.microsoft.com/library/dn951165.aspx), URL 인코딩을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="3b1c9-803"><a name="SearchQueryParameters"></a>
**쿼리 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="3b1c9-804">**검색** 은 쿼리 조건을 제공하고 검색 동작을 지정하는 여러 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="3b1c9-805">호출할 때 이러한 매개 변수 hello URL에 쿼리 문자열을 제공 **검색** GET을 통해 및를 호출할 때 hello 요청 본문의 JSON 속성으로 **검색** POST 통해.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="3b1c9-806">hello 일부 매개 변수의 구문에는 GET 및 POST 간에 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="3b1c9-807">이러한 차이가 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="3b1c9-808">`search=[string]`(선택 사항)-hello에 대 한 텍스트 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="3b1c9-809">`searchFields`를 지정하지 않으면 기본적으로 모든 `searchable` 필드가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="3b1c9-810">검색할 때 `searchable` 필드, hello 검색 텍스트 자체가 토큰화 되므로 여러 용어를 공백으로 구분할 수 있습니다 (예: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="3b1c9-811">모든 용어를 사용 하 여 toomatch `*` (이 기능은 유용 부울 필터 쿼리에서).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="3b1c9-812">효과가 너무 설정 같음 hello에이 매개 변수를 생략`*`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="3b1c9-813">참조 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx) hello 검색 구문에 사양에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="3b1c9-814">**참고**: hello 결과 수 놀라운를 통해 쿼리할 때 `searchable` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="3b1c9-815">숫자, 등에서 아포스트로피, 쉼표와 같은 논리 toohandle의 경우 일반적인 tooEnglish 텍스트를 포함 하는 hello 토크 나이저입니다. 예를 들어 `search=123,456` 영어에서 큰 수의 천 구분 기호로 쉼표를 사용 하므로 hello 개별 용어인 123과 456, 보다는 단일 용어 123456 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="3b1c9-816">이러한 이유로 tooseparate 용어 문장 부호가 아닌 공백을 hello에 사용할 수 있는 권장 `search` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="3b1c9-817">`searchMode=any|all`(선택 사항 너무 기본값`any`)-hello 검색 용어 중 일부 또는 모두 일치 기준으로 하는 순서 toocount hello 문서의 일치 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="3b1c9-818">`searchFields=[string]`(선택 사항)-hello 목록을 쉼표로 구분 된 필드 이름 toosearch hello에 대 한 텍스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="3b1c9-819">대상 필드는 `searchable`로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="3b1c9-820">`queryType=simple|full`(선택 사항 너무 기본값`simple`)와 같은 기호에 대 한 허용 하는 간단한 쿼리 언어를 사용 하 여 텍스트를 "단순" 너무 검색 하는 집합을 해석할 때-+, * 및 ""입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="3b1c9-821">쿼리는 기본적으로 각 문서의 모든 검색 가능 필드(또는 `searchFields`에 나타난 필드)에 걸쳐 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="3b1c9-822">Hello 쿼리 유형을 너무 설정 되 면`full` 검색 텍스트 필드별 및가 중 검색이 허용 하는 hello Lucene 쿼리 언어를 사용 하 여 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="3b1c9-823">참조 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx) 및 [Lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx) hello 검색 구문에 사양에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="3b1c9-824">범위 검색의 hello Lucene $filter 유사한 기능을 제공 하는 대신 쿼리 언어를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="3b1c9-825">`moreLikeThis=[key]`(선택) **중요:** 이 기능은 `2015-02-28-Preview`에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-826">이 옵션은 hello 텍스트 검색 매개 변수를 포함 하는 쿼리에 사용할 수 없습니다 `search=[string]`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="3b1c9-827">hello `moreLikeThis` 매개 변수는 hello 문서 키로 지정 된 유사한 toohello 문서는 문서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="3b1c9-828">검색 요청으로 설정 되는 경우 `moreLikeThis`, 검색 용어 목록을 hello 빈도 및 흔히 볼 hello 소스 문서에서 조건에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="3b1c9-829">이러한 용어가 사용 되는 toomake hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="3b1c9-830">기본적으로 모든 내용을 hello `searchable` 필드가 하지 않는 한 것으로 간주 `searchFields` 가 사용 되는 toorestrict 검색 되는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="3b1c9-831">`$skip=#`(선택 사항)-검색 수가 hello tooskip; 결과 100, 000 보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="3b1c9-832">Tooscan 문서 순서에 필요한 경우 있지만 사용할 수 없습니다 `$skip` toothis 제한으로 인해 사용 하는 것이 좋습니다 `$orderby` 완전히 정렬 된 키에 및 `$filter` 범위를 가진 대신를 쿼리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-833">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$skip` 대신 `skip`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-834">`$top=#`(선택 사항)-tooretrieve 결과 하는 hello 수 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="3b1c9-835">이와 함께에서 사용할 수 있습니다 `$skip` 검색 결과의 tooimplement 클라이언트 쪽 페이징 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-836">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$top` 대신 `top`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-837">`$count=true|false`(선택 사항 너무 기본값`false`)-toofetch hello 총 결과 수 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="3b1c9-838">이 값은 hello와 일치 하는 모든 문서 hello 개수 `search` 및 `$filter` 매개 변수를 무시 하 고 `$top` 및 `$skip`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="3b1c9-839">이 값을 너무 설정`true` 성능 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="3b1c9-840">참고가 반환 하는 hello 개수는 근사값입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-841">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$count` 대신 `count`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-842">`$orderby=[string]`(선택 사항)-toosort hello 쉼표로 구분 된 식 결과의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="3b1c9-843">각 식은 필드 이름 또는 호출 toohello 가능 `geo.distance()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="3b1c9-844">각 식은 올 수 있는 `asc` tooindicated 오름차순 및 `desc` 내림차순 tooindicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="3b1c9-845">hello 기본값은 오름차순입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-845">hello default is ascending order.</span></span> <span data-ttu-id="3b1c9-846">동률 문서의 hello 일치 점수에 의해 손상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="3b1c9-847">하지 않으면 `$orderby` hello 기본 정렬 순서는 문서 일치 점수 기준 내림차순 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="3b1c9-848">`$orderby`절은 32개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-849">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$orderby` 대신 `orderby`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-850">`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3b1c9-851">지정 하지 않으면 hello 스키마에서 검색 가능한로 표시 된 모든 필드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="3b1c9-852">이 매개 변수를 너무 설정 하 여 모든 필드를 명시적으로 요청할 수 있습니다`*`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-853">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$select` 대신 `select`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-854">`facet=[string]`(0 개 이상)-하 여 필드 toofacet 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="3b1c9-855">Hello 문자열 매개 변수 toocustomize hello 패싯 쉼표로 구분 된 00z를 포함할 수 있습니다는 필요에 따라 `name:value` 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="3b1c9-856">유효한 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-856">Valid parameters are:</span></span>

* <span data-ttu-id="3b1c9-857">`count` (패싯 용어의 최대 개수, 기본값은 10).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="3b1c9-858">최대값 없음 있지만 값이 높을수록 hello 패싯 필드에 고유 용어가 많이 포함 하는 경우에 특히 해당 성능 저하를 유발 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="3b1c9-859">예를 들어: `facet=category,count:5` 패싯 결과에서 상위 5 개 범주를 hello 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="3b1c9-860">**참고**: 경우 hello `count` 매개 변수는 고유 용어의 hello 번호 보다 작은, hello 결과가 정확 하 게 불완전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="3b1c9-861">이 패싯 쿼리가 여러 분할으로 분산 된 toohello 방식 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="3b1c9-862">증가 `count` 일반적으로 증가 hello 정확도 hello 용어 개수의 있지만 성능은 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="3b1c9-863">`sort`(중 하나 `count` toosort *내림차순* 개수 별로 `-count` toosort *오름차순* 개수 별로 `value` toosort *오름차순* 값, 또는 `-value` toosort *내림차순* 값별로)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="3b1c9-864">예를 들어: `facet=category,count:3,sort:count` 가져옵니다 hello 각 도시 이름과 사용 하 여 문서의 hello 번호로 순서를 내림차순으로 패싯 결과의 상위 세 가지 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="3b1c9-865">예를 들어 hello 상위 3 개 범주가 Budget, Motel, Luxury 이며 각는 및 적중 수가 5, 6, 및 4, 않으면 hello 버킷 됩니다 hello 순서로 Motel, Budget, Luxury 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="3b1c9-866">예: `facet=rating,sort:-value` 는 값을 기준으로 내림차순으로 정렬된 가능한 모든 등급의 버킷을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="3b1c9-867">예를 들어 hello 등급 인 1 too5에서 5, 4, 3, 2, 1, 문서 각 등급에 일치 하는 관계 없이 hello 버킷 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="3b1c9-868">`values`(파이프로 구분된 숫자 또는 패싯 항목 값의 동적 집합을 지정하는 `Edm.DateTimeOffset` 값)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="3b1c9-869">예를 들어: `facet=baseRate,values:10|20` 세 개의 버킷이 생성:, 및 20, 20 이상의 용 점을 포함 하지 toobut 10에 대 한 10 toobut 기본 숙박료가 0에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="3b1c9-870">예: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z`는 각각 2010년 2월 이전에 리노베이션된 호텔과 2010년 2월 1일 이후에 리노베이션된 호텔에 대한 버킷 2개를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="3b1c9-871">`interval`(숫자의 경우 0보다 큰 정수 간격 또는 날짜/시간 값의 경우 `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year`)</span><span class="sxs-lookup"><span data-stu-id="3b1c9-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="3b1c9-872">예: `facet=baseRate,interval:100`은 기본 요금 범위 100을 기준으로 버킷을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="3b1c9-873">예를 들어 기본 요금이 모두 $60에서 $600 사이에 속한 경우 0-100, 100-200, 200-300, 300-400, 400-500 및 500-600에 대한 버킷이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="3b1c9-874">예: `facet=lastRenovationDate,interval:year`는 호텔이 리노베이션된 각 연도에 대해 하나의 버킷을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="3b1c9-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, 또는 [+-]hh) `timeoffset`은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="3b1c9-876">Hello와 결합할 수만 있습니다 `interval` 옵션을 선택한 경우에만 적용 된 tooa 필드 형식의 `Edm.DateTimeOffset`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="3b1c9-877">hello 값에 대 한 hello UTC 시간 오프셋된 tooaccount 시간 경계 설정 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="3b1c9-878">예를 들어: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` 사용 하 여 hello 01시: 00 UTC (hello 대상 표준 시간대에서 자정)에서 시작 하는 일 경계</span><span class="sxs-lookup"><span data-stu-id="3b1c9-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="3b1c9-879">**참고**: `count` 및 `sort` 에 결합할 수 있습니다 hello 같은 패싯 사양 있지만 함께 사용할 수 없는 `interval` 또는 `values`, 및 `interval` 및 `values` 함께 결합할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="3b1c9-880">**참고**: `timeoffset`을 지정하지 않은 경우 날짜 시간의 간격 패싯은 UTC 시간을 기준으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="3b1c9-881">예를 들어:에 대 한 `facet=lastRenovationDate,interval:day`, hello 일 경계 00시: 00 UTC에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="3b1c9-882">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `facet` 대신 `facets`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="3b1c9-883">또한 문자열의 JSON 배열로 지정할 수도 있습니다. 여기서 각 문자열은 별도의 패싯 식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="3b1c9-884">`$filter=[string]` (선택) - 표준 OData 구문의 구조화된 검색 식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-885">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `$filter` 대신 `filter`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-886">`highlight=[string]` (선택) - 적중 항목을 강조 표시하는 데 사용되는 쉼표로 구분된 필드 이름 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="3b1c9-887">`searchable` 필드만 적중 항목 강조 표시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="3b1c9-888">`highlightPreTag=[string]`(선택 사항 너무 기본값`<em>`)-태그 toohit 밝은 앞에 추가 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="3b1c9-889">`highlightPostTag`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-890">호출할 때 **검색** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3b1c9-891">`highlightPostTag=[string]`(선택 사항 너무 기본값`</em>`)-toohit 하이라이트를 추가 하는 문자열 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="3b1c9-892">`highlightPreTag`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-893">호출할 때 **검색** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3b1c9-894">`scoringProfile=[string]`(선택 사항)-점수 매기기 프로필 tooevaluate의 hello 이름을 순서 toosort hello 결과에 일치 하는 문서에 대 한 점수와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="3b1c9-895">`scoringParameter=[string]`점수 매기기 함수에 정의 된 각 매개 변수에 대해 hello 값을 나타냅니다 (0 개 이상)-(예를 들어 `referencePointParameter`) hello 형식을 사용 하 여 `name-value1,value2,...`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="3b1c9-896">예를 들어 점수 매기기 프로필 hello 함수를 정의 하는 경우 "mylocation" hello 쿼리 문자열 옵션 라는 매개 변수를 것 `&scoringParameter=mylocation--122.2,44.8`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="3b1c9-897">첫 번째 대시 hello hello 두 번째 대시 hello 첫 번째 값 (이 예제의 경도)의 일부인 동안 hello 값 목록에서 hello 이름과 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="3b1c9-898">점수 매기기 매개 변수 태그에 대 한 승격 하는 포함 될 수 있습니다 쉼표와 같은 단일 따옴표를 사용 하 여 hello 목록에서 이러한 값 이스케이프 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="3b1c9-899">Hello 값 자체 작은따옴표가 들어 있으면 이중 이스케이프 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="3b1c9-900">예를 들어 "mytag" 라는 매개 변수를 승격 하는 태그를가 하 고 tooboost hello 태그에 값 "Hello, O'Brien" 및 "Smith", hello 쿼리 문자열 옵션 것 `&scoringParameter=mytag-'Hello, O''Brien',Smith`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="3b1c9-901">따옴표는 쉼표를 포함하는 값에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-902">POST를 사용하여 **검색**을 호출하는 경우 이 매개 변수의 이름은 `scoringParameter` 대신 `scoringParameters`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="3b1c9-903">또한 문자열의 JSON 배열로 지정할 수도 있습니다. 여기서 각 문자열은 별도의 `name-values` 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="3b1c9-904">`minimumCoverage`(선택 사항 기본값 too100)-0과 100 쿼리 toobe hello에 대 한 순서 대로 검색 쿼리에서 포함 되어야 하는 hello 인덱스의 hello 백분율을 나타내는 사이의 숫자를 성공으로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="3b1c9-905">기본적으로 전체 인덱스 hello 사용할 수 있어야 하거나 `Search` 503 HTTP 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="3b1c9-906">설정한 경우 `minimumCoverage` 및 `Search` 성공 하면 HTTP 200을 반환 하 고 포함 한 `@search.coverage` hello에 대 한 응답 hello 쿼리에 포함 된 hello 인덱스의 hello 백분율을 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-907">이 매개 변수 tooa 값 100 검색 가용성 복제본을 하나만 사용 하 여 서비스에 대해서도 보장 하는 데 유용할 수 있습니다 보다 낮게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="3b1c9-908">그러나 일부 일치 하는 문서가 toobe hello 검색 결과 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="3b1c9-909">검색 회수는 가용성, 보다 더 중요 한 tooyour 응용 프로그램을 경우 최상의 tooleave `minimumCoverage` 100 기본값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="3b1c9-910">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-911">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-912">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-913">참고:이 작업에 대 한 hello `api-version` 호출 여부에 관계 없이 hello URL에 쿼리 매개 변수로 지정 **검색** GET 또는 POST입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="3b1c9-914">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-914">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-915">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-916">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-917">문자열 값, 고유 tooyour 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3b1c9-918">hello **검색** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3b1c9-919">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-920">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-921">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-922">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-922">**Request Body**</span></span>

<span data-ttu-id="3b1c9-923">GET의 경우: 없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-923">For GET: None.</span></span>

<span data-ttu-id="3b1c9-924">POST의 경우:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="3b1c9-925">**부분 검색 응답의 연속 작업**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="3b1c9-926">경우에 따라 Azure 검색 모든 hello 단일 검색 응답에서 요청 된 결과 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="3b1c9-927">Hello 쿼리 지정 하 여 너무 많은 문서를 요청 하는 경우와 같은 다양 한 이유로 발생할 수 있습니다 `$top` 에 대 한 값을 지정 하거나 `$top` 는 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="3b1c9-928">이러한 경우 Azure 검색 hello에 포함할 `@odata.nextLink` hello 응답 본문에 주석 및 `@search.nextPageParameters` POST 요청을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="3b1c9-929">검색 요청 tooget hello 다음의 다른 부분 hello 검색 응답의 이러한 주석 tooformulate hello 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="3b1c9-930">이 라고는 ***연속*** 원래 검색 요청 hello 및 hello 주석은 일반적으로 호출 ***연속 토큰***합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="3b1c9-931">참조 [hello 감시할](#SearchResponse) hello 구문 이러한 주석의 및 나타나는 hello 응답 본문에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="3b1c9-932">hello Azure 검색에서 연속 토큰을 반환할 수 있습니다는 이유 원인은 구현의 및 제목 toochange입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="3b1c9-933">강력한 클라이언트에는 항상 준비 toohandle 예상 보다 더 적은 문서가 반환 됩니다 대 한 경우 연속 토큰이 포함된 toocontinue 문서를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="3b1c9-934">또한 사용 해야 하는 hello 순서 toocontinue에 hello 원래 요청으로 동일한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="3b1c9-935">예를 들어 GET 요청을 보냈으면 보내는 모든 연속 작업 요청에서도 GET을 사용해야 합니다(POST도 마찬가지).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="3b1c9-936"><a name="SearchResponse"></a>
**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="3b1c9-937">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="3b1c9-938">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-938">**Examples:**</span></span>

<span data-ttu-id="3b1c9-939">Hello에서 추가 예제를 찾을 수 있습니다 [Azure 검색의 OData 식 구문](https://msdn.microsoft.com/library/azure/dn798921.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="3b1c9-940">인덱스 검색 hello 날짜별으로 내림차순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="3b1c9-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="3b1c9-943">패싯 검색에서 hello 색인을 검색 하 고 특정 범위의 baseRate 항목 뿐만 아니라 범주, 등급, 태그, 패싯 검색:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="3b1c9-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="3b1c9-946">필터를 사용 하 여 범위를 좁힐 hello 이전 패싯 쿼리 결과 hello 사용자가 클릭 한 후 rating 3 및 "Motel" 범주:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="3b1c9-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="3b1c9-949">패싯 검색에서 쿼리에 반환되는 고유 항목의 상한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="3b1c9-950">hello 기본값은 10 이지만 늘리거나 hello를 사용 하 여이 값을 줄일 수 `count` hello에 대 한 매개 변수 `facet` 특성:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="3b1c9-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="3b1c9-953">의 특정 필드 내 인덱스 검색 hello 예를 들어 언어별 필드:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="3b1c9-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="3b1c9-956">여러 필드에서 hello 인덱스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="3b1c9-957">예를 들어 저장할 수 있으며 모든 내 여러 언어로 쿼리 검색 가능한 필드 hello 같은 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="3b1c9-958">영어와 프랑스어 설명에에서 함께 존재 hello 동일한 경우 문서를 반환할 수 있습니다 임의로 또는 모두에 hello 쿼리 결과:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="3b1c9-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="3b1c9-961">한 번에 하나의 인덱스만 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="3b1c9-962">한 번에 하나의 tooquery 하려는 경우가 아니면 각 언어에 대해 여러 인덱스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="3b1c9-963">페이징-항목의 Get hello 첫 페이지 (페이지 크기는 10):</span><span class="sxs-lookup"><span data-stu-id="3b1c9-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="3b1c9-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="3b1c9-966">페이징-항목의 Get hello 두 번째 페이지 (페이지 크기는 10):</span><span class="sxs-lookup"><span data-stu-id="3b1c9-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="3b1c9-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="3b1c9-969">특정 필드 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="3b1c9-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="3b1c9-972">특정 필터 식과 일치하는 문서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="3b1c9-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="3b1c9-975">Hello 색인을 검색 하 고 적중된 항목이 강조 표시 된 조각 반환</span><span class="sxs-lookup"><span data-stu-id="3b1c9-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="3b1c9-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="3b1c9-978">Hello 인덱스를 검색 하는 참조 위치에서 가까운 toofarther에서 순으로 정렬 하는 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="3b1c9-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="3b1c9-981">거리 점수 매기기 설명한 "geo" 라는 점수 매기기 프로필은 검색 hello 인덱스 가정 하는 경우, "currentLocation" 및 포함 된 매개 변수 정의 하나 라는 하나의 매개 변수 정의</span><span class="sxs-lookup"><span data-stu-id="3b1c9-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="3b1c9-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="3b1c9-984">사용 하 여 hello 인덱스에서 문서를 찾습니다 [단순 쿼리 구문을](https://msdn.microsoft.com/library/dn798920.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="3b1c9-985">이 쿼리 hello "comfort" 및 "위치" 있지만 "motel" 하지 검색 가능한 필드에 포함 하는 호텔을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="3b1c9-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3b1c9-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3b1c9-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="3b1c9-988">Hello 사용 `searchMode=all` 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="3b1c9-989">이 매개 변수를 포함 하 여 기본값을 재정의 hello의 `searchMode=any`등과는 `-motel` "AND NOT" 대신 "OR NOT"을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="3b1c9-990">없이 `searchMode=all`"OR NOT"는 검색 결과 제한 하는 것이 아니라 확장 얻게 하 고이 비 직관적인 toosome 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="3b1c9-991">사용 하 여 hello 인덱스에서 문서를 찾습니다 [lucene 쿼리 구문](https://msdn.microsoft.com/library/mt589323.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="3b1c9-992">이 쿼리는 호텔 hello 범주 필드 hello 용어 "budget" 및 "리 최근에" hello 구가 포함 된 모든 검색 가능한 필드를 포함 하는 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="3b1c9-993">Hello 용어 부스트 값 (3)의 결과 "리 최근에" hello 구가 포함 된 문서는 순위가 더 높은</span><span class="sxs-lookup"><span data-stu-id="3b1c9-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="3b1c9-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="3b1c9-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="3b1c9-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="3b1c9-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="3b1c9-996">문서 조회</span><span class="sxs-lookup"><span data-stu-id="3b1c9-996">Lookup Document</span></span>
<span data-ttu-id="3b1c9-997">hello **문서 조회** Azure 검색에서 문서를 검색 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="3b1c9-998">사용자가 특정 검색 결과 클릭 하 고 해당 문서에 대 한 특정 세부 정보를 toolook 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="3b1c9-999">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-999">**Request**</span></span>

<span data-ttu-id="3b1c9-1000">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-1001">hello **문서 조회** 요청을 다음과 같이 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="3b1c9-1002">또는 hello 기존의 OData 구문을 키 조회에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="3b1c9-1003">hello 요청 URI [index name]에 포함 됩니다. [key], 인덱스에서 문서 tooretrieve를 지정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="3b1c9-1004">한 번에 하나의 문서만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1004">You can only get one document at a time.</span></span> <span data-ttu-id="3b1c9-1005">사용 하 여 **검색** tooget 단일 요청에서 여러 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="3b1c9-1006">**쿼리 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1006">**Query Parameters**</span></span>

<span data-ttu-id="3b1c9-1007">`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3b1c9-1008">지정 되지 않았거나 너무 설정 하는 경우`*`, hello 스키마에서 검색 가능한 것으로 표시 하는 모든 필드가 hello 프로젝션에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="3b1c9-1009">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-1010">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-1011">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-1012">참고:이 작업에 대 한 hello `api-version` 쿼리 매개 변수로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="3b1c9-1013">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1013">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-1014">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-1015">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-1016">문자열 값, 고유 tooyour 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3b1c9-1017">hello **문서 조회** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3b1c9-1018">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-1019">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-1020">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-1021">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1021">**Request Body**</span></span>

<span data-ttu-id="3b1c9-1022">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1022">None.</span></span>

<span data-ttu-id="3b1c9-1023">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1023">**Response**</span></span>

<span data-ttu-id="3b1c9-1024">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="3b1c9-1025">**예제**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1025">**Example**</span></span>

<span data-ttu-id="3b1c9-1026">'2' 키를 가진 hello 문서 조회</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="3b1c9-1027">OData 구문을 사용 하 여 ' 3' 키를 가진 조회 hello 문서:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="3b1c9-1028">문서 수 계산</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1028">Count Documents</span></span>
<span data-ttu-id="3b1c9-1029">hello **문서 수 계산** hello 수 검색 인덱스의 문서를 검색 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="3b1c9-1030">hello `$count` 구문 hello OData 프로토콜의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="3b1c9-1031">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1031">**Request**</span></span>

<span data-ttu-id="3b1c9-1032">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-1033">hello **문서 수 계산** hello GET 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3b1c9-1034">hello 요청 URI의에서 [index name] hello hello 서비스 tooreturn 모든 항목의 수 hello 지정 된 인덱스의 문서 컬렉션 hello에에서 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="3b1c9-1035">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-1036">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-1037">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-1038">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1038">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-1039">다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3b1c9-1040">`Accept`:이 값을 너무 설정 해야`text/plain`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="3b1c9-1041">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-1042">문자열 값, 고유 tooyour 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3b1c9-1043">hello **문서 수 계산** 요청 관리자 키 또는 쿼리 키를 지정할 수 있습니다 `api-key`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3b1c9-1044">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-1045">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-1046">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-1047">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1047">**Request Body**</span></span>

<span data-ttu-id="3b1c9-1048">없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1048">None.</span></span>

<span data-ttu-id="3b1c9-1049">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1049">**Response**</span></span>

<span data-ttu-id="3b1c9-1050">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3b1c9-1051">hello 응답 본문을 일반 텍스트로 서식이 지정 된 정수로 hello 개수 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="3b1c9-1052">제안</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1052">Suggestions</span></span>
<span data-ttu-id="3b1c9-1053">hello **제안** 부분 검색 입력을 기준으로 제안을 검색 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="3b1c9-1054">일반적으로 사용자가 검색 용어를 입력 하는 대로 검색 상자 tooprovide 미리 입력 제안에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="3b1c9-1055">제안 요청 대상 문서를 제공 하기 위한 것, 동일한 입력을 검색 하므로 hello를 제안 된 후보 문서가 여러 개이면 hello와 일치 하는 경우에 텍스트를 반복 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="3b1c9-1056">사용할 수 있습니다 `$select` tooretrieve 다른 문서 필드 (hello 문서 키 포함)는 문서는 각 제안에 대 한 hello 원본 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="3b1c9-1057">**제안** 작업이 GET 또는 POST 요청으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="3b1c9-1058">**대신 toouse 게시 하는 경우**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="3b1c9-1059">HTTP GET toocall hello를 사용 하는 경우 **제안** API 해야 toobe 인식 hello 요청 URL의 hello 길이 8KB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="3b1c9-1060">이 크기는 일반적으로 대부분의 응용 프로그램에서 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="3b1c9-1061">그러나 일부 응용 프로그램은 매우 큰 쿼리, 특히 OData 필터 식을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="3b1c9-1062">이러한 응용 프로그램의 경우 GET보다 더 많은 필터를 허용할 수 있는 HTTP POST를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="3b1c9-1063">POST, 필터에서 절 hello 수는 hello 제한 요소를 POST에 대 한 hello 요청 크기 제한 약 16MB 이므로 hello 원시 필터 문자열의 크기를 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1064">Hello POST 요청 크기 제한의 용량이 클 경우에 필터 식은 복잡 한 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="3b1c9-1065">필터 복잡성 제한에 대한 자세한 내용은 [OData 식 구문](https://msdn.microsoft.com/library/dn798921.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1066">**요청**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1066">**Request**</span></span>

<span data-ttu-id="3b1c9-1067">서비스 요청에는 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="3b1c9-1068">hello **제안** hello GET 또는 POST 메서드를 사용 하 여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="3b1c9-1069">hello 요청 URI에는 hello 인덱스 tooquery hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="3b1c9-1070">Hello 부분적으로 입력된 된 검색 용어도 등의 매개 변수는 GET 요청의 경우 hello hello 쿼리 문자열에 지정 된 한 hello 경우 POST의 본문 hello 요청에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="3b1c9-1071">모범 사례로 GET 요청을 만들 때, 기억 너무[URL로 인코드할](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) 특정 쿼리 매개 변수를 호출할 때 REST API를 직접 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="3b1c9-1072">**제안** 작업의 경우 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="3b1c9-1073">URL 인코딩은 위의 쿼리 매개 변수는 hello에만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="3b1c9-1074">실수로 URL로 인코딩할 수 있습니다 (다음의 모든 hello?)는 전체 쿼리 문자열 hello, 요청이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="3b1c9-1075">또한 URL 인코딩은 필요한 경우에 REST API를 사용 하 여 직접 가져올 hello를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="3b1c9-1076">호출할 때 필요한은 URL 인코딩 없이 **제안** POST를 사용 하 여 hello를 사용 하는 경우 [.NET 클라이언트 라이브러리](https://msdn.microsoft.com/library/dn951165.aspx), URL 인코딩을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="3b1c9-1077">**쿼리 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1077">**Query Parameters**</span></span>

<span data-ttu-id="3b1c9-1078">**제안** 은 쿼리 조건을 제공하고 검색 동작을 지정하는 여러 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="3b1c9-1079">호출할 때 이러한 매개 변수 hello URL에 쿼리 문자열을 제공 **제안** GET을 통해 및를 호출할 때 hello 요청 본문의 JSON 속성으로 **제안** POST 통해.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="3b1c9-1080">hello 일부 매개 변수의 구문에는 GET 및 POST 간에 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="3b1c9-1081">이러한 차이가 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="3b1c9-1082">`search=[string]`-hello 검색 텍스트 toouse toosuggest 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="3b1c9-1083">최소 1자가 되어야 하며 100자를 넘지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="3b1c9-1084">`highlightPreTag=[string]`(선택 사항)-toosearch 적중 항목 앞에 추가 하는 문자열 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="3b1c9-1085">`highlightPostTag`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1086">호출할 때 **제안** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3b1c9-1087">`highlightPostTag=[string]`(선택 사항)-toosearch 적중 항목을 추가 하는 문자열 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="3b1c9-1088">`highlightPreTag`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1089">호출할 때 **제안** GET를 사용 하 여 hello URL에서 예약 된 문자 (예: # 대신 %23) 퍼센트 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3b1c9-1090">`suggesterName=[string]`-hello에 지정 된 hello hello 확인 기 이름을 `suggesters` hello 인덱스 정의의 일부인 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="3b1c9-1091">이 `suggester` 에 따라 제안된 쿼리 용어를 검색할 필드가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="3b1c9-1092">자세한 내용은 [확인기](#Suggesters) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="3b1c9-1093">`fuzzy=[boolean]`(옵션, 기본값 = false)-설정 된 경우 tootrue이 API는 제안을 찾습니다 hello 검색 텍스트에 대체 되었거나 누락 된 문자는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="3b1c9-1094">이 경우 일부 시나리오에서는 검색 환경이 개선되지만, 유사 제안 검색 속도가 느려지며 리소스가 더 많이 사용되므로 성능은 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="3b1c9-1095">`searchFields=[string]`(선택 사항)-hello 목록을 쉼표로 구분 된 필드 이름 toosearch hello에 대 한 검색 텍스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="3b1c9-1096">대상 필드가 제안을 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="3b1c9-1097">`$top=#`(옵션, 기본값 = 5)-hello 제안 tooretrieve의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="3b1c9-1098">값은 1~100 사이의 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1099">POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$top` 대신 `top`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1100">`$filter=[string]`(선택 사항)-제안에 대 한 hello 문서를 필터링 하는 식으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1101">POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$filter` 대신 `filter`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1102">`$orderby=[string]`(선택 사항)-toosort hello 쉼표로 구분 된 식 결과의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="3b1c9-1103">각 식은 필드 이름 또는 호출 toohello 가능 `geo.distance()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="3b1c9-1104">각 식은 올 수 있는 `asc` tooindicated 오름차순 및 `desc` 내림차순 tooindicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="3b1c9-1105">hello 기본값은 오름차순입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1105">hello default is ascending order.</span></span> <span data-ttu-id="3b1c9-1106">`$orderby`절은 32개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1107">POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$orderby` 대신 `orderby`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1108">`$select=[string]`(선택 사항)-tooretrieve 쉼표로 구분 된 필드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3b1c9-1109">지정 하지 않으면 문서 키만 hello 및 제안 텍스트가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="3b1c9-1110">이 매개 변수를 너무 설정 하 여 모든 필드를 명시적으로 요청할 수`*`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1111">POST를 사용하여 **제안**을 호출하는 경우 이 매개 변수의 이름은 `$select` 대신 `select`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1112">`minimumCoverage`(선택 사항 기본값 too80)-0과 100 hello 쿼리 toobe 되려면에서 제안 쿼리에서 포함 되어야 하는 hello 인덱스의 hello 백분율을 나타내는 사이의 숫자를 성공으로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="3b1c9-1113">기본적으로 hello 인덱스의 80% 이상을 사용할 수 있어야 하거나 `Suggest` 503 HTTP 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="3b1c9-1114">설정한 경우 `minimumCoverage` 및 `Suggest` 성공 하면 HTTP 200을 반환 하 고 포함 한 `@search.coverage` hello에 대 한 응답 hello 쿼리에 포함 된 hello 인덱스의 hello 백분율을 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1c9-1115">이 매개 변수 tooa 값 100 검색 가용성 복제본을 하나만 사용 하 여 서비스에 대해서도 보장 하는 데 유용할 수 있습니다 보다 낮게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="3b1c9-1116">그러나 일부 일치 하는 제안은 toobe hello 결과 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="3b1c9-1117">회수 가용성, 다음의 모범 하지 toolower 보다 더 중요 한 tooyour 응용 프로그램인 경우 `minimumCoverage` 기본값인 80 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="3b1c9-1118">`api-version=[string]` (필수).</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="3b1c9-1119">hello 미리 보기 버전을 `api-version=2015-02-28-Preview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3b1c9-1120">자세한 내용 및 대체 버전은 [검색 서비스 버전 관리](http://msdn.microsoft.com/library/azure/dn864560.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3b1c9-1121">참고:이 작업에 대 한 hello `api-version` 호출 여부에 관계 없이 hello URL에 쿼리 매개 변수로 지정 **제안** GET 또는 POST입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="3b1c9-1122">**요청 헤더**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1122">**Request Headers**</span></span>

<span data-ttu-id="3b1c9-1123">hello 목록 다음 필요한 hello와 선택적 요청 헤더를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="3b1c9-1124">`api-key`: hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3b1c9-1125">문자열 값, 고유 tooyour 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3b1c9-1126">hello **제안** 요청 hello로 관리자 키 또는 쿼리 키를 지정할 수 `api-key`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="3b1c9-1127">Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3b1c9-1128">Hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello Azure 포털의에서 서비스 대시보드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3b1c9-1129">참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3b1c9-1130">**요청 본문**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1130">**Request Body**</span></span>

<span data-ttu-id="3b1c9-1131">GET의 경우: 없음.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1131">For GET: None.</span></span>

<span data-ttu-id="3b1c9-1132">POST의 경우:</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="3b1c9-1133">**응답**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1133">**Response**</span></span>

<span data-ttu-id="3b1c9-1134">상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="3b1c9-1135">Hello 프로젝션 옵션을 사용 하는 tooretrieve 필드 hello 배열의 각 요소에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="3b1c9-1136">**예제**</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1136">**Example**</span></span>

<span data-ttu-id="3b1c9-1137">Hello 부분 검색 입력 'l u x' 인 제안 5 개 검색</span><span class="sxs-lookup"><span data-stu-id="3b1c9-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
