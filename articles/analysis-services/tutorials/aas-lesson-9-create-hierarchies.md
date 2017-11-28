---
<span data-ttu-id="d3f15-101">제목: aaa "9 Azure Analysis Services 자습서 단원: 계층 만들기 | Microsoft Docs "설명: 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="d3f15-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d3f15-102">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d3f15-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="d3f15-103">단원 9: 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="d3f15-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d3f15-104">이 단원에서는 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="d3f15-105">계층 구조는 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층 구조는 Country, State, County 및 City에 대한 하위 수준을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="d3f15-106">계층 더 쉽게 클라이언트에 대 한 사용자가 toonavigate 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과에서는 별도로 표시 및 보고서에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="d3f15-107">toolearn 더 참조 [계층](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="d3f15-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="d3f15-108">toocreate 계층 hello 모델 디자이너에서 사용 하 여 *다이어그램 보기*합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="d3f15-109">데이터 뷰에서 계층 구조 만들기 및 관리는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="d3f15-110">이 단원에서는 시간 toocomplete 예상: **20 분**</span><span class="sxs-lookup"><span data-stu-id="d3f15-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d3f15-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3f15-111">Prerequisites</span></span>  
<span data-ttu-id="d3f15-112">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d3f15-113">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [8 단원: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="d3f15-114">계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="d3f15-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="d3f15-115">toocreate hello DimProduct 테이블의 범주 계층</span><span class="sxs-lookup"><span data-stu-id="d3f15-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="d3f15-116">Hello를 마우스 오른쪽 단추로 클릭 hello 모델 디자이너 (다이어그램 뷰)에서 **DimProduct** 테이블 > **계층 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="d3f15-117">새 계층 hello hello 테이블 창의 맨 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="d3f15-118">Hello 계층 이름 바꾸기 **범주**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="d3f15-119">클릭 하 고 hello 끌어 **ProductCategoryName** 새 열 toohello **범주** 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="d3f15-120">Hello에 **범주** 계층, 마우스 오른쪽 단추로 클릭 hello **ProductCategoryName** > **이름 바꾸기**, 한 다음 입력 **범주**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="d3f15-121">계층의 열 이름 바꾸기 hello 테이블의 해당 열은 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="d3f15-122">계층의 열은 hello 열 hello 테이블에 대 한 표현일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="d3f15-123">클릭 하 고 hello 끌어 **ProductSubcategoryName** 열 toohello **범주** 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="d3f15-124">**Subcategory**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="d3f15-125">마우스 오른쪽 단추로 클릭 hello **ModelName** 열 > **toohierarchy 추가**를 선택한 후 **범주**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="d3f15-126">**Model**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="d3f15-127">마지막으로 추가 **EnglishProductName** toohello 범주 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="d3f15-128">**Product**로 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="d3f15-130">hello DimDate 테이블에서 toocreate 계층</span><span class="sxs-lookup"><span data-stu-id="d3f15-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="d3f15-131">Hello에 **DimDate** 테이블, 명명 된 계층 구조를 만들 **달력**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="d3f15-132">Hello 다음 순서 대로 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="d3f15-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="d3f15-133">CalendarYear</span></span>
    *  <span data-ttu-id="d3f15-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="d3f15-134">CalendarSemester</span></span>
    *  <span data-ttu-id="d3f15-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="d3f15-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="d3f15-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="d3f15-136">MonthCalendar</span></span>
    *  <span data-ttu-id="d3f15-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="d3f15-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="d3f15-138">Hello에 **DimDate** 테이블을 만들기는 **회계** 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="d3f15-139">다음 순서 대로 열 hello를 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="d3f15-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="d3f15-140">FiscalYear</span></span>
    *  <span data-ttu-id="d3f15-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="d3f15-141">FiscalSemester</span></span>
    *  <span data-ttu-id="d3f15-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="d3f15-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="d3f15-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="d3f15-143">MonthCalendar</span></span>
    *  <span data-ttu-id="d3f15-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="d3f15-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="d3f15-145">Hello에 마지막으로, **DimDate** 테이블을 만들기는 **ProductionCalendar** 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="d3f15-146">다음 순서 대로 열 hello를 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3f15-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="d3f15-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="d3f15-147">CalendarYear</span></span>
    *  <span data-ttu-id="d3f15-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="d3f15-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="d3f15-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="d3f15-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="d3f15-150">다음 작업</span><span class="sxs-lookup"><span data-stu-id="d3f15-150">What's next?</span></span>
<span data-ttu-id="d3f15-151">[단원 10: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)</span><span class="sxs-lookup"><span data-stu-id="d3f15-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
