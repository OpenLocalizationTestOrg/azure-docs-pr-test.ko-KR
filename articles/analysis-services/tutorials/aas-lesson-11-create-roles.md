---
<span data-ttu-id="d16cc-101">제목: aaa "11 Azure Analysis Services 자습서 단원: 역할 만들기 | Microsoft Docs "설명: toocreate 역할에서 Azure Analysis Services tutorial 프로젝트를 hello 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="d16cc-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="d16cc-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d16cc-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d16cc-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="d16cc-104">단원 11: 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="d16cc-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d16cc-105">이 단원에서는 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-105">In this lesson, you create roles.</span></span> <span data-ttu-id="d16cc-106">역할 제공 모델 데이터베이스 개체 및 데이터 보안 tooonly 액세스를 제한 하 여 해당 사용자 역할 구성원 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="d16cc-107">각 역할은 단일 사용 권한(없음, 읽기, 읽기 및 프로세스, 프로세스 또는 관리자)으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="d16cc-108">역할 관리자를 사용하여 모델 작성 중에 역할을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="d16cc-109">모델을 배포한 후에는 SSMS(SQL Server Management Studio)를 사용하여 역할을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="d16cc-110">toolearn 더 참조 [역할](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="d16cc-111">역할을 만드는 필요 하지 않은 toocomplete이이 자습서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="d16cc-112">기본적으로 현재 로그인 하는 hello 계정 관리자에 대 한 권한이 hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="d16cc-113">그러나 다른 사용자는 보고 클라이언트를 사용 하 여 조직 toobrowse 프로그램에 대 한 사용 권한을 읽기 역할을 하나 이상 만들 하며 해당 사용자가 구성원으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="d16cc-114">세 가지 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="d16cc-115">**영업 관리자** –이 역할을 구하려는 toohave 읽기 권한 tooall 모델 개체와 데이터 조직에서 사용자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="d16cc-116">**Sales Analyst US** –이 역할 toobe 수 toobrowse 데이터만 사용 하도록 하려는 조직에서 사용자를 포함할 수 있습니다 toosales hello 미국에에서 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="d16cc-117">DAX 수식 toodefine를 사용 하면이 역할에 대 한 *행 필터*, 미국 hello에 대 한 멤버 toobrowse 데이터 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="d16cc-118">**관리자** –이 역할은 hello model 데이터베이스에서 무제한 액세스 및 사용 권한 tooperform 관리 작업을 허용 toohave 관리자 권한을 사용 하도록 하려는 사용자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="d16cc-119">조직의 Windows 사용자 및 그룹 계정은 고유 하므로 특정 조직 toomembers에서 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="d16cc-120">그러나이 자습서에서는 수 또한 hello 멤버 비워 두면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="d16cc-121">나중에 12 단원 각 역할의 hello 효과 테스트할: Excel에서 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="d16cc-122">이 단원에서는 시간 toocomplete 예상: **15 분**</span><span class="sxs-lookup"><span data-stu-id="d16cc-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d16cc-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d16cc-123">Prerequisites</span></span>  
<span data-ttu-id="d16cc-124">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d16cc-125">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [10 단원: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="d16cc-126">역할 만들기</span><span class="sxs-lookup"><span data-stu-id="d16cc-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="d16cc-127">toocreate Sales Manager 사용자 역할</span><span class="sxs-lookup"><span data-stu-id="d16cc-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="d16cc-128">테이블 형식 모델 탐색기에서 **역할** > **역할**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="d16cc-129">역할 관리자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="d16cc-130">Hello 새 역할을 클릭 한 다음 hello **이름** 열을 너무 hello 역할 이름 바꾸기**판매 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="d16cc-131">Hello에 **사용 권한을** 열에서 hello 드롭다운 목록에서를 클릭 한 다음 hello 선택 **읽기** 권한.</span><span class="sxs-lookup"><span data-stu-id="d16cc-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="d16cc-133">선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="d16cc-134">Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="d16cc-135">toocreate Sales Analyst US 사용자 역할</span><span class="sxs-lookup"><span data-stu-id="d16cc-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="d16cc-136">역할 관리자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="d16cc-137">너무 hello 역할 이름 바꾸기**Sales Analyst US**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="d16cc-138">이 역할에 **읽기** 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="d16cc-139">Hello 행 필터 탭을 클릭 하 고 hello에 대 한 다음 **DimGeography** 다음 수식을 형식 hello hello DAX 필터 열에만 테이블:</span><span class="sxs-lookup"><span data-stu-id="d16cc-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="d16cc-140">행 필터 수식은 tooa 부울 (TRUE/FALSE) 값을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="d16cc-141">이 수식을 사용 하 여 행만 hello Country Region Code 값 "미국" 되는지 표시 toohello 사용자 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="d16cc-143">선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="d16cc-144">Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="d16cc-145">toocreate 관리자 사용자 역할</span><span class="sxs-lookup"><span data-stu-id="d16cc-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="d16cc-146">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="d16cc-147">너무 hello 역할 이름 바꾸기**관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="d16cc-148">이 역할에 **관리자** 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="d16cc-149">선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="d16cc-150">Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d16cc-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="d16cc-151">다음 작업</span><span class="sxs-lookup"><span data-stu-id="d16cc-151">What's next?</span></span>
<span data-ttu-id="d16cc-152">[단원 12: Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="d16cc-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
