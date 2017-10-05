---
title: "Azure Data Catalog에서 관련 데이터 자산을 보는 방법 | Microsoft Docs"
description: "이 문서에서는 Azure Data Catalog에서 선택한 데이터 자산의 관련 데이터 자산을 보는 방법을 설명합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="ca60c-103">Azure Data Catalog에서 관련 데이터 자산을 보는 방법</span><span class="sxs-lookup"><span data-stu-id="ca60c-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="ca60c-104">Azure Data Catalog를 사용하면 선택한 데이터 자산과 관련된 데이터 자산을 보고 관계를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="ca60c-105">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="ca60c-105">Supported data sources</span></span> 
<span data-ttu-id="ca60c-106">다음 데이터 원본의 데이터 자산을 등록하면 Azure Data Catalog는 선택한 데이터 자산 간의 조인 관계에 대한 메타데이터를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="ca60c-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca60c-107">SQL Server</span></span>
- <span data-ttu-id="ca60c-108">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="ca60c-108">Azure SQL Database</span></span>
- <span data-ttu-id="ca60c-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="ca60c-109">MySQL</span></span>
- <span data-ttu-id="ca60c-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="ca60c-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="ca60c-111">관련된 데이터 자산 보기</span><span class="sxs-lookup"><span data-stu-id="ca60c-111">View related data assets</span></span>
<span data-ttu-id="ca60c-112">선택한 데이터 집합과 관련된 데이터 자산을 보려면 다음 그림과 같이 **관계** 탭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog - 관련 데이터 자산 보기](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="ca60c-114">이 예제에는 선택한 **ProductSubcategory** 데이터 자산에 대해 2가지 관계가 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="ca60c-115">Product 테이블의 ProductSubcategoryID 열은 선택한 ProductSubcategory 테이블의 ProductSubcategoryID 열과 외래 키 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="ca60c-116">ProductSubCategory 테이블의 ProductCategoryID 열은 선택한 ProductCategory 테이블의 ProductCategoryID 열과 외래 키 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="ca60c-117">관계 트리 보기의 화살표 방향을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ca60c-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="ca60c-118">열의 정규화된 이름 같은 자세한 정보를 보려면 마우스를 위로 가져갑니다. 그러면 다음 그림과 비슷한 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog - 관계 팝업](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="ca60c-120">이미 등록된 자산 간의 관계를 포함하려면 해당 자산을 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ca60c-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca60c-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca60c-121">Next steps</span></span>
- [<span data-ttu-id="ca60c-122">데이터 자산을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ca60c-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)