---
title: "Azure Analysis Services 자습서 추가 단원: 세부 정보 행 | Microsoft Docs"
description: "Azure Analysis Services 자습서에서 세부 정보 행 식을 만드는 방법을 설명합니다."
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
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="779b3-103">추가 단원 - 세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="779b3-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="779b3-104">이 추가 단원에서는 DAX 편집기를 사용하여 사용자 지정 세부 정보 행 식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="779b3-105">세부 정보 행 식은 최종 사용자에게 측정값의 집계된 결과에 대한 더 많은 정보를 제공하는 측정값에 대한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="779b3-106">이 단원을 완료하기 위한 예상 시간: **10분**</span><span class="sxs-lookup"><span data-stu-id="779b3-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="779b3-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="779b3-107">Prerequisites</span></span>  
<span data-ttu-id="779b3-108">이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="779b3-109">이 추가 단원의 작업을 수행하기 전에 이전의 모든 단원을 완료하거나 완료된 Adventure Works Internet Sales 샘플 모델 프로젝트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="779b3-110">해결을 위해 무엇을 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="779b3-110">What do we need to solve?</span></span>
<span data-ttu-id="779b3-111">세부 정보 행 식을 추가하기 전에 InternetTotalSales 측정값에 대한 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="779b3-112">SSDT에서 **모델** 메뉴 > **Excel에서 분석**을 클릭하여 Excel을 열고 빈 피벗 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="779b3-113">**피벗 테이블 필드**에서, FactInternetSales 테이블의 **InternetTotalSales** 측정값을 **Values**로, DimDate 테이블의 **CalendarYear**를 **Columns**로, **EnglishCountryRegionName**을 **Rows**로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="779b3-114">이제 피벗 테이블은 InternetTotalSales 측정값으로부터 지역 및 연도별로 집계된 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="779b3-116">피벗 테이블에서 연도 및 지역 이름에 대해 집계된 값을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="779b3-117">여기서는 2014년 오스트레일리아에 대한 값을 두 번 클릭했습니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="779b3-118">데이터가 포함된 새 시트가 열리지만 유용한 데이터가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="779b3-120">여기서 보려고 하는 것은 InternetTotalSales 측정값의 집계 결과를 구성하는 데이터 행과 열이 포함된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="779b3-121">이를 위해 세부 정보 행 식을 측정값의 속성으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="779b3-122">세부 정보 행 식 추가</span><span class="sxs-lookup"><span data-stu-id="779b3-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="779b3-123">세부 정보 행 식을 만들려면</span><span class="sxs-lookup"><span data-stu-id="779b3-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="779b3-124">SSDT의 FactInternetSales 테이블 측정값 표에서 **InternetTotalSales** 측정값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="779b3-125">**속성** > **세부 정보 행 식**에서 편집기 단추를 클릭하여 DAX 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="779b3-127">DAX 편집기에서 다음 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-127">In DAX Editor, enter the following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="779b3-128">이 식은 FactInternetSales 테이블에서 이름, 열 및 측정값 결과를 지정하며 사용자가 피벗 테이블 또는 보고서에서 집계된 결과를 두 번 클릭하면 관련 테이블이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="779b3-129">다시 Excel에서 3단계에 만든 시트를 삭제한 후 집계된 값을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="779b3-130">이때, 측정값에 대해 정의된 세부 정보 행 식 속성과 함께, 훨씬 유용한 데이터가 포함된 새 시트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="779b3-132">모델을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="779b3-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="779b3-133">참고 항목</span><span class="sxs-lookup"><span data-stu-id="779b3-133">See Also</span></span>  
<span data-ttu-id="779b3-134">[SELECTCOLUMNS 함수(DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="779b3-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="779b3-135">추가 단원 - 동적 보안</span><span class="sxs-lookup"><span data-stu-id="779b3-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="779b3-136">추가 단원 - 불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="779b3-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
