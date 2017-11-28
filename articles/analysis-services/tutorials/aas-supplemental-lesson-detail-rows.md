---
<span data-ttu-id="862e6-101">제목: aaa "Azure Analysis Services tutorial 추가 단원: 정보 행 | Microsoft Docs "설명: toocreate 세부 행 식에는 Azure Analysis Services 자습서 hello 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="862e6-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="862e6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="862e6-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="862e6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="862e6-104">추가 단원 - 세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="862e6-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="862e6-105">이 추가 단원에서는 DAX 편집기 toodefine hello는 사용자 지정 세부 행 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="862e6-106">세부 정보 행 식 최종 사용자에 게 hello 집계 결과 측정값에 대 한 자세한 정보를 제공 하는 측정값에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="862e6-107">이 단원에서는 시간 toocomplete 예상: **10 분**</span><span class="sxs-lookup"><span data-stu-id="862e6-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="862e6-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="862e6-108">Prerequisites</span></span>  
<span data-ttu-id="862e6-109">이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="862e6-110">이 추가 단원 hello 작업을 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="862e6-111">수행할 작업 toosolve 필요?</span><span class="sxs-lookup"><span data-stu-id="862e6-111">What do we need toosolve?</span></span>
<span data-ttu-id="862e6-112">세부 정보 행 식을 추가 하기 전에 InternetTotalSales 측정값의 hello 세부 정보에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="862e6-113">SSDT에서는 hello 클릭 **모델** 메뉴 > **Excel에서 분석** tooopen Excel 빈 피벗 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="862e6-114">**피벗 테이블 필드**, hello 추가 **InternetTotalSales** 너무 hello FactInternetSales 테이블에서 측정**값**, **CalendarYear**hello DimDate 테이블에서 너무**열**, 및 **EnglishCountryRegionName** 너무**행**합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="862e6-115">이 피벗 테이블 이제 목록에 집계 된 결과 영역 및 연도별 hello InternetTotalSales 측정값에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="862e6-117">Hello 피벗 테이블에서 지역 이름과 1 년에 대 한 집계 값을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="862e6-118">여기에서는 두 번 클릭 hello 값 오스트레일리아 및 hello에 대 한 2014 년입니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="862e6-119">데이터가 포함된 새 시트가 열리지만 유용한 데이터가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="862e6-121">여기 toosee toohello 기여 하는 데이터의 열과 행을 포함 하는 테이블 처럼 사람이 무엇 InternetTotalSales 측정값의 결과 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="862e6-122">toodo을, hello 측정값의 속성으로 정보 행 식을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="862e6-123">세부 정보 행 식 추가</span><span class="sxs-lookup"><span data-stu-id="862e6-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="862e6-124">toocreate 세부 행 식</span><span class="sxs-lookup"><span data-stu-id="862e6-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="862e6-125">SSDT에서는 hello FactInternetSales 테이블의 측정값 표 클릭 hello **InternetTotalSales** 측정값입니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="862e6-126">**속성** > **세부 행 식**, hello 편집기 단추 tooopen hello DAX 편집기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="862e6-128">DAX 편집기에서 다음 식은 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-128">In DAX Editor, enter hello following expression:</span></span>

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

    <span data-ttu-id="862e6-129">이 식 이름, 열를 지정 하 고 사용자가 피벗 테이블 또는 보고서에는 집계 된 결과 두 번 클릭할 경우 hello FactInternetSales 테이블과 관련된 테이블에서 측정값 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="862e6-130">다시 Excel, 3 단계에서에서 만든 hello 시트 삭제 한 후 집계 값을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="862e6-131">이 이번에 hello 측정값에 대해 정의 된 세부 행 식 속성을 새 시트가 열립니다 훨씬 더 유용한 데이터가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="862e6-133">모델을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="862e6-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="862e6-134">참고 항목</span><span class="sxs-lookup"><span data-stu-id="862e6-134">See Also</span></span>  
<span data-ttu-id="862e6-135">[SELECTCOLUMNS 함수(DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="862e6-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="862e6-136">추가 단원 - 동적 보안</span><span class="sxs-lookup"><span data-stu-id="862e6-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="862e6-137">추가 단원 - 불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="862e6-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
