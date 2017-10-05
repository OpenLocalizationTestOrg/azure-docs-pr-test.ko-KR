---
title: "Fiddler를 사용하여 Azure 검색 REST API를 평가 및 테스트하는 방법 | Microsoft Docs"
description: "코드를 작성할 필요가 없는 Fiddler를 사용하여 Azure 검색 가용성을 확인하고 REST API를 사용해 봅니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="4d76b-103">Fiddler를 사용하여 Azure 검색 REST API를 평가 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4d76b-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="4d76b-104">개요</span><span class="sxs-lookup"><span data-stu-id="4d76b-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="4d76b-105">검색 탐색기</span><span class="sxs-lookup"><span data-stu-id="4d76b-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="4d76b-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="4d76b-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="4d76b-107">.NET</span><span class="sxs-lookup"><span data-stu-id="4d76b-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="4d76b-108">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="4d76b-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="4d76b-109">이 문서에서는 [Telerik에서 무료로 다운로드](http://www.telerik.com/fiddler)할 수 있는 Fiddler를 사용하여 HTTP 요청을 실행하고 코드를 작성할 필요 없이 Azure 검색 REST API를 사용하여 응답을 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="4d76b-110">Azure 검색은 Microsoft Azure에서 완벽하게 관리되는 호스트된 클라우드 검색 서비스이며 .NET 및 REST API를 통해 쉽게 프로그래밍 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="4d76b-111">Azure 검색 서비스 REST API는 [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="4d76b-112">아래 단계에서는 인덱스를 만들고 문서를 업로드한 다음 인덱스를 쿼리하고 시스템에 서비스 정보를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="4d76b-113">이러한 단계를 완료하려면 Azure 검색 서비스 및 `api-key`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="4d76b-114">시작하는 방법에 대한 지침은 [포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="4d76b-115">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="4d76b-115">Create an index</span></span>
1. <span data-ttu-id="4d76b-116">Fiddler를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-116">Start Fiddler.</span></span> <span data-ttu-id="4d76b-117">**File** 메뉴에서 **Capture Traffic**을 해제하여 현재 작업과 관련 없는 HTTP 활동을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="4d76b-118">**작성기** 탭에서 다음 스크린샷과 같은 요청을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="4d76b-119">**PUT**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-119">Select **PUT**.</span></span>
4. <span data-ttu-id="4d76b-120">서비스 URL을 지정하는 URL, 요청 특성 및 api-version을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="4d76b-121">다음 몇 가지 사항에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="4d76b-122">HTTPS를 접두사로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="4d76b-123">요청 특성은 "/indexes/hotels"입니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="4d76b-124">그러면 검색에서 'hotels'라는 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="4d76b-125">api-version은 소문자이며 "?api-version=2016-09-01"로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="4d76b-126">Azure 검색은 주기적으로 업데이트를 배포하므로 API 버전이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="4d76b-127">드물긴 하지만 서비스 업데이트에서 새로운 API 변경 사항을 소개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="4d76b-128">이러한 이유로 Azure 검색은 각 요청에 API 버전이 필요하므로 어떤 것을 사용할지 전체를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="4d76b-129">다음 예제와 같은 전체 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="4d76b-130">호스트와 api-key를 해당 서비스에 유효한 값으로 바꾸어 요청 헤더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="4d76b-131">요청 본문에 인덱스 정의를 구성하는 필드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-131">In Request Body, paste in the fields that make up the index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="4d76b-132">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-132">Click **Execute**.</span></span>

<span data-ttu-id="4d76b-133">몇 초 후에 인덱스가 성공적으로 만들어졌음을 나타내는 HTTP 201 응답이 검색 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="4d76b-134">HTTP 504가 표시될 경우 URL이 HTTPS를 지정하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="4d76b-135">HTTP 400 또는 404가 표시되는 경우 요청 본문에서 복사/붙여 넣기 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="4d76b-136">HTTP 403은 대개 api-key에 문제가 있음을 나타냅니다(잘못된 키 또는 api-key 지정 방법과 관련된 구문 문제).</span><span class="sxs-lookup"><span data-stu-id="4d76b-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="4d76b-137">문서 로드</span><span class="sxs-lookup"><span data-stu-id="4d76b-137">Load documents</span></span>
<span data-ttu-id="4d76b-138">**작성기** 탭에서 문서 게시 요청은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="4d76b-139">요청 본문에 4개 호텔에 대한 검색 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="4d76b-140">**POST**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-140">Select **POST**.</span></span>
2. <span data-ttu-id="4d76b-141">HTTPS, 서비스 URL, "/indexes/<'indexname'>/docs/index?api-version=2016-09-01" 순으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="4d76b-142">다음 예제와 같은 전체 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="4d76b-143">요청 헤더는 이전과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-143">Request Header should be the same as before.</span></span> <span data-ttu-id="4d76b-144">호스트와 api-key를 해당 서비스에 유효한 값으로 바꾼 것에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="4d76b-145">요청 본문에 호텔 인덱스에 추가될 문서 4개가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-145">The Request Body contains four documents to be added to the hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be the one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="4d76b-146">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-146">Click **Execute**.</span></span>

