---
title: "Azure Data Catalog에서 데이터 원본을 검색하는 방법 | Microsoft Docs"
description: "이 문서는 검색 및 필터링을 포함하는 Azure Data Catalog 및 Azure Data Catalog 포털의 적중 항목 강조 표시 기능을 사용하여 등록된 데이터 자산을 검색하는 방법을 강조 표시합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 9ff67dcb5ecb00440f73f979fd8d2b79a570c674
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-discover-data-sources-in-azure-data-catalog"></a><span data-ttu-id="756f4-103">Azure Data Catalog에서 데이터 원본을 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="756f4-103">How to discover data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="756f4-104">소개</span><span class="sxs-lookup"><span data-stu-id="756f4-104">Introduction</span></span>
<span data-ttu-id="756f4-105">Azure Data Catalog는 기업 데이터 원본의 등록 시스템 및 검색 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="756f4-106">다시 말해서 데이터 카탈로그는 사람들이 데이터 원본을 검색하고 이해하고 사용하도록 도우면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="756f4-107">데이터 카탈로그를 사용하여 데이터 원본이 등록되면 해당 메타데이터는 서비스로 인덱싱되어 사용자가 쉽게 검색하여 필요한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-107">After a data source is registered with Data Catalog, its metadata is indexed by the service, so that you can easily search to discover the data you need.</span></span>

## <a name="searching-and-filtering"></a><span data-ttu-id="756f4-108">검색 및 필터링</span><span class="sxs-lookup"><span data-stu-id="756f4-108">Searching and filtering</span></span>
<span data-ttu-id="756f4-109">데이터 카탈로그에서 검색은 검색 및 필터링이라는 두 가지 기본 메커니즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-109">Discovery in Data Catalog uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="756f4-110">검색은 직관적이고 강력하게 설계되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-110">Searching is designed to be both intuitive and powerful.</span></span> <span data-ttu-id="756f4-111">기본적으로 검색 용어는 사용자가 제공한 주석을 포함하여 카탈로그의 모든 속성과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-111">By default, search terms are matched against any property in the catalog, including user-provided annotations.</span></span>

<span data-ttu-id="756f4-112">필터링은 검색을 보완하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-112">Filtering is designed to complement searching.</span></span> <span data-ttu-id="756f4-113">전문가, 데이터 원본 유형, 개체 유형 및 태그 등의 특정 특성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-113">You can select specific characteristics such as experts, data source type, object type, and tags.</span></span> <span data-ttu-id="756f4-114">일치하는 데이터 자산만을 볼 수 있으며 일치하는 자산으로 검색 결과 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-114">You can view only matching data assets, and constrain search results to matching assets.</span></span>

<span data-ttu-id="756f4-115">검색 및 필터링 조합을 사용하여 데이터 카탈로그로 등록된 데이터 원본으로 빠르게 이동하여 필요한 데이터 원본을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-115">By using a combination of searching and filtering, you can quickly navigate the data sources that have been registered with Data Catalog to discover the data sources you need.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="756f4-116">검색 구문</span><span class="sxs-lookup"><span data-stu-id="756f4-116">Search syntax</span></span>
<span data-ttu-id="756f4-117">기본 무료 텍스트 검색은 단순하고 직관적이지만 사용자는 데이터 카탈로그의 검색 구문을 사용하여 검색 결과를 더 잘 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-117">Although the default free text search is simple and intuitive, you can also use Data Catalog search syntax for greater control over the search results.</span></span> <span data-ttu-id="756f4-118">데이터 카탈로그는 다음과 같은 기법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-118">Data Catalog search supports the following techniques:</span></span>

| <span data-ttu-id="756f4-119">기법</span><span class="sxs-lookup"><span data-stu-id="756f4-119">Technique</span></span> | <span data-ttu-id="756f4-120">사용</span><span class="sxs-lookup"><span data-stu-id="756f4-120">Use</span></span> | <span data-ttu-id="756f4-121">예</span><span class="sxs-lookup"><span data-stu-id="756f4-121">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="756f4-122">기본 검색</span><span class="sxs-lookup"><span data-stu-id="756f4-122">Basic search</span></span> |<span data-ttu-id="756f4-123">기본 검색은 하나 이상의 검색 용어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-123">Basic search that uses one or more search terms.</span></span> <span data-ttu-id="756f4-124">결과는 지정된 하나 이상의 용어와 속성에 대해 일치하는 모든 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-124">Results are any assets that match any property with one or more of the terms specified.</span></span> |`sales data` |
| <span data-ttu-id="756f4-125">속성 범위</span><span class="sxs-lookup"><span data-stu-id="756f4-125">Property scoping</span></span> |<span data-ttu-id="756f4-126">지정된 속성에서 일치하는 검색 용어가 있는 데이터 원본만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-126">Return only data sources where the search term is matched with the specified property.</span></span> |`name:finance` |
| <span data-ttu-id="756f4-127">부울 연산자</span><span class="sxs-lookup"><span data-stu-id="756f4-127">Boolean operators</span></span> |<span data-ttu-id="756f4-128">부울 연산을 사용하여 검색을 확대하거나 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-128">Broaden or narrow a search by using Boolean operations.</span></span> |`finance NOT corporate` |
| <span data-ttu-id="756f4-129">괄호로 그룹화</span><span class="sxs-lookup"><span data-stu-id="756f4-129">Grouping with parenthesis</span></span> |<span data-ttu-id="756f4-130">특별히 부울 연산자와 함께 논리적 격리를 수행하도록 쿼리의 일부를 그룹화하기 위해 괄호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-130">Use parentheses to group parts of the query to achieve logical isolation, especially in conjunction with Boolean operators.</span></span> |`name:finance AND (tags:Q1 OR tags:Q2)` |
| <span data-ttu-id="756f4-131">비교 연산자</span><span class="sxs-lookup"><span data-stu-id="756f4-131">Comparison operators</span></span> |<span data-ttu-id="756f4-132">숫자 및 날짜 데이터 유형이 있는 속성에 대한 일치가 아닌 비교를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-132">Use comparisons other than equality for properties that have numeric and date data types.</span></span> |`modifiedTime > "11/05/2014"` |

