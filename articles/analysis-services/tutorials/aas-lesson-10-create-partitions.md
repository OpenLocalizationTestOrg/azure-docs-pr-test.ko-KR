---
<span data-ttu-id="54cfe-101">제목: aaa "10 Azure Analysis Services 자습서 단원: 파티션 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트에서 분할 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="54cfe-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="54cfe-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="54cfe-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="54cfe-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="54cfe-104">단원 10: 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="54cfe-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="54cfe-105">이 단원에서는 처리 (새로 고침된) 다른 파티션과 별개로 될 수 있는 더 작은 논리적 부분으로 파티션을 toodivide hello FactInternetSales 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="54cfe-106">기본적으로 모델에 포함할 모든 테이블에는 모든 hello 테이블의 열과 행을 포함 하는 파티션이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="54cfe-107">Hello FactInternetSales 테이블에 대 한 연도별; toodivide hello 데이터 원합니다 각 5 년 hello 테이블에 대해 하나의 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="54cfe-108">그러면 각 파티션은 독립적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="54cfe-109">toolearn 더 참조 [파티션을](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular)합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="54cfe-110">이 단원에서는 시간 toocomplete 예상: **15 분**</span><span class="sxs-lookup"><span data-stu-id="54cfe-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="54cfe-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54cfe-111">Prerequisites</span></span>  
<span data-ttu-id="54cfe-112">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="54cfe-113">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [9 단원: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="54cfe-114">파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="54cfe-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="54cfe-115">hello FactInternetSales 테이블에서 파티션의 toocreate</span><span class="sxs-lookup"><span data-stu-id="54cfe-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="54cfe-116">테이블 형식 모델 탐색기에서 **테이블**를 확장하고 **FactInternetSales** > **파티션**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="54cfe-117">파티션 관리자에서 클릭 **복사**를 바꾼 다음 hello 이름이 너무**FactInternetSales2010**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="54cfe-118">하려고 하기 때문에 파티션 tooinclude hello는 행만 hello 연도 2010에 대 한 특정 기간 내 hello 쿼리 식을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="54cfe-119">클릭 **디자인** tooopen 쿼리 편집기와 hello 클릭 **FactInternetSales2010** 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="54cfe-120">미리 보기에서 아래쪽 화살표를 hello hello 클릭 **OrderDate** 열 머리글을 클릭 한 다음 **날짜/시간 필터** > **사이의**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="54cfe-122">Hello 행 필터 대화 상자에서에서 **인 경우 행 표시: OrderDate**, 둡니다 **이후 또는 같음**, hello 날짜 필드에 입력 한 다음 **1/1/2010**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="54cfe-123">Hello 둡니다 **및** 연산자를 선택 하면 다음 선택 **앞**, hello 날짜 필드에 입력 한 다음 **2011/1/1**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="54cfe-125">쿼리 편집기의 적용 단계에서 필터링된 행이라는 다른 단계가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="54cfe-126">이 필터는 2010에서 tooselect만 주문 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="54cfe-127">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-127">Click **Import**.</span></span>

    <span data-ttu-id="54cfe-128">파티션 관리자는 이제 식에 추가 행 필터링 절 hello 쿼리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="54cfe-130">이 문은이 파티션에 hello OrderDate는 hello에서 2010 년 hello 필터링 된 rows 절에 지정 된 대로 행의 hello 데이터만 포함 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="54cfe-131">2011 년 hello에 대 한 파티션 toocreate</span><span class="sxs-lookup"><span data-stu-id="54cfe-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="54cfe-132">Hello 파티션 목록에서 클릭 hello **FactInternetSales2010** 작성 한을 분할 하 고 클릭 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="54cfe-133">Hello 파티션 이름에도 변경**FactInternetSales2011**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="54cfe-134">쿼리 편집기 toocreate 새 필터링 된 행 절 toouse가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="54cfe-135">2010에 대 한 hello 쿼리의 복사본을 만들 때 toodo 가장 필요한 것 이므로 2011 용 hello 쿼리에서 코드를 약간만 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="54cfe-136">**쿼리 식**, 순서로 파티션 tooinclude이에 대 한 hello에 대 한 행만 2011 연도, 사용 된 hello 행 필터링 절에서 hello 연도 대체 **2011** 및 **2012**에서 위와 같은:</span><span class="sxs-lookup"><span data-stu-id="54cfe-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="54cfe-137">2012, 2013 및 2014에 대 한 toocreate 파티션.</span><span class="sxs-lookup"><span data-stu-id="54cfe-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="54cfe-138">2012, 2013 및 2014 년 hello 년 hello 행 필터링 절 tooinclude만 행에 해당 연도 대 한 변경에 대 한 파티션을 만들면 그 hello 이전 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="54cfe-139">Hello FactInternetSales 파티션을 삭제합니다</span><span class="sxs-lookup"><span data-stu-id="54cfe-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="54cfe-140">각 연도 대 한 파티션을가지고 hello FactInternetSales 파티션을;을 삭제할 수 있습니다. 파티션을 처리할 때 모든 프로세스를 선택할 때 겹침을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="54cfe-141">toodelete hello FactInternetSales 파티션</span><span class="sxs-lookup"><span data-stu-id="54cfe-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="54cfe-142">Hello FactInternetSales 파티션을 클릭 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="54cfe-143">파티션 처리</span><span class="sxs-lookup"><span data-stu-id="54cfe-143">Process partitions</span></span>  
<span data-ttu-id="54cfe-144">파티션 관리자에서 확인 hello **마지막 처리** 이러한 파티션을 처리 하지 않은 표시를 생성 하는 hello 새 파티션 각각에 대 한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="54cfe-145">파티션을 만들 때 해당 파티션을에서 파티션 처리 또는 테이블 처리 작업 toorefresh hello 데이터를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="54cfe-146">tooprocess hello FactInternetSales 파티션</span><span class="sxs-lookup"><span data-stu-id="54cfe-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="54cfe-147">클릭 **확인** tooclose 파티션 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="54cfe-148">Hello 클릭 **FactInternetSales** 테이블을 클릭 hello **모델** 메뉴 > **프로세스** > **파티션 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="54cfe-149">Hello 파티션 처리 대화 상자에서 확인 **모드** 너무 설정**기본값 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="54cfe-150">Hello에 hello 확인란을 선택 **프로세스** 생성 하 고 클릭 한 다음 각 5 hello에 대 한 열 파티션 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="54cfe-152">가장 자격 증명을 묻는 hello Windows 사용자 이름 및 2 단원에서에서 지정한 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="54cfe-153">hello **데이터 처리** 대화 상자가 나타나고 각 파티션에 대 한 처리 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="54cfe-154">파티션마다 서로 다른 행 수가 전송된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="54cfe-155">각 파티션은 hello hello SQL 문의 WHERE 절에에서 지정 된 hello 연도 대 한 행만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="54cfe-156">처리가 완료 되 면 계속 진행 하 고 hello 데이터 처리 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="54cfe-158">다음 작업</span><span class="sxs-lookup"><span data-stu-id="54cfe-158">What's next?</span></span>
<span data-ttu-id="54cfe-159">다음 단원 이동 toohello: [11 단원: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54cfe-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
