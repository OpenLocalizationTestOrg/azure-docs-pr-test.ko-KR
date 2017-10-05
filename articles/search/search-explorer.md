---
title: "인덱스 쿼리(포털 - Azure Search) | Microsoft Docs"
description: "Azure 포털의 검색 탐색기에서 검색 쿼리를 실행합니다."
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a><span data-ttu-id="4e28d-103">Azure Portal에서 Search Explorer를 사용하여 Azure Search 인덱스 쿼리</span><span class="sxs-lookup"><span data-stu-id="4e28d-103">Query an Azure Search index using Search Explorer in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e28d-104">개요</span><span class="sxs-lookup"><span data-stu-id="4e28d-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="4e28d-105">포털</span><span class="sxs-lookup"><span data-stu-id="4e28d-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="4e28d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4e28d-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="4e28d-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="4e28d-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="4e28d-108">이 문서에서는 Azure Portal에서 **Search Explorer**를 사용하여 Azure Search 인덱스를 쿼리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-108">This article shows you how to query an Azure Search index using **Search Explorer** in the Azure portal.</span></span> <span data-ttu-id="4e28d-109">Search Explorer를 사용하여 서비스에서 기존 인덱스에 단일 또는 전체 Lucene 쿼리 문자열을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-109">You can use Search Explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="4e28d-110">서비스 대시보드 열기</span><span class="sxs-lookup"><span data-stu-id="4e28d-110">Open the service dashboard</span></span>
1. <span data-ttu-id="4e28d-111">[Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)의 왼쪽에 있는 점프 표시줄에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-111">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="4e28d-112">Azure Search 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="4e28d-113">인덱스 선택</span><span class="sxs-lookup"><span data-stu-id="4e28d-113">Select an index</span></span>

<span data-ttu-id="4e28d-114">**인덱스** 타일에서 검색하려는 인덱스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-114">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="4e28d-115">Search Explorer 열기</span><span class="sxs-lookup"><span data-stu-id="4e28d-115">Open Search Explorer</span></span>

<span data-ttu-id="4e28d-116">Search Explorer 타일을 클릭하여 검색 표시줄 및 결과 창을 슬라이드로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-116">Click on the Search Explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="4e28d-117">검색 시작</span><span class="sxs-lookup"><span data-stu-id="4e28d-117">Start searching</span></span>

<span data-ttu-id="4e28d-118">Search Explorer를 사용하는 경우 [쿼리 매개 변수](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)를 지정하여 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-118">When using the Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="4e28d-119">**쿼리 문자열**에서 쿼리를 입력한 다음 **검색** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="4e28d-120">쿼리 문자열은 적절한 요청 URL로 자동으로 구문 분석되어 Azure Search REST API에 대해 HTTP 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-120">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="4e28d-121">유효한 단일 또는 전체 Lucene 쿼리 구문을 사용하여 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-121">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="4e28d-122">`*` 문자는 임의의 순서로 모든 문서를 반환하는 비어 있거나 지정되지 않은 검색과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-122">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="4e28d-123">**결과**에서 쿼리 결과는 원시 JSON으로 표시되며 이는 프로그래밍 방식으로 요청을 실행하는 경우 HTTP 응답 본문에서 반환되는 페이로드와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-123">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="4e28d-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e28d-124">Next steps</span></span>

<span data-ttu-id="4e28d-125">다음 리소스는 추가 쿼리 구문 정보 및 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e28d-125">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="4e28d-126">단순 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="4e28d-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="4e28d-127">Lucene 쿼리 구문</span><span class="sxs-lookup"><span data-stu-id="4e28d-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="4e28d-128">Lucene 쿼리 구문 예제</span><span class="sxs-lookup"><span data-stu-id="4e28d-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="4e28d-129">OData 필터 식 구문</span><span class="sxs-lookup"><span data-stu-id="4e28d-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 