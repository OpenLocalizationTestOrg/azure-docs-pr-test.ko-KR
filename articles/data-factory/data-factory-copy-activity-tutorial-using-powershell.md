---
title: "자습서: Azure PowerShell을 사용 하 여 파이프라인 toomove 데이터 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure PowerShell을 사용하여 복사 작업을 사용하는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="fbacd-103">자습서: Azure PowerShell을 사용하여 데이터를 이동하는 Data Factory 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbacd-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="fbacd-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="fbacd-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="fbacd-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="fbacd-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fbacd-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="fbacd-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbacd-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="fbacd-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbacd-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="fbacd-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="fbacd-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="fbacd-110">REST API</span><span class="sxs-lookup"><span data-stu-id="fbacd-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="fbacd-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="fbacd-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="fbacd-112">이 문서에서는 설명 어떻게 toouse PowerShell toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="fbacd-113">새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="fbacd-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="fbacd-115">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="fbacd-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fbacd-117">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="fbacd-118">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="fbacd-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fbacd-120">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="fbacd-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="fbacd-122">이 문서는 모든 hello 데이터 팩터리 cmdlet을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="fbacd-123">이러한 cmdlet에 대한 포괄적인 설명서는 [Data Factory Cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="fbacd-124">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="fbacd-125">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbacd-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fbacd-126">Prerequisites</span></span>
- <span data-ttu-id="fbacd-127">Hello에 나온 필수 조건을 완료 [자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="fbacd-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="fbacd-128">**Azure PowerShell**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="fbacd-129">Hello 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](../powershell-install-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="fbacd-130">단계</span><span class="sxs-lookup"><span data-stu-id="fbacd-130">Steps</span></span>
<span data-ttu-id="fbacd-131">이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="fbacd-132">Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="fbacd-133">이 단계에서는 ADFTutorialDataFactoryPSH라는 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="fbacd-134">만들 **연결 된 서비스** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="fbacd-135">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="fbacd-136">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="fbacd-137">컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="fbacd-138">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="fbacd-139">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="fbacd-140">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="fbacd-141">입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="fbacd-142">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="fbacd-143">고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="fbacd-144">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="fbacd-145">고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="fbacd-146">만들기는 **파이프라인** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="fbacd-147">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="fbacd-148">hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="fbacd-149">모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="fbacd-150">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="fbacd-151">모니터 hello 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-151">Monitor hello pipeline.</span></span> <span data-ttu-id="fbacd-152">이 단계에서는 있습니다 **모니터** PowerShell을 사용 하 여 입력 및 출력 데이터 집합의 조각을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="fbacd-153">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fbacd-154">전체 [hello 자습서에 대 한 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="fbacd-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="fbacd-155">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fbacd-156">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fbacd-157">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="fbacd-158">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="fbacd-159">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-159">Launch **PowerShell**.</span></span> <span data-ttu-id="fbacd-160">이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="fbacd-161">닫고 다시 열 경우 toorun hello 명령을 다시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="fbacd-162">Hello 다음, 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="fbacd-163">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="fbacd-164">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="fbacd-165">대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독:</span><span class="sxs-lookup"><span data-stu-id="fbacd-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="fbacd-166">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="fbacd-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="fbacd-167">이라는 hello 리소스 그룹을 사용 하는 것으로 가정이 자습서의 hello 단계 중 일부 **ADFTutorialResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="fbacd-168">Toouse 필요한 다른 리소스 그룹을 사용 하는 경우이 자습서에서는 ADFTutorialResourceGroup 대신 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="fbacd-169">Hello 실행 **새로 AzureRmDataFactory** 라는 데이터 팩터리 cmdlet toocreate **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="fbacd-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="fbacd-170">이 이름은 이미 사용되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-170">This name may already have been taken.</span></span> <span data-ttu-id="fbacd-171">따라서 고유 하 게 만드는 hello 데이터 팩터리의 hello 이름 접두사 또는 접미사를 추가 하 여 (예: ADFTutorialDataFactoryPSH05152017) hello 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="fbacd-172">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="fbacd-172">Note hello following points:</span></span>

* <span data-ttu-id="fbacd-173">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="fbacd-174">Hello 다음 오류가 표시 되 면 hello 이름 (예를 들어 yournameADFTutorialDataFactoryPSH)을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="fbacd-175">이 자습서의 단계를 수행하는 동안 ADFTutorialFactoryPSH 대신 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="fbacd-176">Data Factory 아티팩트에 대한 내용은 [Data Factory - 명명 규칙](data-factory-naming-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="fbacd-177">toocreate 데이터 팩터리 인스턴스 hello Azure 구독 관리자 또는 참가자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="fbacd-178">hello hello 데이터 팩터리의 이름입니다 hello 미래에 DNS 이름으로 등록 하 고 있으므로 공개 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="fbacd-179">Hello 다음 오류가 나타날 수 있습니다: "**이 구독 microsoft.datafactory가 등록 된 toouse 네임 스페이스가 아닙니다.**"</span><span class="sxs-lookup"><span data-stu-id="fbacd-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="fbacd-180">Hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fbacd-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="fbacd-181">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="fbacd-182">데이터 팩터리 공급자가 등록 되어 해당 hello hello 명령 tooconfirm 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fbacd-183">로그인에 사용 하 여 Azure 구독 toohello hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fbacd-184">Tooa Data Factory 블레이드로 이동 하거나 hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="fbacd-185">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fbacd-186">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-186">Create linked services</span></span>
<span data-ttu-id="fbacd-187">데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="fbacd-188">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="fbacd-189">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="fbacd-190">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="fbacd-191">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="fbacd-192">이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="fbacd-193">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="fbacd-194">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="fbacd-195">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="fbacd-196">Azure 저장소 계정에 대한 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="fbacd-197">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="fbacd-198">라는 JSON 파일을 만들어 **AzureStorageLinkedService.json** 에 **C:\ADFGetStartedPSH** 폴더 콘텐츠를 다음 hello로: (hello 폴더 만들기 ADFGetStartedPSH 아직 없는 경우.)</span><span class="sxs-lookup"><span data-stu-id="fbacd-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fbacd-199">대체 &lt;accountname&gt; 및 &lt;accountkey&gt; 이름과 hello 파일 저장 하기 전에 Azure 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="fbacd-200">**Azure PowerShell**, toohello 전환 **ADFGetStartedPSH** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="fbacd-201">Hello 실행 **새로 AzureRmDataFactoryLinkedService** 연결 된 서비스 cmdlet toocreate hello: **AzureStorageLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="fbacd-202">이 cmdlet 및 기타 데이터 팩터리 cmdlet이이 자습서에서 사용 하 여 값이 필요 하면 toopass hello에 대 한 **ResourceGroupName** 및 **DataFactoryName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="fbacd-203">또는 리소스 그룹 이름 및 DataFactoryName cmdlet을 실행할 때마다 입력 하지 않고도 hello 새로 AzureRmDataFactory cmdlet에서 반환 하는 hello DataFactory 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="fbacd-204">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="fbacd-205">이 연결 된 서비스를 만드는 다른 방법은 toospecify 리소스 그룹 이름 및 hello DataFactory 개체를 지정 하는 대신 데이터 팩터리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="fbacd-206">Azure SQL Database에 대한 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="fbacd-207">이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="fbacd-208">콘텐츠 다음 hello로 AzureSqlLinkedService.json C:\ADFGetStartedPSH 폴더에는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fbacd-209">&lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; 및 &lt;password&gt;를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="fbacd-210">다음 명령은 toocreate hello 연결 된 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="fbacd-211">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="fbacd-212">확인 **tooAzure 서비스 액세스를 허용** SQL 데이터베이스 서버에 대 한 설정이 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="fbacd-213">tooverify 및 켜십시오, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="fbacd-214">Toohello 로그인 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fbacd-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="fbacd-215">클릭 **더 많은 서비스 >** 를 클릭 한 hello 왼쪽 **SQL server** hello에 **데이터베이스** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="fbacd-216">SQL server hello 목록에서 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="fbacd-217">Hello SQL server 블레이드 클릭 **방화벽 설정 표시** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="fbacd-218">Hello에 **방화벽 설정** 블레이드에서 클릭 **ON** 에 대 한 **tooAzure 서비스 액세스를 허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="fbacd-219">클릭 **저장** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="fbacd-220">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-220">Create datasets</span></span>
<span data-ttu-id="fbacd-221">Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="fbacd-222">이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="fbacd-223">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="fbacd-224">고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="fbacd-225">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="fbacd-226">및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="fbacd-227">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-227">Create an input dataset</span></span>
<span data-ttu-id="fbacd-228">이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="fbacd-229">하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="fbacd-230">이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="fbacd-231">라는 JSON 파일을 만들어 **InputDataset.json** hello에 **C:\ADFGetStartedPSH** 폴더에 콘텐츠를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="fbacd-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

    ```json
    {
        "name": "InputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    <span data-ttu-id="fbacd-232">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="fbacd-233">속성</span><span class="sxs-lookup"><span data-stu-id="fbacd-233">Property</span></span> | <span data-ttu-id="fbacd-234">설명</span><span class="sxs-lookup"><span data-stu-id="fbacd-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fbacd-235">type</span><span class="sxs-lookup"><span data-stu-id="fbacd-235">type</span></span> | <span data-ttu-id="fbacd-236">hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="fbacd-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fbacd-237">linkedServiceName</span></span> | <span data-ttu-id="fbacd-238">Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fbacd-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="fbacd-239">folderPath</span></span> | <span data-ttu-id="fbacd-240">Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="fbacd-241">이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="fbacd-242">fileName</span><span class="sxs-lookup"><span data-stu-id="fbacd-242">fileName</span></span> | <span data-ttu-id="fbacd-243">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-243">This property is optional.</span></span> <span data-ttu-id="fbacd-244">이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="fbacd-245">이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="fbacd-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="fbacd-246">format -> type</span></span> |<span data-ttu-id="fbacd-247">사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="fbacd-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fbacd-248">columnDelimiter</span></span> | <span data-ttu-id="fbacd-249">hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="fbacd-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="fbacd-250">frequency/interval</span></span> | <span data-ttu-id="fbacd-251">hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="fbacd-252">즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="fbacd-253">Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="fbacd-254">external</span><span class="sxs-lookup"><span data-stu-id="fbacd-254">external</span></span> | <span data-ttu-id="fbacd-255">이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="fbacd-256">이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="fbacd-257">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="fbacd-258">Hello 명령 toocreate hello Data Factory 데이터 집합을 따라를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="fbacd-259">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="fbacd-260">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fbacd-260">Create an output dataset</span></span>
<span data-ttu-id="fbacd-261">명명 된 출력 데이터 집합을 만들면이 부분 hello 단계 **OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="fbacd-262">이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="fbacd-263">라는 JSON 파일을 만들어 **OutputDataset.json** hello에 **C:\ADFGetStartedPSH** 폴더 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="fbacd-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    <span data-ttu-id="fbacd-264">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="fbacd-265">속성</span><span class="sxs-lookup"><span data-stu-id="fbacd-265">Property</span></span> | <span data-ttu-id="fbacd-266">설명</span><span class="sxs-lookup"><span data-stu-id="fbacd-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fbacd-267">type</span><span class="sxs-lookup"><span data-stu-id="fbacd-267">type</span></span> | <span data-ttu-id="fbacd-268">hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="fbacd-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fbacd-269">linkedServiceName</span></span> | <span data-ttu-id="fbacd-270">Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fbacd-271">tableName</span><span class="sxs-lookup"><span data-stu-id="fbacd-271">tableName</span></span> | <span data-ttu-id="fbacd-272">지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="fbacd-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="fbacd-273">frequency/interval</span></span> | <span data-ttu-id="fbacd-274">hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.</span><span class="sxs-lookup"><span data-stu-id="fbacd-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="fbacd-275">세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="fbacd-276">Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="fbacd-277">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="fbacd-278">Hello toocreate hello data factory 데이터 명령 집합을 따라를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="fbacd-279">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="fbacd-280">파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-280">Create a pipeline</span></span>
<span data-ttu-id="fbacd-281">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="fbacd-282">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="fbacd-283">이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="fbacd-284">hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="fbacd-285">따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="fbacd-286">라는 JSON 파일을 만들어 **ADFTutorialPipeline.json** hello에 **C:\ADFGetStartedPSH** 폴더에 콘텐츠를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="fbacd-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="fbacd-287">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="fbacd-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="fbacd-288">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="fbacd-289">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fbacd-290">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="fbacd-291">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="fbacd-292">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="fbacd-293">원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fbacd-294">소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="fbacd-295">Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="fbacd-296">Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="fbacd-297">예를 들어 "2016-02-03", 즉 너무 "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="fbacd-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="fbacd-298">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="fbacd-299">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="fbacd-300">hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="fbacd-301">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="fbacd-302">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="fbacd-303">앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="fbacd-304">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fbacd-305">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fbacd-306">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="fbacd-307">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="fbacd-308">Hello 명령 toocreate hello 데이터 팩터리 테이블을 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="fbacd-309">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="fbacd-310">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="fbacd-310">**Congratulations!**</span></span> <span data-ttu-id="fbacd-311">Azure blob 저장소 tooan Azure SQL 데이터베이스의 파이프라인 toocopy 데이터로 Azure 데이터 팩터리에 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="fbacd-312">모니터 hello 파이프라인</span><span class="sxs-lookup"><span data-stu-id="fbacd-312">Monitor hello pipeline</span></span>
<span data-ttu-id="fbacd-313">이 단계를 진행 되는 상황에서 Azure 데이터 팩터리에 Azure PowerShell toomonitor 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="fbacd-314">대체 &lt;DataFactoryName&gt; data factory와 실행의 hello 이름의 **Get AzureRmDataFactory**, hello 출력 tooa 변수 $df 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="fbacd-315">예:</span><span class="sxs-lookup"><span data-stu-id="fbacd-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="fbacd-316">다음 출력 $df toosee hello의 인쇄 hello 내용을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="fbacd-317">실행 **Get AzureRmDataFactorySlice** hello의 모든 분할 영역에 대 한 세부 정보 tooget **OutputDataset**, hello 파이프라인의 hello 출력 데이터 집합은입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="fbacd-318">이 설정은 hello 일치 해야 **시작** hello 파이프라인 JSON의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="fbacd-319">24 조각 표시 되어야 다음 날의 hello AM hello 현재 날짜 too12의 오전 12 시에서 각 시간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="fbacd-320">다음은 hello 출력에서 3 개의 샘플 슬라이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="fbacd-321">실행 **Get AzureRmDataFactoryRun** tooget hello 활동 세부 정보에 대해 실행 되는 **특정** 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="fbacd-322">Hello 이전 명령 toospecify hello hello StartDateTime 매개 변수 값의 hello 출력에서 hello 날짜 및 시간 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="fbacd-323">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="fbacd-324">Data Factory cmdlet에 대한 포괄적인 설명서는 [Data Factory cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbacd-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="fbacd-325">요약</span><span class="sxs-lookup"><span data-stu-id="fbacd-325">Summary</span></span>
<span data-ttu-id="fbacd-326">이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="fbacd-327">PowerShell toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="fbacd-328">이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="fbacd-329">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fbacd-330">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-330">Created **linked services**:</span></span>

   <span data-ttu-id="fbacd-331">a.</span><span class="sxs-lookup"><span data-stu-id="fbacd-331">a.</span></span> <span data-ttu-id="fbacd-332">**Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하는 Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="fbacd-333">b.</span><span class="sxs-lookup"><span data-stu-id="fbacd-333">b.</span></span> <span data-ttu-id="fbacd-334">**Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하는 SQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="fbacd-335">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="fbacd-336">만든는 **파이프라인** 와 **복사 작업**와 **BlobSource** hello 소스로 및 **SqlSink** hello 싱크로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbacd-337">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbacd-337">Next steps</span></span>
<span data-ttu-id="fbacd-338">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="fbacd-339">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="fbacd-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="fbacd-340">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbacd-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

