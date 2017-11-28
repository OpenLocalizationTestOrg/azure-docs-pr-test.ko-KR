---
title: "aaaHow tooview 관련 Azure Data Catalog에서 데이터 자산 | Microsoft Docs"
description: "이 문서에서는 tooview Azure Data Catalog에서 선택한 데이터 자산의 데이터 자산을 연결 하는 방법을 설명 합니다."
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
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="6e835-103">어떻게 tooview 데이터 자산 Azure Data Catalog에 관련 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="6e835-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="6e835-104">Azure Data Catalog tooview 데이터 자산 선택 관련된 tooa 데이터 자산 및 뷰 간에 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="6e835-105">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="6e835-105">Supported data sources</span></span> 
<span data-ttu-id="6e835-106">Hello 데이터 원본에서 데이터 자산을 등록 하면 Azure Data Catalog hello 선택한 데이터 자산 간의 관계 조인에 대 한 메타 데이터를 자동으로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="6e835-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6e835-107">SQL Server</span></span>
- <span data-ttu-id="6e835-108">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="6e835-108">Azure SQL Database</span></span>
- <span data-ttu-id="6e835-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="6e835-109">MySQL</span></span>
- <span data-ttu-id="6e835-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="6e835-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="6e835-111">관련된 데이터 자산 보기</span><span class="sxs-lookup"><span data-stu-id="6e835-111">View related data assets</span></span>
<span data-ttu-id="6e835-112">tooview 데이터 자산 관련된 tooa 선택한 데이터 집합을 사용 하 여 hello **관계** hello 다음 이미지에에서 나와 있는 것 처럼 탭:</span><span class="sxs-lookup"><span data-stu-id="6e835-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog - 관련 데이터 자산 보기](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="6e835-114">이 예제에는 선택한 hello에 대 한 두 개의 관계가 **ProductSubcategory** 데이터 자산:</span><span class="sxs-lookup"><span data-stu-id="6e835-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="6e835-115">ProductSubcategoryID 열 hello Product 테이블의 외래 키 관계를 선택 하는 hello ProductSubcategory 테이블의 열이 다르다는 것에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="6e835-116">Hello ProductSubCategory 테이블의 열 ProductCategoryID ProductCategoryID 열이 선택한 hello ProductCategory 테이블의 외래 키 관계를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="6e835-117">Hello 화살표 방향으로 hello hello 관계 트리 보기에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="6e835-118">toosee hello hello 열의 정규화 된 이름 같은 자세한 정보 hello 위로 마우스를 이동 하 고 다음 이미지는 팝업 비슷한 toohello 참조:</span><span class="sxs-lookup"><span data-stu-id="6e835-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog - 관계 팝업](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="6e835-120">이미 등록 자산 간의 tooinclude 관계는 다시 해당 자산을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e835-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e835-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e835-121">Next steps</span></span>
- [<span data-ttu-id="6e835-122">어떻게 toomanage 데이터 자산</span><span class="sxs-lookup"><span data-stu-id="6e835-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
