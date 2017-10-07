---
title: "Azure 검색의 aaaHow toopage 검색 결과 | Microsoft Docs"
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
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="b9358-103">Azure 검색의 toopage 검색 결과 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b9358-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="b9358-104">이 문서는 어떻게 toouse hello Azure 검색 서비스 REST API tooimplement 표준 요소 검색 결과 탐색 총 개수, 문서 검색, 정렬 순서 등의 페이지에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="b9358-105">아래에서 설명한 모든 경우에 데이터 나 정보 tooyour 검색 결과 페이지를 제공 하는 페이지와 관련 된 옵션은 hello를 통해 지정 됩니다 [검색 문서](http://msdn.microsoft.com/library/azure/dn798927.aspx) 전송 된 요청 tooyour Azure 검색 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="b9358-106">요청은 GET 명령, 경로 및 알리는 hello 서비스 기능 요청 되는 쿼리 매개 변수 및 어떻게 tooformulate hello 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="b9358-107">유효한 요청에는 서비스 URL 및 경로, HTTP 동사, `api-version` 등과 같은 요소의 숫자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="b9358-108">간단한 설명을 위해 관련 toopagination 않은 hello 예제 toohighlight 정당한 hello 구문을 잘립니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="b9358-109">Hello를 참조 하십시오 [Azure 검색 서비스 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) 요청 구문에 대 한 세부 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="b9358-110">총 적중 수 및 페이지 수</span><span class="sxs-lookup"><span data-stu-id="b9358-110">Total hits and Page Counts</span></span>
<span data-ttu-id="b9358-111">기본 toovirtually 모든 검색 페이지는 hello 총 결과 수는 쿼리에서 반환 하 고 더 작은 청크에서 결과 반환 하는 것을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="b9358-112">Azure 검색을 사용 하 여 hello `$count`, `$top`, 및 `$skip` 매개 변수 tooreturn 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="b9358-113">hello 다음 보여 주는 예제는 예제 요청으로 반환 하는 총 방문 횟수에 대 한 `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="b9358-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="b9358-114">15의 그룹에 대 한 문서를 검색 고도 hello 총 방문 횟수 hello 첫 페이지부터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="b9358-115">둘 다 필요 하며 결과 뿐 아니라 `$top` 및 `$skip`여기서 `$top` 개수 항목 tooreturn 일괄 처리를 지정 하 고 `$skip` 항목 tooskip 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="b9358-116">Hello 다음 예에서는, 각 페이지에 다음 15 개 항목이 hello 표시로 표시 됩니다 hello에 hello 증분 점프 `$skip` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="b9358-117">레이아웃</span><span class="sxs-lookup"><span data-stu-id="b9358-117">Layout</span></span>
<span data-ttu-id="b9358-118">검색 결과 페이지에 미리 보기 이미지, 필드의 하위 집합 및 링크 tooa 정식 제품 페이지 tooshow 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="b9358-119">Azure 검색에서는 사용 `$select` 조회 명령 tooimplement이이 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="b9358-120">타일 식된 레이아웃에 대 한 필드의 하위 집합 tooreturn:</span><span class="sxs-lookup"><span data-stu-id="b9358-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="b9358-121">이미지 및 미디어 파일은 직접 검색할 수 없습니다 및 Azure Blob 저장소 tooreduce 비용 등의 다른 저장소 플랫폼에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="b9358-122">Hello 인덱스 및 문서에 외부 콘텐츠 hello의 hello URL 주소를 저장 하는 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="b9358-123">다음 이미지 참조로 hello 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="b9358-124">hello URL toohello 이미지 hello 문서에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="b9358-125">제품 설명에 대 한 페이지 tooretrieve는 **onClick** 이벤트를 사용 하 여 [문서 조회](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass hello 문서 tooretrieve의 hello 키에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="b9358-126">hello 키의 데이터 형식이 hello `Edm.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="b9358-127">이 예제에서는 *246810*입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="b9358-128">관련성, 등급, 또는 가격 기준으로 정렬</span><span class="sxs-lookup"><span data-stu-id="b9358-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="b9358-129">정렬 순서 toorelevance, 기본 하지만 고객을 다른 순위 순서로 기존 결과 신속 하 게 나타나거나 수 있도록 쉽게 사용할 수 있는 일반적인 toomake 대체 정렬 순서는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="b9358-130">Azure 검색, 정렬 기준으로 hello `$orderby` 으로 인덱싱된 모든 필드에 대 한 식`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="b9358-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="b9358-131">관련성은 프로필 점수 매기기와 강력하게 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="b9358-132">사용할 수 있습니다 hello 기본 점수 매기기 사용 텍스트 분석 및 통계 toorank 순서에 모든 결과 더 높은 점수가 더 많거나 더 강력한 일치 toodocuments 검색어를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="b9358-133">대체 정렬 순서는 일반적으로 연관 **onClick** 다시 tooa 메서드 호출 하는 이벤트 hello 정렬 순서를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="b9358-134">예를 들어 이 페이지 요소를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="b9358-135">Hello 선택한 정렬 옵션을 입력으로 받아들이고 hello 조건에 연결 된 해당 옵션에 대 한 정렬된 된 목록을 반환 하는 메서드를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="b9358-136">Hello 기본 점수 매기기은 다양 한 시나리오에 대 한 충분 한, 대신 사용자 지정 점수 매기기 프로필의 관련성을으로 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="b9358-137">사용자 지정 점수 매기기 프로필 더 좋습니다 tooyour 비즈니스 있는 방식으로 tooboost 항목을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="b9358-138">자세한 내용은 [점수 매기기 프로필 추가](http://msdn.microsoft.com/library/azure/dn798928.aspx) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b9358-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="b9358-139">패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="b9358-139">Faceted navigation</span></span>
<span data-ttu-id="b9358-140">검색 탐색이 대개 hello 쪽 또는 페이지의 위쪽에 위치 하는 결과 페이지에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="b9358-141">Azure 검색에서는 미리 정의된 필터에 따라 패싯 탐색이 자기 주도 탐색을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="b9358-142">자세한 내용은 [Azure 탐색의 패싯 탐색](search-faceted-navigation.md) 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b9358-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="b9358-143">Hello 페이지 수준에서 필터</span><span class="sxs-lookup"><span data-stu-id="b9358-143">Filters at hello page level</span></span>
<span data-ttu-id="b9358-144">와 함께 필터 식에 삽입할 수 솔루션 디자인 특정 유형의 콘텐츠 (예를 들어 온라인 소매상 응용 프로그램 hello hello 페이지 위쪽에 나열 된 부서 있는)에 대 한 전용된 검색 페이지를 포함 하는 경우는 **onClick** 이벤트 tooopen 대 상태에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="b9358-145">검색 식의 사용 여부에 관계 없이 필터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="b9358-146">예를 들어 hello 다음 요청은 필터링 할 브랜드 이름으로 일치 하는 문서에만 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9358-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="b9358-147">`$filter` 식에 대한 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b9358-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="b9358-148">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b9358-148">See Also</span></span>
* [<span data-ttu-id="b9358-149">Azure 검색 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="b9358-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="b9358-150">인덱스 작업</span><span class="sxs-lookup"><span data-stu-id="b9358-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="b9358-151">문서 작업</span><span class="sxs-lookup"><span data-stu-id="b9358-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="b9358-152">Azure 검색에 대한 비디오 및 자습서</span><span class="sxs-lookup"><span data-stu-id="b9358-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="b9358-153">Azure 검색의 패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="b9358-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
