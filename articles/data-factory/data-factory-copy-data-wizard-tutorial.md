---
title: "자습서: 복사 마법사를 사용하여 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure 데이터 팩터리 파이프라인 복사 활동으로 사용 하 여 만들면 hello Data Factory에서 지 원하는 복사 마법사"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="9d771-103">자습서: 데이터 팩터리 복사 마법사를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="9d771-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d771-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9d771-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9d771-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="9d771-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9d771-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9d771-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9d771-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d771-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9d771-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d771-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9d771-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="9d771-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9d771-110">REST API</span><span class="sxs-lookup"><span data-stu-id="9d771-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9d771-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="9d771-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="9d771-112">이 자습서에서는 어떻게 toouse hello **복사 마법사** toocopy 데이터를 Azure blob 저장소 tooan Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="9d771-113">Azure Data Factory hello **복사 마법사** 있습니다 tooquickly 지원 되는 원본 데이터 저장소 지원 tooa 대상 데이터 저장소에서 데이터를 복사 하는 데이터 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="9d771-114">따라서 데이터 이동 시나리오에 대 한 첫 번째 단계 toocreate 샘플 파이프라인으로 hello 마법사를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="9d771-115">원본 및 대상으로 지원되는 데이터 저장소의 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d771-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="9d771-116">이 자습서에서는 어떻게 toocreate Azure 데이터 팩터리에 시작 hello 복사 마법사는 일련의 데이터 수집/이동 시나리오에 대 한 단계 tooprovide 정보를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="9d771-117">Hello 마법사의 단계를 완료 하면 hello 마법사 파이프라인 Azure blob 저장소 tooan Azure SQL 데이터베이스의 복사 작업 toocopy 데이터로 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="9d771-118">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d771-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d771-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9d771-119">Prerequisites</span></span>
<span data-ttu-id="9d771-120">Hello에 나온 필수 조건을 완료 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="9d771-121">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="9d771-121">Create data factory</span></span>
<span data-ttu-id="9d771-122">이 단계를 사용 하 여 Azure 포털 toocreate 라는 Azure 데이터 팩터리에 hello **ADFTutorialDataFactory**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="9d771-123">로그 너무[Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9d771-124">클릭 **+ 새로 만들기** hello 왼쪽 위 모퉁이에서 클릭 **데이터 + 분석**를 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="9d771-126">Hello에 **새 데이터 팩터리** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="9d771-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="9d771-127">입력 **ADFTutorialDataFactory** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="9d771-128">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="9d771-129">Hello 오류가 나타나면: `Data factory name “ADFTutorialDataFactory” is not available`을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFTutorialDataFactoryYYYYMMDD)을 변경 하 고 다시 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9d771-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="9d771-130">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d771-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="9d771-132">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="9d771-133">리소스 그룹에 대 한 단계를 수행 하는 hello 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="9d771-134">선택 **기존 항목 사용** tooselect 기존 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="9d771-135">선택 **새로 만들기** tooenter 리소스 그룹에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="9d771-136">이 자습서에서는 hello 단계 중 일부를 가정 hello 이름을 사용 합니다: **ADFTutorialResourceGroup** hello 리소스 그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="9d771-137">리소스 그룹에 대 한 toolearn 참조 [toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="9d771-138">선택 된 **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="9d771-139">선택 **Pin toodashboard** hello hello 블레이드 맨 아래에 있는 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="9d771-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-140">Click **Create**.</span></span>
      
       ![새 데이터 팩터리 블레이드](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="9d771-142">Hello 참조 hello 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 블레이드:</span><span class="sxs-lookup"><span data-stu-id="9d771-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="9d771-144">복사 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="9d771-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="9d771-145">Hello Data Factory 블레이드에서 클릭 **[미리 보기] 데이터 복사** toolaunch hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9d771-146">해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 사용 안 함/취소 **타사 쿠키를 차단 하 고 사이트 데이터** hello 브라우저 설정 (또는) 유지 하지만 사용 하도록 설정에서 설정 하 고 예외를 만들  **login.microsoftonline.com** 및 hello 마법사를 다시 시작 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="9d771-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="9d771-147">Hello에 **속성** 페이지:</span><span class="sxs-lookup"><span data-stu-id="9d771-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="9d771-148">**태스크 이름**에 **CopyFromBlobToAzureSql**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="9d771-149">**설명** 을 입력합니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="9d771-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="9d771-150">변경 hello **시작 날짜 시간이** 및 hello **종료 날짜 시간** hello 종료 날짜는 tootoday를 설정 하 고 toofive 일 전인 날짜 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="9d771-151">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-151">Click **Next**.</span></span>  
      
      ![복사 도구 - 속성 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="9d771-153">Hello에 **소스 데이터 저장소** 페이지 **Azure Blob 저장소** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="9d771-154">이 페이지 toospecify hello 원본 데이터 저장소를 사용 하 여 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="9d771-156">Hello에 **hello Azure Blob 저장소 계정을 지정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="9d771-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="9d771-157">**연결된 서비스 이름**에 **AzureStorageLinkedService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="9d771-158">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="9d771-159">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="9d771-160">선택 된 **Azure 저장소 계정** hello에서 목록은 Azure 저장소 계정 선택 hello 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="9d771-161">선택할 수도 있습니다 tooenter 저장소 계정 설정을 수동으로 선택 하 여 **수동으로 입력** hello에 대 한 옵션 **계정 선택 방법을**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![도구에 복사-hello Azure Blob 저장소 계정을 지정 합니다.](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="9d771-163">**선택 hello 입력된 파일이 나 폴더** 페이지:</span><span class="sxs-lookup"><span data-stu-id="9d771-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="9d771-164">**adftutorial**(폴더)을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="9d771-165">**emp.txt**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="9d771-167">Hello에 **선택 hello 입력된 파일이 나 폴더** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="9d771-168">**이진 복사**를 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-168">Do not select **Binary copy**.</span></span> 
   
    ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="9d771-170">Hello에 **파일 형식 설정** hello 구분 기호 및 hello 파일을 구문 분석 하 여 hello 마법사에 의해 자동으로 감지 있는 hello 스키마 참조 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="9d771-171">또한 hello 복사 마법사 toostop 자동 검색할 또는 toooverride hello 구분 기호를 수동으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="9d771-172">클릭 **다음** hello 구분 기호를 검토 하 고 데이터를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![복사 도구 - 파일 형식 설정](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="9d771-174">Hello 대상 데이터 페이지를 저장, 선택 **Azure SQL 데이터베이스**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![복사 도구 - 대상 저장소 선택](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="9d771-176">**지정 hello Azure SQL 데이터베이스** 페이지:</span><span class="sxs-lookup"><span data-stu-id="9d771-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="9d771-177">입력 **AzureSqlLinkedService** hello에 대 한 **연결 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="9d771-178">**서버/데이터베이스 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="9d771-179">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="9d771-180">**서버 이름** 및 **데이터베이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="9d771-181">**사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="9d771-182">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-182">Click **Next**.</span></span>  
      
      ![복사 도구 - Azure SQL Database 지정](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="9d771-184">Hello에 **테이블 매핑** 페이지에서 **emp** hello에 대 한 **대상** hello 드롭 다운 목록에서 필드를 클릭 **아래쪽 화살표** (선택 사항) toosee hello 스키마 및 toopreview hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![복사 도구 - 테이블 매핑](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="9d771-186">Hello에 **스키마 매핑** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![복사 도구 - 스키마 매핑](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="9d771-188">Hello에 **성능 설정** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="9d771-190">Hello에 대 한 정보를 검토 **요약** 페이지를 클릭 하 여 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="9d771-191">hello 마법사 (여기서 hello 복사 마법사를 실행)에서 hello data factory에 두 개의 연결 된 서비스, 두 개의 데이터 집합 (입력 및 출력) 및 하나의 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="9d771-193">응용 프로그램 모니터링 및 관리 시작</span><span class="sxs-lookup"><span data-stu-id="9d771-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="9d771-194">Hello에 **배포** 페이지에서 hello 링크 클릭: `Click here toomonitor copy pipeline`합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![복사 도구 - 배포 성공 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="9d771-196">응용 프로그램을 모니터링 하는 hello 웹 브라우저에서 별도 탭에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![모니터링 앱](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="9d771-198">시간 조각의 toosee hello 최신 상태를 클릭 **새로 고침** hello 단추 **활동 창** hello 맨 아래에는 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="9d771-199">5 개 활동 windows hello 파이프라인에 대 한 시작 및 종료 시간 사이의 5 일 동안 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="9d771-200">hello 목록이 자동으로 새로 고쳐진 하지, 다음과 같은 행위는 하므로 필요 tooclick 새로 고침 몇 번 모든 hello 활동 windows hello 준비 상태에서를 보기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="9d771-201">Hello 목록에서 활동을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-201">Select an activity window in hello list.</span></span> <span data-ttu-id="9d771-202">Hello에 대 한 hello 세부 사항을 볼 **활동 창 탐색기** hello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![활동 창 세부 정보](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="9d771-204">즉, 이러한 날짜에 대 한 hello 매일 출력 조각만 생성 이미 녹색에서 11, 12, 13, 14 및 15 hello 날짜는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="9d771-205">또한이 색 구분 hello 파이프라인에서 참조 하 고 hello 다이어그램 보기에서 출력 데이터 집합을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="9d771-206">Hello 이전 단계에서 고 해당 데이터베이스 두 슬라이스 이미 생성 된 파일, 한 조각 현재 처리 중인 hello 다른 두 대기 중인 toobe 처리 (hello 색 구분에 따라).</span><span class="sxs-lookup"><span data-stu-id="9d771-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="9d771-207">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d771-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d771-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d771-208">Next steps</span></span>
<span data-ttu-id="9d771-209">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9d771-210">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="9d771-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9d771-211">데이터 저장소에 대 한 hello 복사 마법사에서 볼 수 있는 필드/속성에 대 한 자세한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d771-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
