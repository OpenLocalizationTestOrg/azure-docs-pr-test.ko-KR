---
title: "Azure Analysis Services 자습서 단원 9: 계층 구조 만들기 | Microsoft Docs"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="4a808-102">단원 9: 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="4a808-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4a808-103">이 단원에서는 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="4a808-104">계층 구조는 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층 구조는 Country, State, County 및 City에 대한 하위 수준을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="4a808-105">계층 구조는 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과 별도로 표시될 수 있으므로 클라이언트 사용자가 보고서에서 쉽게 탐색 및 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="4a808-106">자세한 내용은 [계층 구조](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a808-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="4a808-107">계층 구조를 만들려면 *다이어그램 뷰*에서 모델 디자이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="4a808-108">데이터 뷰에서 계층 구조 만들기 및 관리는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="4a808-109">이 단원을 완료하기 위한 예상 시간: **20분**</span><span class="sxs-lookup"><span data-stu-id="4a808-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4a808-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4a808-110">Prerequisites</span></span>  
<span data-ttu-id="4a808-111">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4a808-112">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 8: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="4a808-113">계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="4a808-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="4a808-114">DimProduct 테이블에 Category 계층 구조를 만들려면</span><span class="sxs-lookup"><span data-stu-id="4a808-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="4a808-115">모델 디자이너(다이어그램 뷰)에서 **DimProduct** 테이블 > **계층 구조 만들기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="4a808-116">새 계층 구조가 테이블 창 맨 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="4a808-117">계층 구조 이름을 **Category**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="4a808-118">**ProductCategoryName** 열을 클릭하여 새 **Category** 계층 구조로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="4a808-119">**Category** 계층 구조에서 **ProductCategoryName** > **이름 바꾸기**를 마우스 오른쪽 단추로 클릭한 후 **Category**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="4a808-120">계층 구조에서 열 이름을 변경해도 테이블의 열 이름은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="4a808-121">계층 구조의 열은 테이블의 열을 표현한 것일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="4a808-122">**ProductSubcategoryName** 열을 클릭하여 **Category** 계층 구조로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="4a808-123">**Subcategory**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="4a808-124">**ModelName** 열 > **계층 구조에 추가**를 마우스 오른쪽 단추로 클릭한 후 **Category**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="4a808-125">**Model**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="4a808-126">마지막으로, **EnglishProductName**을 Category 계층 구조에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="4a808-127">**Product**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="4a808-129">DimDate 테이블에서 계층 구조를 만들려면</span><span class="sxs-lookup"><span data-stu-id="4a808-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="4a808-130">**DimDate** 테이블에서 **Calendar**라는 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="4a808-131">다음 열을 순서대로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="4a808-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="4a808-132">CalendarYear</span></span>
    *  <span data-ttu-id="4a808-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="4a808-133">CalendarSemester</span></span>
    *  <span data-ttu-id="4a808-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4a808-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="4a808-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="4a808-135">MonthCalendar</span></span>
    *  <span data-ttu-id="4a808-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="4a808-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="4a808-137">**DimDate** 테이블에서 **Fiscal** 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="4a808-138">다음 열을 순서대로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="4a808-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="4a808-139">FiscalYear</span></span>
    *  <span data-ttu-id="4a808-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="4a808-140">FiscalSemester</span></span>
    *  <span data-ttu-id="4a808-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4a808-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="4a808-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="4a808-142">MonthCalendar</span></span>
    *  <span data-ttu-id="4a808-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="4a808-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="4a808-144">마지막으로, **DimDate** 테이블에서 **ProductionCalendar** 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="4a808-145">다음 열을 순서대로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4a808-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="4a808-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="4a808-146">CalendarYear</span></span>
    *  <span data-ttu-id="4a808-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="4a808-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="4a808-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="4a808-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="4a808-149">다음 작업</span><span class="sxs-lookup"><span data-stu-id="4a808-149">What's next?</span></span>
<span data-ttu-id="4a808-150">[단원 10: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)</span><span class="sxs-lookup"><span data-stu-id="4a808-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
