---
title: "Azure Analysis Services 자습서 추가 단원: 불규칙한 계층 구조 | Microsoft Docs"
description: "Azure Analysis Services 자습서에서 불규칙한 계층 구조를 수정하는 방법을 설명합니다."
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
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="b8f98-103">추가 단원 - 불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="b8f98-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b8f98-104">이 추가 단원에서는 다양한 수준에서 빈 값(멤버)을 포함하는 계층 구조를 피벗할 때 발생하는 일반적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="b8f98-105">예를 들어, 고위 관리자가 부하 직원으로 부서별 관리자와 비관리자를 포함하는 조직을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="b8f98-106">또는 워싱턴 D.C., 바티칸 시티처럼 일부 도시는 상위 시/도가 없는 국가-지역-도시로 구성된 지리적 계층 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="b8f98-107">계층 구조에 빈 멤버가 있는 경우 보통 서로 다르거나 불규칙한 수준으로 내려갑니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="b8f98-109">1400 호환성 수준의 테이블 형식 모델에는 계층 구조에 대한 추가 **멤버 숨기기** 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="b8f98-110">**기본** 설정에서는 어떤 수준에도 빈 멤버가 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="b8f98-111">**빈 멤버 숨기기** 설정은 피벗 테이블 또는 보고서에 계층 구조가 추가된 경우 계층 구조에서 빈 멤버를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="b8f98-112">이 단원을 완료하기 위한 예상 시간: **20분**</span><span class="sxs-lookup"><span data-stu-id="b8f98-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b8f98-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b8f98-113">Prerequisites</span></span>  
<span data-ttu-id="b8f98-114">이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="b8f98-115">이 추가 단원의 작업을 수행하기 전에 이전의 모든 단원을 완료하거나 완료된 Adventure Works Internet Sales 샘플 모델 프로젝트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="b8f98-116">자습서의 일부로 AW Internet Sales 프로젝트를 만들었으면 모델에는 아직 데이터 또는 불규칙한 계층 구조가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="b8f98-117">이 추가 단원을 완료하려면 먼저 몇 가지 테이블을 더 추가하고, 관계, 계산된 열, 측정값 및 새 조직 계층 구조를 만들어서 문제를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="b8f98-118">이 부분에는 약 15분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="b8f98-119">그런 다음 몇 분 안에 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="b8f98-120">테이블 및 개체 추가</span><span class="sxs-lookup"><span data-stu-id="b8f98-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="b8f98-121">모델에 새 테이블을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b8f98-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="b8f98-122">테이블 형식 모델 탐색기에서 **데이터 원본**을 확장한 후 연결을 마우스 오른쪽 단추로 클릭한 다음 > **새 테이블 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="b8f98-123">탐색기에서 **DimEmployee** 및 **FactResellerSales**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="b8f98-124">쿼리 편집기에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="b8f98-125">다음 [관계](../tutorials/aas-lesson-4-create-relationships.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="b8f98-126">표 1</span><span class="sxs-lookup"><span data-stu-id="b8f98-126">Table 1</span></span>           | <span data-ttu-id="b8f98-127">열</span><span class="sxs-lookup"><span data-stu-id="b8f98-127">Column</span></span>       | <span data-ttu-id="b8f98-128">필터 방향</span><span class="sxs-lookup"><span data-stu-id="b8f98-128">Filter Direction</span></span>   | <span data-ttu-id="b8f98-129">표 2</span><span class="sxs-lookup"><span data-stu-id="b8f98-129">Table 2</span></span>     | <span data-ttu-id="b8f98-130">열</span><span class="sxs-lookup"><span data-stu-id="b8f98-130">Column</span></span>      | <span data-ttu-id="b8f98-131">Active</span><span class="sxs-lookup"><span data-stu-id="b8f98-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="b8f98-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8f98-132">FactResellerSales</span></span> | <span data-ttu-id="b8f98-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-133">OrderDateKey</span></span> | <span data-ttu-id="b8f98-134">기본값</span><span class="sxs-lookup"><span data-stu-id="b8f98-134">Default</span></span>            | <span data-ttu-id="b8f98-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8f98-135">DimDate</span></span>     | <span data-ttu-id="b8f98-136">Date</span><span class="sxs-lookup"><span data-stu-id="b8f98-136">Date</span></span>        | <span data-ttu-id="b8f98-137">예</span><span class="sxs-lookup"><span data-stu-id="b8f98-137">Yes</span></span>    |
    | <span data-ttu-id="b8f98-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8f98-138">FactResellerSales</span></span> | <span data-ttu-id="b8f98-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="b8f98-139">DueDate</span></span>      | <span data-ttu-id="b8f98-140">기본값</span><span class="sxs-lookup"><span data-stu-id="b8f98-140">Default</span></span>            | <span data-ttu-id="b8f98-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8f98-141">DimDate</span></span>     | <span data-ttu-id="b8f98-142">Date</span><span class="sxs-lookup"><span data-stu-id="b8f98-142">Date</span></span>        | <span data-ttu-id="b8f98-143">아니요</span><span class="sxs-lookup"><span data-stu-id="b8f98-143">No</span></span>     |
    | <span data-ttu-id="b8f98-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8f98-144">FactResellerSales</span></span> | <span data-ttu-id="b8f98-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-145">ShipDateKey</span></span>  | <span data-ttu-id="b8f98-146">기본값</span><span class="sxs-lookup"><span data-stu-id="b8f98-146">Default</span></span>            | <span data-ttu-id="b8f98-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8f98-147">DimDate</span></span>     | <span data-ttu-id="b8f98-148">Date</span><span class="sxs-lookup"><span data-stu-id="b8f98-148">Date</span></span>        | <span data-ttu-id="b8f98-149">아니요</span><span class="sxs-lookup"><span data-stu-id="b8f98-149">No</span></span>     |
    | <span data-ttu-id="b8f98-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8f98-150">FactResellerSales</span></span> | <span data-ttu-id="b8f98-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-151">ProductKey</span></span>   | <span data-ttu-id="b8f98-152">기본값</span><span class="sxs-lookup"><span data-stu-id="b8f98-152">Default</span></span>            | <span data-ttu-id="b8f98-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="b8f98-153">DimProduct</span></span>  | <span data-ttu-id="b8f98-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-154">ProductKey</span></span>  | <span data-ttu-id="b8f98-155">예</span><span class="sxs-lookup"><span data-stu-id="b8f98-155">Yes</span></span>    |
    | <span data-ttu-id="b8f98-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8f98-156">FactResellerSales</span></span> | <span data-ttu-id="b8f98-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-157">EmployeeKey</span></span>  | <span data-ttu-id="b8f98-158">두 테이블로</span><span class="sxs-lookup"><span data-stu-id="b8f98-158">To Both Tables</span></span> | <span data-ttu-id="b8f98-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="b8f98-159">DimEmployee</span></span> | <span data-ttu-id="b8f98-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b8f98-160">EmployeeKey</span></span> | <span data-ttu-id="b8f98-161">예</span><span class="sxs-lookup"><span data-stu-id="b8f98-161">Yes</span></span>    |

