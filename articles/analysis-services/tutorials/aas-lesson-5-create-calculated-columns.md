---
title: "Azure Analysis Services 자습서 단원 5: 계산된 열 만들기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 계산된 열을 만드는 방법을 설명합니다."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="70b8f-103">단원 5: 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="70b8f-104">이 단원에서는 계산된 열을 추가하여 모델에서 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="70b8f-105">쿼리 편집기를 사용하거나 여기에서처럼 나중에 모델 디자이너에서 데이터 가져오기를 사용할 때 계산된 열(사용자 지정 열로)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="70b8f-106">자세한 내용은 [계산된 열](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70b8f-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="70b8f-107">서로 다른 세 테이블에 5개의 새 계산된 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="70b8f-108">단계는 열을 생성하고 이름을 바꾸며 테이블의 여러 위치에 배치하는 여러 가지 방법이 있음을 보여 주는 각 작업에 대해 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="70b8f-109">이 단원에서는 먼저 DAX(Data Analysis Expressions)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="70b8f-110">DAX는 테이블 형식 모델에 대해 사용자 지정 가능한 수식을 만드는 특별한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="70b8f-111">이 자습서에서는 DAX를 사용하여 계산된 열, 측정값 및 역할 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="70b8f-112">자세한 내용은 [테이블 형식 모델의 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70b8f-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="70b8f-113">이 단원을 완료하기 위한 예상 시간: **15분**</span><span class="sxs-lookup"><span data-stu-id="70b8f-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="70b8f-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="70b8f-114">Prerequisites</span></span>  
<span data-ttu-id="70b8f-115">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="70b8f-116">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 4: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="70b8f-117">계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="70b8f-118">DimDate 테이블에서 MonthCalendar 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="70b8f-119">**모델** 메뉴 > **모델 뷰** > **데이터 뷰**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="70b8f-120">데이터 뷰에서는 모델 디자이너를 사용하여 계산된 열만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="70b8f-121">모델 디자이너에서 **DimDate** 테이블(탭)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="70b8f-122">**CalendarQuarter** 열 머리글을 마우스 오른쪽 단추로 클릭한 후 **열 삽입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="70b8f-123">**계산된 열 1**이라는 새 열이 **사분기** 열의 왼쪽에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="70b8f-124">테이블 위의 수식 입력줄에 다음 DAX 수식을 입력합니다. 자동 완성을 통해 열 및 테이블의 정규화된 이름을 입력하고 사용 가능한 함수 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="70b8f-125">그러면 계산된 열의 모든 행에 대한 값이 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="70b8f-126">테이블을 아래로 스크롤하면, 각 행의 데이터에 따라 행이 이 열에 대해 서로 다른 값을 포함할 수 있는 것을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="70b8f-127">이 열의 이름을 **MonthCalendar**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="70b8f-129">MonthCalendar 계산된 열은 Month(월)에 대한 정렬 가능한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="70b8f-130">DimDate 테이블에서 DayOfWeek 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="70b8f-131">**DimDate** 테이블이 활성 상태인 동안 **열** 메뉴를 클릭한 후 **열 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="70b8f-132">수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="70b8f-133">수식 작성을 마쳤으면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="70b8f-134">새 열은 테이블의 오른쪽 끝에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="70b8f-135">열 이름을 **DayOfWeek**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="70b8f-136">열 머리글을 클릭하고 열을 **EnglishDayNameOfWeek** 열과 **DayNumberOfMonth** 열 사이로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="70b8f-137">테이블에서 열을 이동하여 쉽게 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="70b8f-138">DayOfWeek 계산된 열은 요일에 대한 정렬 가능한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="70b8f-139">DimProduct 테이블의 ProductSubcategoryName 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="70b8f-140">**DimProduct** 테이블에서 오른쪽 끝으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="70b8f-141">맨 오른쪽 열 이름이 **열 추가**(기울임꼴)인 것을 확인하고 열 머리글을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="70b8f-142">수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="70b8f-143">열 이름을 **ProductSubcategoryName**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="70b8f-144">ProductSubcategoryName 계산된 열은 DimProductSubcategory 테이블에서 EnglishProductSubcategoryName 열의 데이터를 포함하는 DimProduct 테이블의 계층 구조를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="70b8f-145">계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="70b8f-146">계층 구조는 단원 9에서 나중에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="70b8f-147">DimProduct 테이블의 ProductCategoryName 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="70b8f-148">**DimProduct** 테이블이 활성 상태인 동안 **열** 메뉴를 클릭한 후 **열 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="70b8f-149">수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="70b8f-150">열 이름을 **ProductCategoryName**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="70b8f-151">ProductCategoryName 계산된 열은 DimProductCategory 테이블에서 EnglishProductCategoryName 열의 데이터를 포함하는 DimProduct 테이블의 계층 구조를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="70b8f-152">계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="70b8f-153">FactInternetSales 테이블에서 Margin 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="70b8f-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="70b8f-154">모델 디자이너에서 **FactInternetSales** 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="70b8f-155">**SalesAmount** 열과 **TaxAmt** 열 사이에 새로운 계산된 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="70b8f-156">수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="70b8f-157">열 이름을 **Margin**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="70b8f-159">Margin 계산된 열은 각 판매의 이익률을 분석하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b8f-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="70b8f-160">다음 작업</span><span class="sxs-lookup"><span data-stu-id="70b8f-160">What's next?</span></span>
<span data-ttu-id="70b8f-161">[단원 6: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)</span><span class="sxs-lookup"><span data-stu-id="70b8f-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
