---
<span data-ttu-id="b7a93-101">제목: aaa "12 Azure Analysis Services 자습서 단원: Excel에서 분석 | Microsoft Docs "설명: Azure Analysis Services 하는 hello에 toouse Excel에서 분석 방법에 대해 설명 tutorial 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b7a93-101">title: aaa"Azure Analysis Services tutorial lesson 12: Analyze in Excel | Microsoft Docs" description: Describes how toouse Analyze in Excel in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="b7a93-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="b7a93-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b7a93-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="b7a93-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="b7a93-104">단원 12: Excel에서 분석</span><span class="sxs-lookup"><span data-stu-id="b7a93-104">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b7a93-105">Excel 기능은 tooopen Microsoft Excel에서에서 분석 hello를 사용 하 여이 단원에서는 자동으로 연결 toohello 모델 작업 영역 만들기 및 자동으로 피벗 테이블 toohello 워크시트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-105">In this lesson, you use hello Analyze in Excel feature tooopen Microsoft Excel, automatically create a connection toohello model workspace, and automatically add a PivotTable toohello worksheet.</span></span> <span data-ttu-id="b7a93-106">기능은 Excel에서 분석 hello tooprovide 사용 되므로 모델의 쉽고 빠르게 tootest hello 효율성 이전 toodeploying 모델을 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-106">hello Analyze in Excel feature is meant tooprovide a quick and easy way tootest hello efficacy of your model design prior toodeploying your model.</span></span> <span data-ttu-id="b7a93-107">이 단원에서는 어떠한 데이터 분석도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-107">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="b7a93-108">이 단원에서는의 hello 목적은 toofamiliarize hello 모델을 작성, hello 도구와 함께 사용할 수 있습니다 tootest 모델 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-108">hello purpose of this lesson is toofamiliarize you, hello model author, with hello tools you can use tootest your model design.</span></span>   
  
<span data-ttu-id="b7a93-109">이 단원에서는 Excel hello에 설치 해야 toocomplete SSDT와 같은 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="b7a93-109">toocomplete this lesson, Excel must be installed on hello same computer as SSDT.</span></span>
  
<span data-ttu-id="b7a93-110">이 단원에서는 시간 toocomplete 예상: **5 분**</span><span class="sxs-lookup"><span data-stu-id="b7a93-110">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b7a93-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b7a93-111">Prerequisites</span></span>  
<span data-ttu-id="b7a93-112">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b7a93-113">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [11 단원: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a><span data-ttu-id="b7a93-114">Hello 기본 및 인터넷 판매 큐브 뷰를 사용 하 여 찾아보기</span><span class="sxs-lookup"><span data-stu-id="b7a93-114">Browse using hello Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="b7a93-115">이러한 첫 번째 작업에서 모델을 찾으면 프로그램 모든 모델 개체를 포함 하는 두 hello 기본 큐브를 사용 하 여 및 hello Internet Sales 큐브 뷰를 사용 하 여 앞서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-115">In these first tasks, you browse your model by using both hello default perspective, which includes all model objects, and also by using hello Internet Sales perspective you earlier.</span></span> <span data-ttu-id="b7a93-116">hello Internet Sales 큐브 뷰는 hello Customer 테이블 개체가 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-116">hello Internet Sales perspective excludes hello Customer table object.</span></span>  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a><span data-ttu-id="b7a93-117">hello 기본 큐브 뷰를 사용 하 여 toobrowse</span><span class="sxs-lookup"><span data-stu-id="b7a93-117">toobrowse by using hello Default perspective</span></span>  
  
