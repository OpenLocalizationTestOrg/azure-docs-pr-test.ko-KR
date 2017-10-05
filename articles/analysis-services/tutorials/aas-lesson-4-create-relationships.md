---
title: "Azure Analysis Services 자습서 단원 4: 관계 만들기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 관계를 만드는 방법을 설명합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d79af3915c718a79f60e5f589527eb4c2ae8b367
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-4-create-relationships"></a><span data-ttu-id="7bb61-103">단원 4: 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="7bb61-103">Lesson 4: Create relationships</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7bb61-104">이 단원에서는 데이터를 가져오고 서로 다른 테이블 간에 새 관계를 추가할 때 자동으로 생성된 관계를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-104">In this lesson, you verify the relationships that were created automatically when you imported data and add new relationships between different tables.</span></span> <span data-ttu-id="7bb61-105">관계는 해당 테이블의 데이터가 상호 관련되는 방식을 설정하는 두 테이블 간의 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-105">A relationship is a connection between two tables that establishes how the data in those tables should be correlated.</span></span> <span data-ttu-id="7bb61-106">예를 들어 DimProduct 테이블과 DimProductSubcategory 테이블은 각 제품이 하위 범주에 속한다는 사실에 따라 관계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-106">For example, the DimProduct table and the DimProductSubcategory table have a relationship based on the fact that each product belongs to a subcategory.</span></span> <span data-ttu-id="7bb61-107">자세한 내용은 [관계](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bb61-107">To learn more, see [Relationships](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).</span></span>
  
<span data-ttu-id="7bb61-108">이 단원을 완료하기 위한 예상 시간: **10분**</span><span class="sxs-lookup"><span data-stu-id="7bb61-108">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7bb61-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7bb61-109">Prerequisites</span></span>  
<span data-ttu-id="7bb61-110">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7bb61-111">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 3: 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)를 모두 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span> 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a><span data-ttu-id="7bb61-112">기존 관계 검토 및 새 관계 추가</span><span class="sxs-lookup"><span data-stu-id="7bb61-112">Review existing relationships and add new relationships</span></span>  
<span data-ttu-id="7bb61-113">데이터 가져오기를 사용하여 데이터를 가져올 때 AdventureWorksDW2014 데이터베이스에서 7개의 테이블을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-113">When you imported data by using Get Data, you got seven tables from the AdventureWorksDW2014 database.</span></span> <span data-ttu-id="7bb61-114">일반적으로 관계형 원본에서 데이터를 가져올 때 데이터와 함께 기존 관계가 자동으로 가져오기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-114">Generally, when you import data from a relational source, existing relationships are automatically imported together with the data.</span></span> <span data-ttu-id="7bb61-115">그러나 모델 작성을 진행하기 전에 테이블 간의 관계가 적절히 생성되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-115">However, before you proceed with authoring your model you should verify those relationships between tables were created properly.</span></span> <span data-ttu-id="7bb61-116">이 자습서에서는 3가지 새로운 관계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-116">For this tutorial, you add three new relationships.</span></span>  
  
#### <a name="to-review-existing-relationships"></a><span data-ttu-id="7bb61-117">기존 관계를 검토하려면</span><span class="sxs-lookup"><span data-stu-id="7bb61-117">To review existing relationships</span></span>  
  
