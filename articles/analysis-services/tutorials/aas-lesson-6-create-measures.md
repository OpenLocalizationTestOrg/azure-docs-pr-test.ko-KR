---
<span data-ttu-id="96905-101">제목: aaa "6 Azure Analysis Services 자습서 단원: 측정값 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트에 측정 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="96905-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="96905-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="96905-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="96905-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="96905-104">단원 6: 측정값 만들기</span><span class="sxs-lookup"><span data-stu-id="96905-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="96905-105">이 단원에서는 모델에 포함할 측정값 toobe를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="96905-106">비슷한 toohello 계산 만든 열, 측정값은 DAX 수식을 사용 하 여 만든 계산입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="96905-107">그러나 계산된 열과 달리 측정값은 사용자가 선택한 *필터*를 기반으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="96905-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="96905-108">예를 들어 특정 열 이나 슬라이서 toohello 행 레이블 필드 피벗 테이블에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="96905-109">Hello 필터의 각 셀에 대 한 값이 적용 된 hello 측정값으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96905-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="96905-110">측정값은 숫자 데이터에 대해 거의 모든 테이블 형식 모델 tooperform 동적 계산에서 tooinclude 되도록 하는 강력 하 고 유연한 계산입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="96905-111">toolearn 더 참조 [측정값](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular)합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="96905-112">hello를 사용 하면 toocreate 측정값 *측정값 표*합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="96905-113">기본적으로 각 테이블에는 빈 측정값 표가 있습니다. 그러나 일반적으로 모든 테이블에 대해 측정값을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="96905-114">데이터 보기 hello 모델 디자이너에서 테이블 아래 hello 측정값 표가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96905-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="96905-115">표시 / toohide hello 측정값 표는 테이블에 대 한 클릭 hello **테이블** 메뉴를 차례로 클릭 **측정값 표 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="96905-116">Hello 측정값 표에서 빈 셀을 클릭 하 고 hello 수식 입력줄에 DAX 수식을 입력 하 여 측정값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="96905-117">ENTER toocomplete hello 수식 hello 측정값 클릭 후 hello 셀에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96905-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="96905-118">열을 클릭 하 여 표준 집계 함수를 사용 하 여 측정값을 만들 수 있습니다 및 자동 합계 단추 hello 클릭 한 다음 (**∑**) hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="96905-119">Hello 자동 합계 기능을 이용해 만든 측정값 hello 측정값 표 셀 hello 열 바로 아래에 표시 되지만 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="96905-120">이 단원에서는 둘 다 DAX 수식을 입력 hello 수식 입력줄에 고 hello 자동 합계 기능을 사용 하 여 측정값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96905-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="96905-121">이 단원에서는 시간 toocomplete 예상: **30 분**</span><span class="sxs-lookup"><span data-stu-id="96905-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="96905-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="96905-122">Prerequisites</span></span>  
<span data-ttu-id="96905-123">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="96905-124">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [5 단원: 계산된 열 만들기](../tutorials/aas-lesson-5-create-calculated-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="96905-125">측정값 만들기</span><span class="sxs-lookup"><span data-stu-id="96905-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="96905-126">toocreate hello DimDate 테이블의 DaysCurrentQuarterToDate 측정값</span><span class="sxs-lookup"><span data-stu-id="96905-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="96905-127">Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="96905-128">Hello 측정값 표의 hello 왼쪽 위 빈 셀을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="96905-129">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="96905-130">공지 hello 왼쪽 위 셀에는 이제 측정값 이름 포함 **DaysCurrentQuarterToDate**hello 결과 **92**합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="96905-132">측정값 수식으로 계산 된 열과 달리 hello 측정값 이름, 밑줄 hello 수식 식 뒤에 오는 콜론을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="96905-133">toocreate hello DimDate 테이블의 DaysInCurrentQuarter 측정값</span><span class="sxs-lookup"><span data-stu-id="96905-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="96905-134">Hello로 **DimDate** hello 측정값 표의 hello 모델 디자이너에서 계속 활성 상태 테이블을 hello 만든 hello 측정값 아래의 빈 셀을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="96905-135">Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="96905-136">이 이전 기간의 불완전 한 기간과 hello 사이의 비교 비율을 만들 때는</span><span class="sxs-lookup"><span data-stu-id="96905-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="96905-137">hello 수식은 경과 된 hello 기간의 hello 비율을 계산 하 고 toohello 이전 기간의 hello에는 동일한 비율을 비교 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="96905-138">이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 제공 hello 비율 hello 현재 기간 경과 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="96905-139">toocreate hello FactInternetSales 테이블의 한 InternetDistinctCountSalesOrder 측정값</span><span class="sxs-lookup"><span data-stu-id="96905-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="96905-140">Hello 클릭 **FactInternetSales** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="96905-141">Hello 클릭 **SalesOrderNumber** 열 머리글입니다.</span><span class="sxs-lookup"><span data-stu-id="96905-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="96905-142">Hello 도구 모음에서 hello 아래쪽 화살표 다음 toohello 자동 합계 (**∑**) 단추를 선택한 다음 선택 **DistinctCount**합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="96905-143">hello 자동 합계 기능은 DistinctCount 표준 집계 수식을 hello를 사용 하 여 hello 선택한 열에 대 한 측정값을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96905-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="96905-145">Hello 측정값 표의 hello 새 측정값을 클릭 한 다음 hello **속성** 창, **측정값 이름**, 너무 hello 측정값 이름을 바꿀**InternetDistinctCountSalesOrder**합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="96905-146">hello FactInternetSales 테이블에서 추가 측정이 toocreate</span><span class="sxs-lookup"><span data-stu-id="96905-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="96905-147">Hello 자동 합계 기능을 사용 하 여 만들고 hello 다음 측정값 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="96905-148">열</span><span class="sxs-lookup"><span data-stu-id="96905-148">Column</span></span>|<span data-ttu-id="96905-149">측정값 이름</span><span class="sxs-lookup"><span data-stu-id="96905-149">Measure name</span></span>|<span data-ttu-id="96905-150">자동 합계(∑)</span><span class="sxs-lookup"><span data-stu-id="96905-150">AutoSum (∑)</span></span>|<span data-ttu-id="96905-151">수식</span><span class="sxs-lookup"><span data-stu-id="96905-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="96905-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="96905-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="96905-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="96905-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="96905-154">개수</span><span class="sxs-lookup"><span data-stu-id="96905-154">Count</span></span>|<span data-ttu-id="96905-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="96905-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="96905-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="96905-156">OrderQuantity</span></span>|<span data-ttu-id="96905-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="96905-157">InternetTotalUnits</span></span>|<span data-ttu-id="96905-158">합계</span><span class="sxs-lookup"><span data-stu-id="96905-158">Sum</span></span>|<span data-ttu-id="96905-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="96905-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="96905-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="96905-160">DiscountAmount</span></span>|<span data-ttu-id="96905-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="96905-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="96905-162">합계</span><span class="sxs-lookup"><span data-stu-id="96905-162">Sum</span></span>|<span data-ttu-id="96905-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="96905-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="96905-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="96905-164">TotalProductCost</span></span>|<span data-ttu-id="96905-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="96905-165">InternetTotalProductCost</span></span>|<span data-ttu-id="96905-166">합계</span><span class="sxs-lookup"><span data-stu-id="96905-166">Sum</span></span>|<span data-ttu-id="96905-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="96905-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="96905-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="96905-168">SalesAmount</span></span>|<span data-ttu-id="96905-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="96905-169">InternetTotalSales</span></span>|<span data-ttu-id="96905-170">합계</span><span class="sxs-lookup"><span data-stu-id="96905-170">Sum</span></span>|<span data-ttu-id="96905-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="96905-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="96905-172">Margin</span><span class="sxs-lookup"><span data-stu-id="96905-172">Margin</span></span>|<span data-ttu-id="96905-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="96905-173">InternetTotalMargin</span></span>|<span data-ttu-id="96905-174">합계</span><span class="sxs-lookup"><span data-stu-id="96905-174">Sum</span></span>|<span data-ttu-id="96905-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="96905-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="96905-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="96905-176">TaxAmt</span></span>|<span data-ttu-id="96905-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="96905-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="96905-178">합계</span><span class="sxs-lookup"><span data-stu-id="96905-178">Sum</span></span>|<span data-ttu-id="96905-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="96905-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="96905-180">Freight</span><span class="sxs-lookup"><span data-stu-id="96905-180">Freight</span></span>|<span data-ttu-id="96905-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="96905-181">InternetTotalFreight</span></span>|<span data-ttu-id="96905-182">합계</span><span class="sxs-lookup"><span data-stu-id="96905-182">Sum</span></span>|<span data-ttu-id="96905-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="96905-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="96905-184">클릭 하 여 hello 측정값 표의 및 hello 수식 입력줄을 사용 하 여 빈 셀, 만들고 hello 다음 이름을 순서 대로 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96905-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="96905-185">Hello FactInternetSales 테이블에 대해 만든 측정값 매출, 비용, 이익률 hello 사용자가 선택한 필터로 필터링 된 항목 등 중요 한 재무 데이터를 사용 하는 tooanalyze 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96905-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="96905-186">다음 작업</span><span class="sxs-lookup"><span data-stu-id="96905-186">What's next?</span></span>
<span data-ttu-id="96905-187">[단원 7: 핵심 성과 지표 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)</span><span class="sxs-lookup"><span data-stu-id="96905-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
