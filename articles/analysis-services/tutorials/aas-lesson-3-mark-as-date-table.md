---
<span data-ttu-id="85fda-101">제목: aaa "3 Azure Analysis Services 자습서 단원: 날짜 테이블로 표시 | Microsoft Docs "설명: 방법을 toomark 날짜 테이블에 hello Azure Analysis Services tutorial 프로젝트에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-101">title: aaa"Azure Analysis Services tutorial lesson 3: Mark as Date Table | Microsoft Docs" description: Describes how toomark a date table in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="85fda-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="85fda-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="85fda-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="85fda-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="85fda-104">단원 3: 날짜 테이블로 표시</span><span class="sxs-lookup"><span data-stu-id="85fda-104">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="85fda-105">2단원: 데이터 가져오기에서는 이름이 DimDate인 차원 테이블을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-105">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="85fda-106">모델에서 이 테이블의 이름은 DimDate이지만 날짜 및 시간 데이터가 포함되어 있으므로 *날짜 테이블*이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-106">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="85fda-107">DAX 시간 인텔리전스 함수를 사용할 때마다, 나중에 측정값을 만들 때와 같이 *날짜 테이블* 및 해당 테이블에 고유 식별자 *날짜 열*을 포함하는 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-107">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="85fda-108">Hello DimDate 테이블 hello로 표시 하면이 단원에서는 *날짜 테이블* hello 날짜 열 hello 날짜 테이블에 hello로 *날짜 열* (고유 식별자)입니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-108">In this lesson, you mark hello DimDate table as hello *Date table* and hello Date column (in hello Date table) as hello *Date column* (unique identifier).</span></span>  

<span data-ttu-id="85fda-109">Hello 날짜 테이블 및 날짜 열을 표시 하기 전에 모델 보다 쉽게 toounderstand toomake를 약간 à 좋은 시간 toodo 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-109">Before you mark hello date table and date column, it's a good time toodo a little housekeeping toomake your model easier toounderstand.</span></span> <span data-ttu-id="85fda-110">Hello DimDate 테이블에서 명명 된 열을 알 **FullDateAlternateKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-110">Notice in hello DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="85fda-111">이 열 hello 테이블에 포함 된 각 달력 연도의 모든 날에 대 한 하나의 행을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-111">This column contains one row for every day in each calendar year included in hello table.</span></span> <span data-ttu-id="85fda-112">측정 수식 및 보고서에서 이 열을 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-112">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="85fda-113">하지만 실제로 FullDateAlternateKey는 이 열에 대한 적절한 식별자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-113">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="85fda-114">너무 바꾸면**날짜**만들고 쉽게 tooidentify 하 수식에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-114">You rename it too**Date**, making it easier tooidentify and include in formulas.</span></span> <span data-ttu-id="85fda-115">가능 하면 항상 좋습니다 toorename는 개체 테이블 및 열 toomake 같은으로 SSDT 및 Power BI 및 Excel 같은 응용 프로그램을 보고 클라이언트에 보다 쉽게 tooidentify 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-115">Whenever possible, it's a good idea toorename objects like tables and columns toomake them easier tooidentify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="85fda-116">이 단원에서는 시간 toocomplete 예상: **3 분**</span><span class="sxs-lookup"><span data-stu-id="85fda-116">Estimated time toocomplete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="85fda-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="85fda-117">Prerequisites</span></span>  
<span data-ttu-id="85fda-118">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-118">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="85fda-119">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [2 단원: 데이터 가져오기](../tutorials/aas-lesson-2-get-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-119">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="toorename-hello-fulldatealternatekey-column"></a><span data-ttu-id="85fda-120">toorename hello FullDateAlternateKey 열</span><span class="sxs-lookup"><span data-stu-id="85fda-120">toorename hello FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="85fda-121">Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-121">In hello model designer, click hello **DimDate** table.</span></span>

2.  <span data-ttu-id="85fda-122">Hello에 대 한 hello 헤더를 두 번 클릭 **FullDateAlternateKey** 열을 선택한 다음 너무 이름을**날짜**합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-122">Double-click hello header for hello **FullDateAlternateKey** column, and then rename it too**Date**.</span></span>

  
### <a name="tooset-mark-as-date-table"></a><span data-ttu-id="85fda-123">tooset 날짜 테이블로 표시</span><span class="sxs-lookup"><span data-stu-id="85fda-123">tooset Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="85fda-124">선택 hello **날짜** 열을 선택한 다음 hello **속성** 창 아래에서 **데이터 형식**, 있는지 확인 **날짜** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-124">Select hello **Date** column, and then in hello **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="85fda-125">Hello 클릭 **테이블** 메뉴를 클릭 한 다음 **날짜**, 클릭 하 고 **날짜 테이블로 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-125">Click hello **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="85fda-126">Hello에 **날짜 테이블로 표시** 대화 상자의 hello **날짜** 목록 상자에서 선택 hello **날짜** hello 고유 식별자 열입니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-126">In hello **Mark as Date Table** dialog box, in hello **Date** listbox, select hello **Date** column as hello unique identifier.</span></span> <span data-ttu-id="85fda-127">보통은 기본적으로 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-127">It's usually selected by default.</span></span> <span data-ttu-id="85fda-128">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85fda-128">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="85fda-130">다음 작업</span><span class="sxs-lookup"><span data-stu-id="85fda-130">What's next?</span></span>
<span data-ttu-id="85fda-131">[단원 4: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)</span><span class="sxs-lookup"><span data-stu-id="85fda-131">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