<span data-ttu-id="4d76b-147">몇 초 후에 HTTP 200 응답이 검색 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="4d76b-148">이는 문서가 성공적으로 만들어졌음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="4d76b-149">207이 표시될 경우 하나 이상의 문서를 업로드하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="4d76b-150">404가 표시될 경우 요청의 헤더 또는 본문에 구문 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="4d76b-151">인덱스 쿼리</span><span class="sxs-lookup"><span data-stu-id="4d76b-151">Query the index</span></span>
<span data-ttu-id="4d76b-152">이제 인덱스와 문서가 로드되었으므로 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="4d76b-153">**작성기** 탭에서 서비스를 쿼리하는 **GET** 명령은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="4d76b-154">**GET**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-154">Select **GET**.</span></span>
2. <span data-ttu-id="4d76b-155">HTTPS, 서비스 URL, "/indexes/<'indexname'>/docs?", 쿼리 매개 변수 순으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="4d76b-156">예를 들어 샘플 호스트 이름을 해당 서비스에 유효한 이름으로 바꾸어 다음 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="4d76b-157">이 쿼리는 "motel" 용어를 검색하고 등급에 대한 패싯 범주를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="4d76b-158">요청 헤더는 이전과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-158">Request Header should be the same as before.</span></span> <span data-ttu-id="4d76b-159">호스트와 api-key를 해당 서비스에 유효한 값으로 바꾼 것에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="4d76b-160">응답 코드는 200이고, 다음 스크린샷과 같은 응답 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="4d76b-161">다음 예제 쿼리는 MSDN의 [검색 인덱스 작업(Azure 검색 API)](http://msdn.microsoft.com/library/dn798927.aspx) 에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="4d76b-162">이 항목의 많은 예제 쿼리에는 공백이 포함되어 있으며, 공백은 Fiddler에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="4d76b-163">Fiddler에서 쿼리를 시도하기에 앞서, 쿼리 문자열을 붙여 넣기 전에 각 공백을 + 문자로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="4d76b-164">**공백을 바꾸기 전:**</span><span class="sxs-lookup"><span data-stu-id="4d76b-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="4d76b-165">**공백을 +로 바꾼 후:**</span><span class="sxs-lookup"><span data-stu-id="4d76b-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="4d76b-166">시스템 쿼리</span><span class="sxs-lookup"><span data-stu-id="4d76b-166">Query the system</span></span>
<span data-ttu-id="4d76b-167">시스템을 쿼리하여 문서 수와 저장소 사용을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="4d76b-168">**작성기** 탭에서 요청은 다음과 유사하고, 응답에서 문서 수와 사용된 공간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="4d76b-169">**GET**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-169">Select **GET**.</span></span>
2. <span data-ttu-id="4d76b-170">해당 서비스 URL과 그 뒤에 "/indexes/hotels/stats?api-version=2016-09-01"을 포함하는 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="4d76b-171">호스트와 api-key를 해당 서비스에 유효한 값으로 바꾸어 요청 헤더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="4d76b-172">요청 본문을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="4d76b-173">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-173">Click **Execute**.</span></span> <span data-ttu-id="4d76b-174">세션 목록에 HTTP 200 상태 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="4d76b-175">명령에 대해 게시할 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="4d76b-176">**검사기** 탭과 **헤더** 탭을 차례로 클릭하고 JSON 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="4d76b-177">문서 수와 저장소 크기(KB)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d76b-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d76b-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d76b-178">Next steps</span></span>
<span data-ttu-id="4d76b-179">Azure 검색을 관리 및 사용하는 코드 없는 접근 방식은 [Azure에서 검색 서비스 관리](search-manage.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d76b-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