5. <span data-ttu-id="b8f98-162">**DimEmployee** 테이블에서 다음 [계산된 열](../tutorials/aas-lesson-5-create-calculated-columns.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="b8f98-163">**Path**</span><span class="sxs-lookup"><span data-stu-id="b8f98-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="b8f98-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="b8f98-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="b8f98-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="b8f98-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="b8f98-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="b8f98-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="b8f98-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="b8f98-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="b8f98-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="b8f98-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="b8f98-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="b8f98-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="b8f98-170">**DimEmployee** 테이블에서 **Organization**이라는 이름의 [계층 구조](../tutorials/aas-lesson-9-create-hierarchies.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="b8f98-171">다음 열을 순서대로 추가합니다. **Level1**, **Level2**, **Level3**, **Level4**, **Level5**</span><span class="sxs-lookup"><span data-stu-id="b8f98-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="b8f98-172">**FactResellerSales** 테이블에서 다음 [측정값](../tutorials/aas-lesson-6-create-measures.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="b8f98-173">[Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)을 사용하여 Excel을 열고 피벗 테이블을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="b8f98-174">**피벗 테이블 필드**에서 **DimEmployee** 테이블의 **Organization** 계층 구조를 **Rows**에 추가하고 **FactResellerSales** 테이블의 **ResellerTotalSales** 측정값을 **Values**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="b8f98-176">피벗 테이블에서 볼 수 있는 것처럼 계층 구조에 불규칙한 행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="b8f98-177">빈 멤버가 표시된 많은 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="b8f98-178">멤버 숨기기 속성을 설정하여 불규칙한 계층 구조를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="b8f98-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="b8f98-179">**테이블 형식 모델 탐색기**에서 **테이블** > **DimEmployee** > **계층 구조** > **조직**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="b8f98-180">**속성** > **멤버 숨기기**에서 **빈 멤버 숨기기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="b8f98-182">다시 Excel에서 피벗 테이블을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="b8f98-184">이제 훨씬 좋아 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f98-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="b8f98-185">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b8f98-185">See Also</span></span>   
[<span data-ttu-id="b8f98-186">단원 9: 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="b8f98-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="b8f98-187">추가 단원 - 동적 보안</span><span class="sxs-lookup"><span data-stu-id="b8f98-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="b8f98-188">추가 단원 - 세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="b8f98-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  