1.  <span data-ttu-id="7bb61-118">**모델** 메뉴 > **모델 뷰** > **다이어그램 뷰**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-118">Click the **Model** menu > **Model View** > **Diagram View**.</span></span>  

    <span data-ttu-id="7bb61-119">이제 모델 디자이너가 다이어그램 뷰에 표시됩니다. 다이어그램 뷰는 가져온 모든 테이블을 테이블 간의 선으로 표시하는 그래픽 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-119">The model designer now appears in Diagram View, a graphical format displaying all the tables you imported with lines between them.</span></span> <span data-ttu-id="7bb61-120">테이블 간의 선은 데이터를 가져올 때 자동으로 생성된 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-120">The lines between tables indicate the relationships that were automatically created when you imported the data.</span></span>
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    <span data-ttu-id="7bb61-122">모델 디자이너의 오른쪽 아래 모서리에 있는 미니맵 컨트롤을 사용하여 가능한 많은 테이블을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-122">Include as many of the tables as possible by using minimap controls in the lower-right corner of the model designer.</span></span> <span data-ttu-id="7bb61-123">테이블을 다른 위치로 클릭하여 끌어 가깝게 가져오거나 특정 순서로 배치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-123">You can also click and drag tables to different locations, bringing tables closer together, or putting them in a particular order.</span></span> <span data-ttu-id="7bb61-124">테이블을 이동해도 테이블 간 관계에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-124">Moving tables does not affect the relationships already between the tables.</span></span> <span data-ttu-id="7bb61-125">특정 테이블의 모든 열을 보려면 테이블 가장자리를 클릭하고 끌어 확장하거나 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-125">To view all the columns in a particular table, click and drag on a table edge to expand or make it smaller.</span></span>  
  
2.  <span data-ttu-id="7bb61-126">**DimCustomer** 테이블 및 **DimGeography** 테이블 사이의 실선을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-126">Click the solid line between the **DimCustomer** table and the **DimGeography** table.</span></span> <span data-ttu-id="7bb61-127">이러한 두 테이블 간의 실선은 이 관계가 활성 상태임을 나타내므로 기본적으로 DAX 수식을 계산할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-127">The solid line between these two tables shows this relationship is active, that is, it is used by default when calculating DAX formulas.</span></span>  
  
    <span data-ttu-id="7bb61-128">이제 **DimCustomer** 테이블 **GeographyKey** 열 및 **DimGeography** 테이블의 **GeographyKey** 열이 모두 각각 상자 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-128">Notice the **GeographyKey** column in the **DimCustomer** table and the **GeographyKey** column in the **DimGeography** table now both each appear within a box.</span></span> <span data-ttu-id="7bb61-129">이러한 열은 관계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-129">These columns are used in the relationship.</span></span> <span data-ttu-id="7bb61-130">관계의 속성도 **속성** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-130">The relationship’s properties now also appear in the **Properties** window.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="7bb61-131">다이어그램 뷰에서 모델 디자이너를 사용하는 것 외에도 테이블 형식으로 모든 테이블 간에 관계를 표시하려면 관계 관리 대화 상자를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-131">In addition to using the model designer in diagram view, you can also use the Manage Relationships dialog box to show the relationships between all tables in a table format.</span></span> <span data-ttu-id="7bb61-132">테이블 형식 모델 탐색기에서 **관계** > **관계 관리**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-132">In Tabular Model Explorer, right-click **Relationships** > **Manage Relationships**.</span></span>
  
