---
title: "자습서: 복사 마법사를 사용하여 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 데이터 팩터리가 지원하는 복사 마법사를 사용하여 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="73eed-103">자습서: 데이터 팩터리 복사 마법사를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="73eed-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="73eed-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="73eed-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="73eed-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="73eed-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="73eed-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="73eed-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="73eed-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73eed-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="73eed-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73eed-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="73eed-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="73eed-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="73eed-110">REST API</span><span class="sxs-lookup"><span data-stu-id="73eed-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="73eed-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="73eed-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="73eed-112">이 자습서에서는 **복사 마법사**를 사용하여 Azure Blob 저장소에서 Azure SQL 데이터베이스로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="73eed-113">Azure Data Factory **복사 마법사**를 사용하면 지원되는 원본 데이터 저장소에서 지원되는 대상 데이터 저장소로 데이터를 복사하는 데이터 파이프라인을 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="73eed-114">따라서 데이터 이동 시나리오에 대한 샘플 파이프라인을 만드는 첫 번째 단계로 마법사를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="73eed-115">원본 및 대상으로 지원되는 데이터 저장소의 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73eed-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="73eed-116">이 자습서는 Azure Data Factory를 만들고, 복사 마법사를 실행하고, 데이터 수집/이동 시나리오에 대한 세부 정보를 제공하는 일련의 단계를 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="73eed-117">마법사의 단계를 마치면, Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 복사 작업이 있는 파이프라인이 마법사에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="73eed-118">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73eed-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73eed-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="73eed-119">Prerequisites</span></span>
<span data-ttu-id="73eed-120">이 자습서를 수행하기 전에 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서에 나열된 필수 구성 요소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="73eed-121">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="73eed-121">Create data factory</span></span>
<span data-ttu-id="73eed-122">이 단계에서는 Azure 포털을 사용하여 **ADFTutorialDataFactory**라는 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="73eed-123">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="73eed-124">왼쪽 위 모서리에서 **+ 새로 만들기**를 클릭하고, **데이터 + 분석**을 클릭한 다음, **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="73eed-126">**새 데이터 팩터리** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="73eed-127">**ADFTutorialDataFactory**를 **이름**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="73eed-128">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="73eed-129">`Data factory name “ADFTutorialDataFactory” is not available` 오류가 표시되면 데이터 팩터리 이름을 변경하고(예: yournameADFTutorialDataFactoryYYYYMMDD) 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="73eed-130">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73eed-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="73eed-132">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="73eed-133">리소스 그룹에 대해 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="73eed-134">**기존 항목 사용**을 선택하고 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="73eed-135">**새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="73eed-136">이 자습서의 일부 단계에서는 리소스 그룹에 **ADFTutorialResourceGroup** 이라는 이름을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="73eed-137">리소스 그룹에 대한 자세한 내용은 [리소스 그룹을 사용하여 Azure 리소스 관리](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73eed-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="73eed-138">Data Factory의 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="73eed-139">블레이드 하단에서 **대시보드에 고정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="73eed-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-140">Click **Create**.</span></span>
      
       ![새 데이터 팩터리 블레이드](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="73eed-142">만들기가 완료되면 다음 이미지와 같이 **Data Factory** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="73eed-144">복사 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="73eed-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="73eed-145">Data Factory 블레이드에서 **데이터 복사[미리 보기]** 타일을 클릭하여 **복사 마법사**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="73eed-146">웹 브라우저가 "권한 부여 중..." 상태에서 갇혀 있음이 확인되면, 브라우저 설정에서 **타사 쿠키 및 사이트 데이터 차단** 설정을 사용 안 함/선택 취소로 지정하거나 계속 사용하도록 유지하고 **login.microsoftonline.com**에 대한 예외를 만든 다음, 마법사를 다시 시작해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="73eed-147">**속성** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="73eed-148">**태스크 이름**에 **CopyFromBlobToAzureSql**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="73eed-149">**설명** 을 입력합니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="73eed-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="73eed-150">종료 날짜가 오늘로 설정되고 시작 날짜가 5일 전으로 설정되도록 **시작 날짜 시간** 및 **종료 날짜 시간**을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="73eed-151">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-151">Click **Next**.</span></span>  
      
      ![복사 도구 - 속성 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="73eed-153">**원본 데이터 저장소** 페이지에서 **Azure Blob Storage** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="73eed-154">이 페이지를 사용하여 복사 작업에 사용할 원본 데이터 저장소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="73eed-156">**Azure Blob 저장소 계정 지정** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="73eed-157">**연결된 서비스 이름**에 **AzureStorageLinkedService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="73eed-158">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="73eed-159">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="73eed-160">선택한 구독에서 사용할 수 있는 Azure Storage 계정 목록에서 **Azure Storage 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="73eed-161">**계정 선택 방법**으로 **수동으로 입력** 옵션을 선택하여 저장소 계정 설정을 수동으로 입력할 수도 있습니다. 그리고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![복사 도구 - Azure Blob 저장소 계정 지정 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="73eed-163">**입력 파일 또는 폴더 선택** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="73eed-164">**adftutorial**(폴더)을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="73eed-165">**emp.txt**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![복사 도구 - 입력 파일 또는 폴더 선택 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="73eed-167">**입력 파일 또는 폴더 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="73eed-168">**이진 복사**를 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-168">Do not select **Binary copy**.</span></span> 
   
    ![복사 도구 - 입력 파일 또는 폴더 선택 페이지](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="73eed-170">**파일 형식 설정** 페이지에 파일을 구문 분석하여 마법사에 의해 자동으로 감지되는 구분 기호와 스키마가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="73eed-171">복사 마법사의 자동 감지를 중지하거나 재정하기 위해 구분 기호를 수동으로 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="73eed-172">구분 기호를 검토하고 데이터를 미리 본 후에 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![복사 도구 - 파일 형식 설정](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="73eed-174">대상 데이터 저장소 페이지에서 **Azure SQL Database**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![복사 도구 - 대상 저장소 선택](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="73eed-176">**Azure SQL 데이터베이스 지정** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="73eed-177">**연결 이름** 필드에 **AzureSqlLinkedService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="73eed-178">**서버/데이터베이스 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="73eed-179">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="73eed-180">**서버 이름** 및 **데이터베이스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="73eed-181">**사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="73eed-182">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-182">Click **Next**.</span></span>  
      
      ![복사 도구 - Azure SQL Database 지정](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="73eed-184">**테이블 매핑** 페이지에 있는 드롭다운 목록의 **대상** 필드에서 **emp**를 선택하고 **아래쪽 화살표**를 클릭하여(선택 사항) 스키마를 확인하고 데이터를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![복사 도구 - 테이블 매핑](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="73eed-186">**스키마 매핑** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![복사 도구 - 스키마 매핑](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="73eed-188">**성능 설정** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="73eed-190">**요약** 페이지에서 정보를 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="73eed-191">마법사는 데이터 팩터리(복사 마법사를 실행한 위치)에 두 개의 연결된 서비스, 두 개의 데이터 집합(입력 및 출력), 하나의 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="73eed-193">응용 프로그램 모니터링 및 관리 시작</span><span class="sxs-lookup"><span data-stu-id="73eed-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="73eed-194">**배포** 페이지에서 `Click here to monitor copy pipeline` 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![복사 도구 - 배포 성공 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="73eed-196">모니터링 응용 프로그램이 웹 브라우저의 별도 탭에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![모니터링 앱](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="73eed-198">매시간 조각의 최신 상태를 보려면 아래쪽의 **활동 창** 목록에서 **새로 고침** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="73eed-199">파이프라인의 시작 시간과 종료 시간 사이의 5일 동안 5개의 활동 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="73eed-200">목록을 자동으로 새로 고치지 않으므로 [준비] 상태의 모든 활동 창을 표시하려면 [새로 고침] 단추를 몇 번 클릭해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="73eed-201">목록에서 활동 창을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-201">Select an activity window in the list.</span></span> <span data-ttu-id="73eed-202">**활동 창 탐색기**에서 해당 활동 창에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![활동 창 세부 정보](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="73eed-204">11, 12, 13, 14 및 15에 해당하는 날짜가 녹색으로 표시되어 있습니다. 즉 이러한 날짜에 대해 이미 출력 조각이 매일 생성되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="73eed-205">또한 다이어그램 보기에서도 파이프라인과 출력 데이터 집합에 대한 이러한 색 구분이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="73eed-206">이전 단계에서 색 구분을 기반으로 하여 두 조각이 이미 생성되었고, 하나의 조각이 현재 처리 중이며, 다른 두 조각이 처리 대기 중임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="73eed-207">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73eed-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73eed-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73eed-208">Next steps</span></span>
<span data-ttu-id="73eed-209">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="73eed-210">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="73eed-211">데이터 저장소에 대한 복사 마법사에 표시되는 필드/속성에 대한 자세한 내용을 보려면 표에 나와 있는 해당 데이터 저장소에 대한 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="73eed-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 