1.  <span data-ttu-id="b7a93-118">Hello 클릭 **모델** 메뉴 > **Excel에서 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-118">Click hello **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="b7a93-119">Hello에 **Excel에서 분석** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-119">In hello **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="b7a93-120">Excel에서 새 통합 문서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-120">Excel opens with a new workbook.</span></span> <span data-ttu-id="b7a93-121">Hello 기본 큐브는 사용 되는 toodefine 보기 가능한 필드와 데이터 원본 연결을 hello 현재 사용자 계정을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-121">A data source connection is created using hello current user account and hello Default perspective is used toodefine viewable fields.</span></span> <span data-ttu-id="b7a93-122">피벗 테이블 toohello 워크시트를 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-122">A PivotTable is automatically added toohello worksheet.</span></span>  
  
3.  <span data-ttu-id="b7a93-123">Excel의 hello **피벗 테이블 필드 목록**, 통지 hello **DimDate** 및 **FactInternetSales** 측정값 그룹에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-123">In Excel, in hello **PivotTable Field List**, notice hello **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="b7a93-124">hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales** 해당 열이 있는 테이블도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-124">hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="b7a93-125">Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-125">Close Excel without saving hello workbook.</span></span>  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a><span data-ttu-id="b7a93-126">hello Internet Sales 큐브 뷰를 사용 하 여 toobrowse</span><span class="sxs-lookup"><span data-stu-id="b7a93-126">toobrowse by using hello Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="b7a93-127">Hello 클릭 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-127">Click hello **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="b7a93-128">Hello에 **Excel에서 분석** 대화 상자 **현재 Windows 사용자** 선택 되 면 다음 hello **관점** 드롭 다운 목록 상자에서 **인터넷 판매** , 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-128">In hello **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in hello **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="b7a93-130">Excel에서의 **피벗 테이블 필드**, hello DimCustomer 테이블은 hello 필드 목록에서 제외를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-130">In Excel, in **PivotTable Fields**, notice hello DimCustomer table is excluded from hello field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="b7a93-132">Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-132">Close Excel without saving hello workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="b7a93-133">역할을 사용하여 찾아보기</span><span class="sxs-lookup"><span data-stu-id="b7a93-133">Browse by using roles</span></span>  
<span data-ttu-id="b7a93-134">역할은 테이블 형식 모델의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-134">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="b7a93-135">하나 이상의 역할이 없는 toowhich 사용자가을 구성원으로 추가 사용자가 액세스를 업데이트 하 고 모델을 사용 하 여 데이터를 분석할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-135">Without at least one role toowhich users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="b7a93-136">기능은 Excel에서 분석 hello는 하기 위한 방법을 제공 하면 정의한 tootest hello 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-136">hello Analyze in Excel feature provides a way for you tootest hello roles you have defined.</span></span>  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a><span data-ttu-id="b7a93-137">hello Sales Manager 사용자 역할을 사용 하 여 toobrowse</span><span class="sxs-lookup"><span data-stu-id="b7a93-137">toobrowse by using hello Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="b7a93-138">SSDT에서는 hello 클릭 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-138">In SSDT, click hello **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="b7a93-139">**지정 hello 사용자 이름 또는 역할 toouse tooconnect toohello 모델**선택, **역할**, hello 드롭다운 목록 상자에서 선택 **판매 관리자**, 를클릭한다음 **정상**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-139">In **Specify hello user name or role toouse tooconnect toohello model**, select **Role**, and then in hello drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="b7a93-140">Excel에서 새 통합 문서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-140">Excel opens with a new workbook.</span></span> <span data-ttu-id="b7a93-141">피벗 테이블이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-141">A PivotTable is automatically created.</span></span> <span data-ttu-id="b7a93-142">hello 피벗 테이블 필드 목록에 새 모델에서 사용 가능한 모든 hello 데이터 필드에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-142">hello Pivot Table Field List includes all hello data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="b7a93-143">Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-143">Close Excel without saving hello workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="b7a93-144">다음 작업</span><span class="sxs-lookup"><span data-stu-id="b7a93-144">What's next?</span></span>
<span data-ttu-id="b7a93-145">다음 단원 이동 toohello: [13 단원: 배포](../tutorials/aas-lesson-13-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a93-145">Go toohello next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
