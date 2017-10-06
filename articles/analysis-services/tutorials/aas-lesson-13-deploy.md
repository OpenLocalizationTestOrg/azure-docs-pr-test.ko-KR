---
<span data-ttu-id="ac358-101">제목: aaa "Azure Analysis Services 자습서 단원인 13: 배포 | Microsoft Docs "설명: toodeploy hello 자습서 tooAzure Analysis Services 프로젝트 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="ac358-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="ac358-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="ac358-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="ac358-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="ac358-104">단원 13: 배포</span><span class="sxs-lookup"><span data-stu-id="ac358-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ac358-105">이 단원에서는 배포 속성 구성 Azure Analysis Services 서버 toodeploy tooand hello 모델의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="ac358-106">그런 다음 hello 모델 toothat 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="ac358-107">모델 배포 된 후 사용자가 보고 클라이언트 응용 프로그램을 사용 하 여 tooit를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="ac358-108">toolearn 더 참조 [tooAzure Analysis Services 배포](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="ac358-109">이 단원에서는 시간 toocomplete 예상: **5 분**</span><span class="sxs-lookup"><span data-stu-id="ac358-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ac358-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ac358-110">Prerequisites</span></span>  
<span data-ttu-id="ac358-111">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ac358-112">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [12 단원: Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="ac358-113">있어야 [관리자 권한을](../analysis-services-server-admins.md) on hello 원격 Analysis Services 서버 순서로 toodeploy tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="ac358-114">온-프레미스 SQL Server에 hello AdventureWorksDW2014 예제 데이터베이스를 설치 하 고 모델 tooan Azure Analysis Services 서버를 배포 하는 경우는 [온-프레미스 데이터 게이트웨이](../analysis-services-gateway.md) 가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="ac358-115">Hello 모델 배포</span><span class="sxs-lookup"><span data-stu-id="ac358-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="ac358-116">tooconfigure 배포 속성</span><span class="sxs-lookup"><span data-stu-id="ac358-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="ac358-117">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트를 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="ac358-118">Hello에 **AW Internet Sales 속성 페이지** 대화 상자의 **배포 서버**, hello에 **서버** 속성 hello 전체 서버를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="ac358-120">Hello에 **데이터베이스** 속성을 입력 **Adventure Works Internet Sales**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="ac358-121">Hello에 **모델 이름** 속성을 입력 **Adventure Works Internet Sales Model**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="ac358-122">선택 내용을 확인한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="ac358-123">toodeploy hello Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="ac358-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="ac358-124">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트 > **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="ac358-125">마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트 > **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="ac358-126">다음과 같은 행위는 tooAzure Analysis Services를 배포할 때는 증명된 tooenter 사용자 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="ac358-127">조직의 계정 및 암호를 입력합니다(예: nancy@adventureworks.com). 이 계정은 hello 서버에서 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="ac358-128">hello 배포 대화 상자가 표시 되 고 hello 메타 데이터의 배포 상태 hello 및 hello 모델에 포함 된 각 테이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="ac358-130">배포가 성공적으로 완료되면 진행하고 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="ac358-131">결론</span><span class="sxs-lookup"><span data-stu-id="ac358-131">Conclusion</span></span>  
<span data-ttu-id="ac358-132">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-132">Congratulations!</span></span> <span data-ttu-id="ac358-133">첫 번째 Analysis Services 테이블 형식 모델의 작성 및 배포가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="ac358-134">이 자습서에서는 도움이 hello 테이블 형식 모델을 만드는 가장 일반적인 작업을 완료 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="ac358-135">Adventure Works Internet Sales 모델을 배포 했으므로, SQL Server Management Studio toomanage hello 모델을 사용할 수 있습니다. 처리 스크립트와 백업 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="ac358-136">사용자가 Microsoft Excel 또는 Power BI와 같은 보고 클라이언트 응용 프로그램을 사용 하 여 toohello 모델을 연결할 이제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac358-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="ac358-138">다음 작업</span><span class="sxs-lookup"><span data-stu-id="ac358-138">What's next?</span></span>
<span data-ttu-id="ac358-139">[Power BI Desktop으로 연결](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="ac358-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="ac358-140">[추가 단원 - 동적 보안](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="ac358-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="ac358-141">[추가 단원 - 세부 정보 행](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="ac358-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="ac358-142">추가 단원 - 불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="ac358-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
