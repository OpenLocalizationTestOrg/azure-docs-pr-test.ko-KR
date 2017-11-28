---
<span data-ttu-id="27d1b-101">제목: aaa "Azure Analysis Services tutorial 추가 단원: 비정형 계층 | Microsoft Docs "설명: toofix hello Azure Analysis Services 자습서의 계층 구조를 정렬 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="27d1b-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="27d1b-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="27d1b-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="27d1b-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="27d1b-104">추가 단원 - 불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="27d1b-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="27d1b-105">이 추가 단원에서는 다양한 수준에서 빈 값(멤버)을 포함하는 계층 구조를 피벗할 때 발생하는 일반적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="27d1b-106">예를 들어, 고위 관리자가 부하 직원으로 부서별 관리자와 비관리자를 포함하는 조직을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="27d1b-107">또는 워싱턴 D.C., 바티칸 시티처럼 일부 도시는 상위 시/도가 없는 국가-지역-도시로 구성된 지리적 계층 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="27d1b-108">계층에 구성원이 비어 있는 경우 종종 toodifferent, 상속 또는 비정형 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="27d1b-110">Hello 1400 호환성 수준에서 테이블 형식 모델은 추가 **멤버 숨기기** 계층에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="27d1b-111">hello **기본** 설정에서는 빈 멤버가 모든 수준에서 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="27d1b-112">hello **빈 멤버를 숨기도록** 설정을 추가할 때 hello 계층에서 빈 멤버를 제외 시킵니다. tooa 피벗 테이블 또는 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="27d1b-113">이 단원에서는 시간 toocomplete 예상: **20 분**</span><span class="sxs-lookup"><span data-stu-id="27d1b-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="27d1b-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="27d1b-114">Prerequisites</span></span>  
<span data-ttu-id="27d1b-115">이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="27d1b-116">이 추가 단원 hello 작업을 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="27d1b-117">Hello AW Internet Sales 프로젝트 hello 자습서의 일부로 만든 모델에 아직 없는 경우 데이터 나 비정형된 계층이 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="27d1b-118">toocomplete이 추가 단원에서는 먼저 있는 toocreate 몇 가지 추가 테이블을 추가 하 여 문제를 hello, 관계, 계산된 열, 측정값 및 새로운 조직 계층을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="27d1b-119">이 부분에는 약 15분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="27d1b-120">Toosolve를 가져온 후, 단 몇 분 후에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="27d1b-121">테이블 및 개체 추가</span><span class="sxs-lookup"><span data-stu-id="27d1b-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="27d1b-122">tooadd 새 테이블 tooyour 모델</span><span class="sxs-lookup"><span data-stu-id="27d1b-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="27d1b-123">테이블 형식 모델 탐색기에서 **데이터 원본**을 확장한 후 연결을 마우스 오른쪽 단추로 클릭한 다음 > **새 테이블 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="27d1b-124">탐색기에서 **DimEmployee** 및 **FactResellerSales**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="27d1b-125">쿼리 편집기에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="27d1b-126">Hello 다음 만들기 [관계](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="27d1b-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="27d1b-127">표 1</span><span class="sxs-lookup"><span data-stu-id="27d1b-127">Table 1</span></span>           | <span data-ttu-id="27d1b-128">열</span><span class="sxs-lookup"><span data-stu-id="27d1b-128">Column</span></span>       | <span data-ttu-id="27d1b-129">필터 방향</span><span class="sxs-lookup"><span data-stu-id="27d1b-129">Filter Direction</span></span>   | <span data-ttu-id="27d1b-130">표 2</span><span class="sxs-lookup"><span data-stu-id="27d1b-130">Table 2</span></span>     | <span data-ttu-id="27d1b-131">열</span><span class="sxs-lookup"><span data-stu-id="27d1b-131">Column</span></span>      | <span data-ttu-id="27d1b-132">Active</span><span class="sxs-lookup"><span data-stu-id="27d1b-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="27d1b-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="27d1b-133">FactResellerSales</span></span> | <span data-ttu-id="27d1b-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-134">OrderDateKey</span></span> | <span data-ttu-id="27d1b-135">기본값</span><span class="sxs-lookup"><span data-stu-id="27d1b-135">Default</span></span>            | <span data-ttu-id="27d1b-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="27d1b-136">DimDate</span></span>     | <span data-ttu-id="27d1b-137">Date</span><span class="sxs-lookup"><span data-stu-id="27d1b-137">Date</span></span>        | <span data-ttu-id="27d1b-138">예</span><span class="sxs-lookup"><span data-stu-id="27d1b-138">Yes</span></span>    |
    | <span data-ttu-id="27d1b-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="27d1b-139">FactResellerSales</span></span> | <span data-ttu-id="27d1b-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="27d1b-140">DueDate</span></span>      | <span data-ttu-id="27d1b-141">기본값</span><span class="sxs-lookup"><span data-stu-id="27d1b-141">Default</span></span>            | <span data-ttu-id="27d1b-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="27d1b-142">DimDate</span></span>     | <span data-ttu-id="27d1b-143">Date</span><span class="sxs-lookup"><span data-stu-id="27d1b-143">Date</span></span>        | <span data-ttu-id="27d1b-144">아니요</span><span class="sxs-lookup"><span data-stu-id="27d1b-144">No</span></span>     |
    | <span data-ttu-id="27d1b-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="27d1b-145">FactResellerSales</span></span> | <span data-ttu-id="27d1b-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-146">ShipDateKey</span></span>  | <span data-ttu-id="27d1b-147">기본값</span><span class="sxs-lookup"><span data-stu-id="27d1b-147">Default</span></span>            | <span data-ttu-id="27d1b-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="27d1b-148">DimDate</span></span>     | <span data-ttu-id="27d1b-149">Date</span><span class="sxs-lookup"><span data-stu-id="27d1b-149">Date</span></span>        | <span data-ttu-id="27d1b-150">아니요</span><span class="sxs-lookup"><span data-stu-id="27d1b-150">No</span></span>     |
    | <span data-ttu-id="27d1b-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="27d1b-151">FactResellerSales</span></span> | <span data-ttu-id="27d1b-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-152">ProductKey</span></span>   | <span data-ttu-id="27d1b-153">기본값</span><span class="sxs-lookup"><span data-stu-id="27d1b-153">Default</span></span>            | <span data-ttu-id="27d1b-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="27d1b-154">DimProduct</span></span>  | <span data-ttu-id="27d1b-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-155">ProductKey</span></span>  | <span data-ttu-id="27d1b-156">예</span><span class="sxs-lookup"><span data-stu-id="27d1b-156">Yes</span></span>    |
    | <span data-ttu-id="27d1b-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="27d1b-157">FactResellerSales</span></span> | <span data-ttu-id="27d1b-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-158">EmployeeKey</span></span>  | <span data-ttu-id="27d1b-159">tooBoth 테이블</span><span class="sxs-lookup"><span data-stu-id="27d1b-159">tooBoth Tables</span></span> | <span data-ttu-id="27d1b-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="27d1b-160">DimEmployee</span></span> | <span data-ttu-id="27d1b-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="27d1b-161">EmployeeKey</span></span> | <span data-ttu-id="27d1b-162">예</span><span class="sxs-lookup"><span data-stu-id="27d1b-162">Yes</span></span>    |

5. <span data-ttu-id="27d1b-163">Hello에 **DimEmployee** 테이블에서 만들 hello 다음 [계산 된 열](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="27d1b-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="27d1b-164">**Path**</span><span class="sxs-lookup"><span data-stu-id="27d1b-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="27d1b-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="27d1b-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="27d1b-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="27d1b-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="27d1b-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="27d1b-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="27d1b-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="27d1b-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="27d1b-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="27d1b-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="27d1b-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="27d1b-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="27d1b-171">Hello에 **DimEmployee** 테이블을 만들기는 [계층](../tutorials/aas-lesson-9-create-hierarchies.md) 라는 **조직**합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="27d1b-172">다음 순서 대로 열 hello 추가: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="27d1b-173">Hello에 **FactResellerSales** 테이블에서 만들 hello 다음 [측정값](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="27d1b-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="27d1b-174">사용 하 여 [Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel 피벗 테이블을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="27d1b-175">**피벗 테이블 필드**, hello 추가 **조직** hello 계층 **DimEmployee** 너무 테이블**행**, 및 hello **ResellerTotalSales** hello에서 측정값 **FactResellerSales** 너무 테이블**값**합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="27d1b-177">Hello 피벗 테이블에서에서 볼 수 있습니다, hello 계층 구조는 비정형 않은 행을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="27d1b-178">빈 멤버가 표시된 많은 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="27d1b-179">hello 숨기기 멤버 속성을 설정 하 여 toofix hello 비정형 계층</span><span class="sxs-lookup"><span data-stu-id="27d1b-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="27d1b-180">**테이블 형식 모델 탐색기**에서 **테이블** > **DimEmployee** > **계층 구조** > **조직**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="27d1b-181">**속성** > **멤버 숨기기**에서 **빈 멤버 숨기기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="27d1b-183">Excel에서 다시 hello를 피벗 테이블을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="27d1b-185">이제 훨씬 좋아 보입니다.</span><span class="sxs-lookup"><span data-stu-id="27d1b-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="27d1b-186">참고 항목</span><span class="sxs-lookup"><span data-stu-id="27d1b-186">See Also</span></span>   
[<span data-ttu-id="27d1b-187">단원 9: 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="27d1b-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="27d1b-188">추가 단원 - 동적 보안</span><span class="sxs-lookup"><span data-stu-id="27d1b-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="27d1b-189">추가 단원 - 세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="27d1b-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  