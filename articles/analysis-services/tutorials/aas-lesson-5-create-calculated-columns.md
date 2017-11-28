---
<span data-ttu-id="393da-101">제목: aaa "5 Azure Analysis Services 자습서 단원: 계산된 열 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트의 열을 계산 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="393da-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="393da-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="393da-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="393da-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="393da-104">단원 5: 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="393da-105">이 단원에서는 계산된 열을 추가하여 모델에서 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393da-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="393da-106">(사용자 정의 열)으로 계산 된 열을 만들 수 있습니다 쿼리 편집기 hello를 사용 하 여 가져올 데이터를 사용할 때 또는 나중에 모델 디자이너 같은 hello 있습니다 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="393da-107">toolearn 더 참조 [계산 된 열](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="393da-108">서로 다른 세 테이블에 5개의 새 계산된 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393da-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="393da-109">hello 단계는 약간 다른 여러 가지 toocreate 열을 보여 주는 각 작업에 대해, 이름을 바꾸고 테이블의 다양 한 위치에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="393da-110">이 단원에서는 먼저 DAX(Data Analysis Expressions)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="393da-111">DAX는 테이블 형식 모델에 대해 사용자 지정 가능한 수식을 만드는 특별한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="393da-112">이 자습서에서는 DAX toocreate 계산 열, 측정값 및 역할 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="393da-113">toolearn 더 참조 [테이블 형식 모델에서 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="393da-114">이 단원에서는 시간 toocomplete 예상: **15 분**</span><span class="sxs-lookup"><span data-stu-id="393da-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="393da-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="393da-115">Prerequisites</span></span>  
<span data-ttu-id="393da-116">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="393da-117">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [4 단원: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="393da-118">계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="393da-119">Hello DimDate 테이블에서 MonthCalendar 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="393da-120">Hello 클릭 **모델** 메뉴 > **모델 뷰** > **데이터 뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="393da-121">계산 된 열 데이터 뷰에서 hello 모델 디자이너를 사용 하 여 만들 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393da-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="393da-122">Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블 (탭).</span><span class="sxs-lookup"><span data-stu-id="393da-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="393da-123">마우스 오른쪽 단추로 클릭 hello **CalendarQuarter** 열 머리글을 클릭 한 다음 **열 삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="393da-124">이라는 새 열 **계산 열 1** hello 삽입된 toohello 왼쪽은 **Calendar Quarter** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="393da-125">Hello hello 테이블 위의 수식 입력줄에서 다음 DAX 수식을 hello 입력: 자동 완성 사용 하면 입력 열과 테이블의 정규화 된 이름을 hello 및 목록을 사용할 수 있는 함수와 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="393da-126">값이 모든 hello 행 hello 계산된 열에 대해 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="393da-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="393da-127">Hello 테이블을 통해 아래로 스크롤할 경우 행이 열에서 각 행에 hello 데이터에 따라 다른 값을 가질 수 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393da-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="393da-128">이 열을 너무 이름 바꾸기**MonthCalendar**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="393da-130">hello MonthCalendar 계산된 열에는 월에 대 한 정렬 가능한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="393da-131">Hello DimDate 테이블의 DayOfWeek 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="393da-132">Hello로 **DimDate** 여전히 활성 상태 테이블에서 hello **열** 메뉴를 차례로 클릭 **열 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="393da-133">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="393da-134">Hello 수식 작성을 마쳤으면 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="393da-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="393da-135">새 열 hello toohello hello 테이블의 맨 오른쪽에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393da-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="393da-136">너무 hello 열 이름 바꾸기**DayOfWeek**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="393da-137">Hello 열 머리글을 클릭 한 다음 hello 간의 hello 열을 끌어 **EnglishDayNameOfWeek** 열과 hello **DayNumberOfMonth** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="393da-138">테이블에서 열을 이동 하면 더 쉽게 toonavigate 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393da-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="393da-139">hello DayOfWeek 계산된 열에는 hello 요일에 대 한 정렬 가능한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="393da-140">Hello DimProduct 테이블에서 ProductSubcategoryName 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="393da-141">Hello에 **DimProduct** 테이블, hello 테이블의 맨 오른쪽 toohello 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="393da-142">공지 hello 맨 오른쪽 열 이름이 **열 추가** (기울임꼴) hello 열 머리글을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="393da-143">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="393da-144">너무 hello 열 이름 바꾸기**ProductSubcategoryName**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="393da-145">hello ProductSubcategoryName 계산된 열에 사용 되는 toocreate hello DimProductSubcategory 테이블에 hello EnglishProductSubcategoryName 열에서 데이터를 포함 하는 hello DimProduct 테이블의 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="393da-146">계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="393da-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="393da-147">계층 구조는 단원 9에서 나중에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393da-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="393da-148">Hello DimProduct 테이블의 ProductCategoryName 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="393da-149">Hello로 **DimProduct** 여전히 활성 상태 테이블에서 hello **열** 메뉴를 차례로 클릭 **열 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="393da-150">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="393da-151">너무 hello 열 이름 바꾸기**ProductCategoryName**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="393da-152">hello ProductCategoryName에 대 한 계산 된 열에 사용 되는 toocreate hello DimProductCategory 테이블에 hello EnglishProductCategoryName 열에서 데이터를 포함 하는 hello DimProduct 테이블의 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="393da-153">계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="393da-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="393da-154">Hello FactInternetSales 테이블에서 Margin 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="393da-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="393da-155">Hello 모델 디자이너에서 선택 hello **FactInternetSales** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="393da-156">Hello 사이 새 계산된 열 만들기 **SalesAmount** 열과 hello **TaxAmt** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="393da-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="393da-157">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="393da-158">너무 hello 열 이름 바꾸기**여백**합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="393da-160">hello Margin 계산된 열은 사용 되는 tooanalyze 매출 이익률을 각 판매 합니다.</span><span class="sxs-lookup"><span data-stu-id="393da-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="393da-161">다음 작업</span><span class="sxs-lookup"><span data-stu-id="393da-161">What's next?</span></span>
<span data-ttu-id="393da-162">[단원 6: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)</span><span class="sxs-lookup"><span data-stu-id="393da-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
