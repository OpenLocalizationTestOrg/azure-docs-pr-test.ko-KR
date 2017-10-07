---
<span data-ttu-id="7cf89-101">제목: aaa "7 Azure Analysis Services 자습서 단원: 핵심 성과 지표 만들기 | Microsoft Docs "설명: 방법을 toocreate 핵심 성과 지표의 hello Azure Analysis Services tutorial 프로젝트에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="7cf89-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="7cf89-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="7cf89-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="7cf89-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="7cf89-104">단원 7: 핵심 성과 지표 만들기</span><span class="sxs-lookup"><span data-stu-id="7cf89-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7cf89-105">이 단원에서는 KPI(핵심 성과 지표)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="7cf89-106">Kpi는 정의 된 값의 사용 되는 toogauge 성능을 *자료* 측정값에 대해는 *대상* 측정값으로 또는 절대값으로 정의 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="7cf89-107">보고 클라이언트 응용 프로그램을 쉽고 빠르게 toounderstand 비즈니스의 성공 또는 tooidentify 추세의 요약이 Kpi 경영진이 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="7cf89-108">toolearn 더 참조 [Kpi](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="7cf89-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="7cf89-109">이 단원에서는 시간 toocomplete 예상: **15 분**</span><span class="sxs-lookup"><span data-stu-id="7cf89-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7cf89-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7cf89-110">Prerequisites</span></span>  
<span data-ttu-id="7cf89-111">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7cf89-112">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [6 단원: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="7cf89-113">핵심 성과 지표 만들기</span><span class="sxs-lookup"><span data-stu-id="7cf89-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="7cf89-114">toocreate InternetCurrentQuarterSalesPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="7cf89-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="7cf89-115">Hello 모델 디자이너에서 클릭 hello **FactInternetSales** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="7cf89-116">Hello 측정값 표에서 빈 셀을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="7cf89-117">Hello 테이블 위에 hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="7cf89-118">이 측정값 hello hello KPI 기본 측정값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="7cf89-119">**InternetCurrentQuarterSalesPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="7cf89-120">Hello KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="7cf89-121">Hello 왼쪽된 (아래쪽) 슬라이더 필드에 입력 **1**, 한 다음 hello 오른쪽 (위쪽) 슬라이더 필드를 입력 **1.07**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="7cf89-122">**아이콘 스타일 선택**원 (녹색) 아이콘 유형의 hello 다이아몬드 (빨간색), 삼각형 (노란색)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="7cf89-124">확장 가능한 알림 hello **설명** hello 가능한 아이콘 스타일 아래에 레이블을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="7cf89-125">Hello에 대 한 설명을 사용 하 여 다양 한 KPI 요소 toomake을 클라이언트 응용 프로그램에서 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="7cf89-126">클릭 **확인** toocomplete hello KPI입니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="7cf89-127">Hello 측정값 표의 hello 아이콘 다음 toohello 확인 **InternetCurrentQuarterSalesPerformance** 측정값입니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="7cf89-128">이 아이콘은 이 측정값이 KPI에 대한 기본값으로 제공됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="7cf89-129">toocreate InternetCurrentQuarterMarginPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="7cf89-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="7cf89-130">Hello에 대 한 측정값 표에서 hello **FactInternetSales** 테이블에서 빈 셀을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="7cf89-131">Hello 테이블 위에 hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="7cf89-132">**InternetCurrentQuarterMarginPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="7cf89-133">Hello KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.25**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="7cf89-134">Hello 필드 표시 될 때까지 슬라이드 hello 왼쪽된 (아래쪽) 슬라이더 필드에서 **0.8**, 및 hello 필드 표시 될 때까지 다음 슬라이드 hello 오른쪽 (높음) 슬라이더 필드 **1.03**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="7cf89-135">**아이콘 스타일 선택**, hello 다이아몬드 (빨간색), 삼각형 (노란색), 원 (녹색) 아이콘 유형을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7cf89-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="7cf89-136">다음 작업</span><span class="sxs-lookup"><span data-stu-id="7cf89-136">What's next?</span></span>
<span data-ttu-id="7cf89-137">[단원 8: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)</span><span class="sxs-lookup"><span data-stu-id="7cf89-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