3.  <span data-ttu-id="7bb61-133">AdventureWorksDW 데이터베이스에서 각 테이블을 가져올 때 다음 관계가 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-133">Verify the following relationships were created when each of the tables were imported from the AdventureWorksDW database:</span></span>  
  
    |<span data-ttu-id="7bb61-134">Active</span><span class="sxs-lookup"><span data-stu-id="7bb61-134">Active</span></span>|<span data-ttu-id="7bb61-135">테이블</span><span class="sxs-lookup"><span data-stu-id="7bb61-135">Table</span></span>|<span data-ttu-id="7bb61-136">관련된 조회 테이블</span><span class="sxs-lookup"><span data-stu-id="7bb61-136">Related Lookup Table</span></span>|  
    |----------|---------|------------------------|  
    |<span data-ttu-id="7bb61-137">예</span><span class="sxs-lookup"><span data-stu-id="7bb61-137">Yes</span></span>|<span data-ttu-id="7bb61-138">**DimCustomer [GeographyKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-138">**DimCustomer [GeographyKey]**</span></span>|<span data-ttu-id="7bb61-139">**DimGeography [GeographyKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-139">**DimGeography [GeographyKey]**</span></span>|  
    |<span data-ttu-id="7bb61-140">예</span><span class="sxs-lookup"><span data-stu-id="7bb61-140">Yes</span></span>|<span data-ttu-id="7bb61-141">**DimProduct [ProductSubcategoryKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-141">**DimProduct [ProductSubcategoryKey]**</span></span>|<span data-ttu-id="7bb61-142">**DimProductSubcategory [ProductSubcategoryKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-142">**DimProductSubcategory [ProductSubcategoryKey]**</span></span>|  
    |<span data-ttu-id="7bb61-143">예</span><span class="sxs-lookup"><span data-stu-id="7bb61-143">Yes</span></span>|<span data-ttu-id="7bb61-144">**DimProductSubcategory [ProductCategoryKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-144">**DimProductSubcategory [ProductCategoryKey]**</span></span>|<span data-ttu-id="7bb61-145">**DimProductCategory [ProductCategoryKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-145">**DimProductCategory [ProductCategoryKey]**</span></span>|  
    |<span data-ttu-id="7bb61-146">예</span><span class="sxs-lookup"><span data-stu-id="7bb61-146">Yes</span></span>|<span data-ttu-id="7bb61-147">**FactInternetSales [CustomerKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-147">**FactInternetSales [CustomerKey]**</span></span>|<span data-ttu-id="7bb61-148">**DimCustomer [CustomerKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-148">**DimCustomer [CustomerKey]**</span></span>|  
    |<span data-ttu-id="7bb61-149">예</span><span class="sxs-lookup"><span data-stu-id="7bb61-149">Yes</span></span>|<span data-ttu-id="7bb61-150">**FactInternetSales [ProductKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-150">**FactInternetSales [ProductKey]**</span></span>|<span data-ttu-id="7bb61-151">**DimProduct [ProductKey]**</span><span class="sxs-lookup"><span data-stu-id="7bb61-151">**DimProduct [ProductKey]**</span></span>|  
  
    <span data-ttu-id="7bb61-152">관계가 없는 경우 사용자 모델에 DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory 및 FactInternetSales 테이블이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-152">If any of the relationships are missing, verify that your model includes the following tables: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory, and FactInternetSales.</span></span> <span data-ttu-id="7bb61-153">동일한 데이터 원본 연결의 테이블을 별도의 시간에 가져오는 경우 해당 테이블 간의 관계가 만들어지지 않으므로 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-153">If tables from the same data source connection are imported at separate times, any relationships between those tables are not be created and must be created manually.</span></span>  

### <a name="take-a-closer-look"></a><span data-ttu-id="7bb61-154">자세히 보기</span><span class="sxs-lookup"><span data-stu-id="7bb61-154">Take a closer look</span></span>
<span data-ttu-id="7bb61-155">다이어그램 뷰에는 화살표, 별표 및 테이블 간의 관계를 보여 주는 선 수를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-155">In Diagram View, notice an arrow, an asterisk, and a number on the lines that show the relationship between tables.</span></span>

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

<span data-ttu-id="7bb61-157">화살표는 필터 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-157">The arrow shows the filter direction.</span></span> <span data-ttu-id="7bb61-158">별표는 이 테이블이 관계의 카디널리티에서 많은 면인 것을 보여 주며, 1은 이 테이블이 관계에서 한 면인 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-158">The asterisk shows this table is the many side in the relationship's cardinality, and the one shows this table is the one side of the relationship.</span></span> <span data-ttu-id="7bb61-159">관계를 편집해야 하는 경우, 예를 들어 관계의 필터 방향 또는 카디널리티를 변경하는 경우 관계 선을 두 번 클릭하여 관계 편집 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-159">If you need to edit a relationship; for example, change the relationship's filter direction or cardinality, double-click the relationship line to open the Edit Relationship dialog.</span></span>

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

<span data-ttu-id="7bb61-161">이러한 기능은 고급 데이터 모델링에 대한 내용이며 이 자습서에서는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-161">These features are meant for advanced data modeling and are outside the scope of this tutorial.</span></span> <span data-ttu-id="7bb61-162">자세한 내용은 [Analysis Services에서 테이블 형식 모델에 대한 양방향 크로스 필터](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bb61-162">To learn more, see [Bi-directional cross filters for tabular models in Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).</span></span>

<span data-ttu-id="7bb61-163">일부 경우 특정 비즈니스 논리를 지원하기 위해서는 모델에서 테이블 간의 추가 관계를 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-163">In some cases, you may need to create additional relationships between tables in your model to support certain business logic.</span></span> <span data-ttu-id="7bb61-164">이 자습서에서는 FactInternetSales 테이블 및 DimDate 테이블 간에 세 개의 관계를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-164">For this tutorial, you need to create three additional relationships between the FactInternetSales table and the DimDate table.</span></span>  
  
#### <a name="to-add-new-relationships-between-tables"></a><span data-ttu-id="7bb61-165">테이블 간에 새로운 관계를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="7bb61-165">To add new relationships between tables</span></span>  
  
1.  <span data-ttu-id="7bb61-166">모델 디자이너의 **FactInternetSales** 테이블에서 **OrderDate** 열을 클릭한 채로 커서를 **DimDate** 테이블의 **Date** 열로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-166">In the model designer, in the **FactInternetSales** table, click, and hold on the **OrderDate** column, then drag the cursor to the **Date** column in the **DimDate** table, and then release.</span></span>  

    <span data-ttu-id="7bb61-167">**Internet Sales** 테이블의 **OrderDate** 열과 **Date** 테이블의 **Date** 열 간에 활성 관계가 만들어졌음을 보여 주는 실선이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-167">A solid line appears showing you have created an active relationship between the **OrderDate** column in the **Internet Sales** table, and the **Date** column in the **Date** table.</span></span> 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > <span data-ttu-id="7bb61-169">관계를 만들 때는 기본 테이블과 관련된 조회 테이블 간에 카디널리티 및 필터 방향이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-169">When creating relationships, the cardinality and filter direction between the primary table and the related lookup table is automatically selected.</span></span>  
  
2.  <span data-ttu-id="7bb61-170">**FactInternetSales** 테이블에서 **DueDate** 열을 클릭한 채로 커서를 **DimDate** 테이블의 **Date** 열로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-170">In the **FactInternetSales** table, click and hold on the **DueDate** column, then drag the cursor to the **Date** column in the **DimDate** table, and then release.</span></span>  
  
    <span data-ttu-id="7bb61-171">**FactInternetSales** 테이블의 **DueDate** 열과 **DimDate** 테이블의 **Date** 열 간에 비활성 관계가 만들어졌음을 보여 주는 점선이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-171">A dotted line appears showing you have created an inactive relationship between the **DueDate** column in the **FactInternetSales** table, and the **Date** column in the **DimDate** table.</span></span> <span data-ttu-id="7bb61-172">테이블 간에 여러 관계를 포함할 수 있지만 한 번에 하나의 관계만 활성화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-172">You can have multiple relationships between tables, but only one relationship can be active at a time.</span></span> <span data-ttu-id="7bb61-173">사용자 지정 DAX 식에서 특별한 집계를 수행하기 위해 비활성 관계를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-173">Inactive relationships can be made active to perform special aggregations in custom DAX expressions.</span></span>  
  
3.  <span data-ttu-id="7bb61-174">마지막으로 관계를 하나 더 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-174">Finally, create one more relationship.</span></span> <span data-ttu-id="7bb61-175">**FactInternetSales** 테이블에서 **ShipDate** 열을 클릭한 채로 커서를 **DimDate** 테이블의 **Date** 열로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb61-175">In the **FactInternetSales** table, click and hold on the **ShipDate** column, then drag the cursor to the **Date** column in the **DimDate** table, and then release.</span></span>  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a><span data-ttu-id="7bb61-177">다음 작업</span><span class="sxs-lookup"><span data-stu-id="7bb61-177">What's next?</span></span>
<span data-ttu-id="7bb61-178">[단원 5: 계산된 열 만들기](../tutorials/aas-lesson-5-create-calculated-columns.md)</span><span class="sxs-lookup"><span data-stu-id="7bb61-178">[Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>
  
  
  