<span data-ttu-id="756f4-133">카탈로그 데이터 검색에 대한 자세한 내용은 [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="756f4-133">For more information about Data Catalog search, see the [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) article.</span></span>

## <a name="hit-highlighting"></a><span data-ttu-id="756f4-134">적중 항목 강조 표시</span><span class="sxs-lookup"><span data-stu-id="756f4-134">Hit highlighting</span></span>
<span data-ttu-id="756f4-135">검색 결과를 볼 때 데이터 자산 이름, 설명 및 태그와 같은 지정된 검색 용어와 일치하는 표시된 모든 속성은 지정된 데이터 자산이 지정된 검색에서 반환된 이유를 쉽게 확인할 수 있도록 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-135">When you view search results, any displayed properties that match the specified search terms (such as the data asset name, description, and tags) are highlighted to make it easier to identify why a given data asset was returned by a given search.</span></span>

> [!NOTE]
> <span data-ttu-id="756f4-136">적중 항목 강조 표시를 해제하려면 데이터 카탈로그 포털에서 **강조 표시** 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-136">To turn off hit highlighting, use the **Highlight** switch in the Data Catalog portal.</span></span>
>
>

<span data-ttu-id="756f4-137">검색 결과를 볼 때 적중 항목 강조 표시가 활성화되어 있더라도 데이터 자산이 포함된 이유가 항상 명확하지는 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-137">When you view search results, it might not always be obvious why a data asset is included, even with hit highlighting enabled.</span></span> <span data-ttu-id="756f4-138">모든 속성은 기본적으로 검색되므로 열 수준 속성과 일치로 인해 데이터 자산이 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-138">Because all properties are searched by default, a data asset might be returned because of a match on a column-level property.</span></span> <span data-ttu-id="756f4-139">또한 여러 사용자가 자신의 태그 및 설명을 사용하여 등록된 데이터 자산에 주석을 지정할 수 있으므로 모든 메타데이터는 검색 결과 목록에 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-139">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata might be displayed in the list of search results.</span></span>

<span data-ttu-id="756f4-140">기본 타일 보기에서 검색 결과에 표시된 각 타일은 사용자가 일치 수와 해당 위치를 신속하게 보고 원하는 경우 이동할 수 있도록 **검색 용어 일치 항목 보기** 아이콘을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-140">In the default tile view, each tile displayed in the search results includes a **View search term matches** icon, so that you can quickly view the number of matches and their location, and to jump to them if you want.</span></span>

 ![적중 항목 강조 표시 및 Azure 데이터 카탈로그 포털에서 일치하는 항목 검색](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a><span data-ttu-id="756f4-142">요약</span><span class="sxs-lookup"><span data-stu-id="756f4-142">Summary</span></span>
<span data-ttu-id="756f4-143">데이터 원본을 데이터 카탈로그에 등록하면 구조적 메타데이터 및 설명이 포함된 메타데이터를 데이터 원본에서 카탈로그 서비스로 복사하므로 데이터 원본을 보다 쉽게 검색하고 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-143">Because registering a data source with Data Catalog copies structural and descriptive metadata from the data source to the catalog service, the data source becomes easier to discover and understand.</span></span> <span data-ttu-id="756f4-144">데이터 원본을 등록하면 사용자는 데이터 카탈로그 포털 내에서 필터링 및 검색을 사용하여 데이터 원본을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756f4-144">After you've registered a data source, you can discover it by using filtering and search from within the Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="756f4-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="756f4-145">Next steps</span></span>
* <span data-ttu-id="756f4-146">데이터 원본을 검색하는 방법에 대한 자세한 단계별 내용은 [Azure Data Catalog 시작](data-catalog-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="756f4-146">For step-by-step details about how to discover data sources, see [Get Started with Azure Data Catalog](data-catalog-get-started.md).</span></span>
