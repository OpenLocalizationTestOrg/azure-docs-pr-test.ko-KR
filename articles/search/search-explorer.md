---
title: "aaa \"는 인덱스 (포털-Azure 검색) 쿼리하여 | \"Microsoft Docs"
description: "Hello Azure 포털의 검색 탐색기에서 검색 쿼리를 실행 합니다."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="bfb26-103">검색 탐색기를 사용 하 여 hello Azure 포털에서에서 Azure 검색 인덱스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfb26-104">개요</span><span class="sxs-lookup"><span data-stu-id="bfb26-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="bfb26-105">포털</span><span class="sxs-lookup"><span data-stu-id="bfb26-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="bfb26-106">.NET</span><span class="sxs-lookup"><span data-stu-id="bfb26-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="bfb26-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="bfb26-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="bfb26-108">이 문서에서는 어떻게 tooquery Azure 검색 인덱스를 사용 하 여 **탐색기 검색** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="bfb26-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="bfb26-109">서비스에서 검색 탐색기 toosubmit 전체 또는 단순 Lucene 쿼리 문자열 tooany 기존 인덱스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="bfb26-110">열기 hello 서비스 대시보드</span><span class="sxs-lookup"><span data-stu-id="bfb26-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="bfb26-111">클릭 **모든 리소스** hello hello의 왼쪽에 hello 점프 막대 [Azure 포털](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="bfb26-112">Azure Search 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="bfb26-113">인덱스 선택</span><span class="sxs-lookup"><span data-stu-id="bfb26-113">Select an index</span></span>

<span data-ttu-id="bfb26-114">선택 hello 인덱스 toosearch hello에서 원하는 **인덱스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="bfb26-115">Search Explorer 열기</span><span class="sxs-lookup"><span data-stu-id="bfb26-115">Open Search Explorer</span></span>

<span data-ttu-id="bfb26-116">Hello 탐색기 검색 타일 tooslide 열기 hello 검색 표시줄을 클릭 하 고 결과 창.</span><span class="sxs-lookup"><span data-stu-id="bfb26-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="bfb26-117">검색 시작</span><span class="sxs-lookup"><span data-stu-id="bfb26-117">Start searching</span></span>

<span data-ttu-id="bfb26-118">Hello 검색 탐색기를 사용 하는 경우 지정할 수 있습니다 [쿼리 매개 변수](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="bfb26-119">**쿼리 문자열**에서 쿼리를 입력한 다음 **검색** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="bfb26-120">hello 쿼리 문자열은 자동으로 구문 분석 hello 적절 한 요청으로 URL toosubmit hello Azure 검색 REST API에 대 한 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="bfb26-121">모든 유효한 전체 또는 단순 Lucene 쿼리 구문을 toocreate hello 요청을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="bfb26-122">hello `*` 문자는 임의의 순서로 모든 문서를 반환 하는 해당 tooan 비어 있거나 지정 되지 않은 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="bfb26-123">**결과**, 쿼리 결과 원시 JSON으로 표시 됩니다. 동일한 toohello 페이로드 반환 프로그래밍 방식으로 요청을 실행 하는 경우에 HTTP 응답 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="bfb26-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfb26-124">Next steps</span></span>

<span data-ttu-id="bfb26-125">다음 리소스는 hello 추가 쿼리 구문 정보 및 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfb26-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="bfb26-126">단순 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="bfb26-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="bfb26-127">Lucene 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="bfb26-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="bfb26-128">Lucene 쿼리 구문 예제</span><span class="sxs-lookup"><span data-stu-id="bfb26-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="bfb26-129">OData 필터 식 구문</span><span class="sxs-lookup"><span data-stu-id="bfb26-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 