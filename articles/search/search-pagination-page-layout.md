---
title: "Azure Search에서 검색 결과를 페이징하는 방법 | Microsoft Docs"
description: "Microsoft Azure에서 호스팅되는 클라우드 검색 서비스인 Azure 검색에서의 페이징"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="ed1db-103">Azure 검색에서 검색 결과를 페이징하는 방법</span><span class="sxs-lookup"><span data-stu-id="ed1db-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="ed1db-104">이 문서는 총 횟수, 문서 검색, 정렬 순서, 탐색과 같은 검색 결과 페이지의 표준 요소를 구현하기 위한 Azure 검색 서비스의 사용 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="ed1db-105">아래에서 설명한 모든 경우에 데이터 또는 정보를 검색 결과 페이지에 적용하는 페이지 관련 옵션은 Azure 검색 서비스에 전송된 [문서 검색](http://msdn.microsoft.com/library/azure/dn798927.aspx) 요청을 통해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="ed1db-106">요청에는 GET 명령, 경로 및 서비스에 필요한 것과 응답을 작성하는 방법을 서비스에 알려주는 쿼리 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="ed1db-107">유효한 요청에는 서비스 URL 및 경로, HTTP 동사, `api-version` 등과 같은 요소의 숫자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="ed1db-108">요약하자면, 페이지 매김에 관련된 구문만 강조하기 위해 예제를 잘라냈습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="ed1db-109">요청 구분에 대한 자세한 설명서는 [Azure 검색 서비스 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed1db-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="ed1db-110">총 적중 수 및 페이지 수</span><span class="sxs-lookup"><span data-stu-id="ed1db-110">Total hits and Page Counts</span></span>
<span data-ttu-id="ed1db-111">쿼리에서 반환된 결과의 총 수를 표시한 후 해당 결과를 더 작은 청크로 반환하는 것은 모든 검색 페이지의 기반이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="ed1db-112">Azure 검색에서는 `$count`, `$top` 및 `$skip` 매개 변수를 사용하여 이러한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="ed1db-113">다음 예제에서는 `@OData.count`(으)로 반환되는 총 적중 수에 대한 샘플 요청을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="ed1db-114">첫 페이지에서 시작하여 15개 그룹에 대한 문서를 검색하고, 총 적중 수도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="ed1db-115">페이지 매김 결과에는 `$top`이(가) 일괄적으로 반환할 항목의 수를 지정하고 `$skip`은(는) 건너뛸 항목 수를 지정하는 `$top` 및 `$skip`이(가) 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="ed1db-116">다음 예제에서는 각 페이지에서 `$skip` 매개 변수로 증분 점프하여 증가하는 다음 15개 항목을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="ed1db-117">레이아웃</span><span class="sxs-lookup"><span data-stu-id="ed1db-117">Layout</span></span>
<span data-ttu-id="ed1db-118">검색 결과 페이지에서 축소판 이미지, 필드의 하위 집합 및 전체 제품 페이지에 대한 링크를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="ed1db-119">Azure 검색에서는 `$select` 및 조회 명령을 사용하여 이 환경을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="ed1db-120">타일화된 레이아웃에 대한 필드의 하위 집합을 반환하는 방법:</span><span class="sxs-lookup"><span data-stu-id="ed1db-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="ed1db-121">이미지 및 미디어 파일은 직접 검색할 수 없으며, 비용을 줄이기위해 Azure Blob 저장소와 같은 다른 저장소 플랫폼에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="ed1db-122">인덱스 및 문서에서 외부 콘텐츠의 URL 주소를 저장하는 필드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="ed1db-123">그러면 필드를 이미지 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="ed1db-124">이미지에 대한 URL은 문서에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="ed1db-125">**onClick** 이벤트에 대한 제품 설명 페이지를 검색하려면 [문서 조회](http://msdn.microsoft.com/library/azure/dn798929.aspx) 를 사용하여 검색할 문서의 키에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="ed1db-126">키의 데이터 형식은 `Edm.String`입니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="ed1db-127">이 예제에서는 *246810*입니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="ed1db-128">관련성, 등급, 또는 가격 기준으로 정렬</span><span class="sxs-lookup"><span data-stu-id="ed1db-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="ed1db-129">정렬 순서는 종종 기본적으로 관련도에 따르지만, 고객이 다른 순위 순서로 기존 결과를 신속하게 바꿀 수 있도록 대체 정렬 순서를 준비해 놓는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="ed1db-130">Azure 검색에서는 `"Sortable": true.`(으)로 인덱싱되는 모든 필드에 대해 `$orderby` 식에 기반하여 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="ed1db-131">관련성은 프로필 점수 매기기와 강력하게 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="ed1db-132">검색 단어가 더 많이 또는 더 강력하게 일치되는 문서에 더 높은 점수를 매기는 텍스트 분석 및 통계에 따라 모든 결과의 순서를 정하는 기본 점수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="ed1db-133">대체 정렬 순서는 일반적으로 정렬 순서를 작성하는 메서드를 다시 호출하는 **onClick** 이벤트에 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="ed1db-134">예를 들어 이 페이지 요소를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="ed1db-135">선택한 정렬 옵션을 입력으로 받아 메서드를 생성하고 해당 옵션과 관련된 조건에 대한 정렬된 목록을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="ed1db-136">기본 점수 매기기는 다양한 시나리오에 적용할 수 있으므로 대신 사용자 지정 점수 매기기 프로필의 관련성에 기반하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="ed1db-137">사용자 지정 점수 매기기 프로필은 비즈니스에 더 많은 이점을 제공하는 항목 강화 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="ed1db-138">자세한 내용은 [점수 매기기 프로필 추가](http://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed1db-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="ed1db-139">패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="ed1db-139">Faceted navigation</span></span>
<span data-ttu-id="ed1db-140">종종 페이지의 옆쪽 또는 위쪽에 있는 검색 탐색은 결과 페이지에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="ed1db-141">Azure 검색에서는 미리 정의된 필터에 따라 패싯 탐색이 자기 주도 탐색을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="ed1db-142">자세한 내용은 [Azure 탐색의 패싯 탐색](search-faceted-navigation.md) 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed1db-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="ed1db-143">페이지 수준의 필터</span><span class="sxs-lookup"><span data-stu-id="ed1db-143">Filters at the page level</span></span>
<span data-ttu-id="ed1db-144">솔루션 디자인이 특정 유형의 콘텐츠에 대한 전용 검색 페이지를 포함하는 경우(예를 들어 페이지 위쪽에 부서 목록이 있는 온라인 소매상 응용 프로그램), 필터식과 함께 미리 필터링된 상태로 페이지를 여는 **onClick** 이벤트를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="ed1db-145">검색 식의 사용 여부에 관계 없이 필터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="ed1db-146">예를 들어 다음 요청은 브랜드 이름으로 필터링하고 일치하는 문서만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed1db-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="ed1db-147">`$filter` 식에 대한 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed1db-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed1db-148">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ed1db-148">See Also</span></span>
* [<span data-ttu-id="ed1db-149">Azure 검색 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="ed1db-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="ed1db-150">인덱스 작업</span><span class="sxs-lookup"><span data-stu-id="ed1db-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="ed1db-151">문서 작업</span><span class="sxs-lookup"><span data-stu-id="ed1db-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="ed1db-152">Azure 검색에 대한 비디오 및 자습서</span><span class="sxs-lookup"><span data-stu-id="ed1db-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="ed1db-153">Azure 검색의 패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="ed1db-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
