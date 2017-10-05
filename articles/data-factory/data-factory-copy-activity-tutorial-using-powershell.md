---
title: "자습서: Azure PowerShell을 사용하여 데이터를 이동하는 파이프라인 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 81efe7c6af29af778686e1f6bcf62fedc9711052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="2a1f7-103">자습서: Azure PowerShell을 사용하여 데이터를 이동하는 Data Factory 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a1f7-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2a1f7-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="2a1f7-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="2a1f7-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="2a1f7-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2a1f7-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="2a1f7-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a1f7-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="2a1f7-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a1f7-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="2a1f7-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="2a1f7-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="2a1f7-110">REST API</span><span class="sxs-lookup"><span data-stu-id="2a1f7-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="2a1f7-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="2a1f7-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="2a1f7-112">이 문서에서는 PowerShell을 사용하여 Azure Blob 저장소에서 Azure SQL 데이터베이스로 데이터를 복사하는 파이프라인이 있는 데이터 팩터리를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-112">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="2a1f7-113">Azure Data Factory를 처음 사용하는 경우 이 자습서를 수행하기 전에 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="2a1f7-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="2a1f7-115">복사 작업은 지원되는 데이터 저장소에서 지원되는 싱크 데이터 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="2a1f7-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2a1f7-117">이 작업은 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2a1f7-118">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="2a1f7-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2a1f7-120">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="2a1f7-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="2a1f7-122">이 문서는 모든 데이터 팩터리 cmdlet을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-122">This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="2a1f7-123">이러한 cmdlet에 대한 포괄적인 설명서는 [Data Factory Cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="2a1f7-124">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="2a1f7-125">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a1f7-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a1f7-126">Prerequisites</span></span>
- <span data-ttu-id="2a1f7-127">[자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서에서 나열하는 필수 구성 요소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="2a1f7-128">**Azure PowerShell**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="2a1f7-129">[Azure PowerShell을 설치 및 구성하는 방법](../powershell-install-configure.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-129">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="2a1f7-130">단계</span><span class="sxs-lookup"><span data-stu-id="2a1f7-130">Steps</span></span>
<span data-ttu-id="2a1f7-131">이 자습서의 일부로 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-131">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="2a1f7-132">Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="2a1f7-133">이 단계에서는 ADFTutorialDataFactoryPSH라는 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="2a1f7-134">데이터 팩터리에서 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-134">Create **linked services** in the data factory.</span></span> <span data-ttu-id="2a1f7-135">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="2a1f7-136">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-136">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="2a1f7-137">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 컨테이너를 만들고 이 저장소 계정에 데이터를 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-137">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="2a1f7-138">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-138">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="2a1f7-139">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-139">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="2a1f7-140">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="2a1f7-141">데이터 팩터리에서 입력 및 출력 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-141">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="2a1f7-142">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-142">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="2a1f7-143">그리고 입력 Blob 데이터 집합은 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-143">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="2a1f7-144">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-144">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="2a1f7-145">그리고 출력 SQL 테이블 데이터 집합은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-145">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="2a1f7-146">데이터 팩터리에서 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-146">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="2a1f7-147">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="2a1f7-148">복사 활동은 Azure Blob 저장소의 Blob에서 Azure SQL 데이터베이스의 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-148">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="2a1f7-149">파이프라인의 복사 활동을 사용하여 지원되는 모든 원본의 데이터를 지원되는 모든 대상으로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-149">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="2a1f7-150">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="2a1f7-151">파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-151">Monitor the pipeline.</span></span> <span data-ttu-id="2a1f7-152">이 단계에서는 PowerShell을 사용하여 입력 및 출력 데이터 집합의 조각을 **모니터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-152">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="2a1f7-153">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2a1f7-154">아직 완료하지 않은 경우 [자습서의 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-154">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="2a1f7-155">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="2a1f7-156">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="2a1f7-157">예를 들어 원본에서 대상 데이터 저장소에 데이터를 복사하는 복사 작업 및 입력 데이터를 제품 출력 데이터로 변환하는 Hive 스크립트를 실행하는 HDInsight Hive 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-157">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="2a1f7-158">이 단계에서는 데이터 팩터리 만들기를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-158">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="2a1f7-159">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-159">Launch **PowerShell**.</span></span> <span data-ttu-id="2a1f7-160">이 자습서를 마칠 때까지 Azure PowerShell을 열어 두세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-160">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="2a1f7-161">닫은 후 다시 여는 경우 명령을 다시 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-161">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="2a1f7-162">다음 명령을 실행하고 Azure Portal에 로그인하는 데 사용할 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-162">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="2a1f7-163">다음 명령을 실행하여 이 계정의 모든 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-163">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="2a1f7-164">다음 명령을 실행하여 사용하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-164">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="2a1f7-165">**&lt;NameOfAzureSubscription**&gt;을 Azure 구독의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-165">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="2a1f7-166">다음 명령을 실행하여 **ADFTutorialResourceGroup** 이라는 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="2a1f7-167">이 자습서의 일부 단계에서는 **ADFTutorialResourceGroup**이라는 리소스 그룹을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-167">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="2a1f7-168">다른 리소스 그룹을 사용하는 경우 이 자습서에서 ADFTutorialResourceGroup 대신 해당 리소스 그룹을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-168">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="2a1f7-169">**New-AzureRmDataFactory** cmdlet을 실행하여 **ADFTutorialDataFactoryPSH**라는 Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-169">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="2a1f7-170">이 이름은 이미 사용되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-170">This name may already have been taken.</span></span> <span data-ttu-id="2a1f7-171">따라서 접두사 또는 접미사(예: ADFTutorialDataFactoryPSH05152017)를 추가하여 데이터 팩터리 이름을 고유하게 만들어 해당 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-171">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span></span>  

<span data-ttu-id="2a1f7-172">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-172">Note the following points:</span></span>

* <span data-ttu-id="2a1f7-173">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-173">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="2a1f7-174">다음과 같은 오류가 발생하면 이름(예: yournameADFTutorialDataFactoryPSH)을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-174">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="2a1f7-175">이 자습서의 단계를 수행하는 동안 ADFTutorialFactoryPSH 대신 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="2a1f7-176">Data Factory 아티팩트에 대한 내용은 [Data Factory - 명명 규칙](data-factory-naming-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="2a1f7-177">Data Factory 인스턴스를 만들려면 Azure 구독의 참가자 또는 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-177">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="2a1f7-178">Data Factory의 이름은 나중에 DNS 이름으로 표시되므로 공개적으로 등록될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-178">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="2a1f7-179">"**구독이 Microsoft.DataFactory 네임스페이스를 사용하도록 등록되어 있지 않습니다.**"라는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-179">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="2a1f7-180">다음 중 하나를 수행하고 다시 게시해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-180">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="2a1f7-181">Azure PowerShell에서 다음 명령을 실행하여 데이터 팩터리 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-181">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="2a1f7-182">데이터 팩터리 공급자가 등록되어 있는지 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-182">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="2a1f7-183">Azure 구독을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-183">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2a1f7-184">Azure Portal에서 Data Factory 블레이드로 이동하거나 Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-184">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="2a1f7-185">이 작업은 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-185">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="2a1f7-186">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-186">Create linked services</span></span>
<span data-ttu-id="2a1f7-187">데이터 팩터리에서 연결된 서비스를 만들어 데이터 저장소를 연결하고 계산 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-187">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="2a1f7-188">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="2a1f7-189">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="2a1f7-190">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="2a1f7-191">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-191">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="2a1f7-192">이 저장소 계정은 컨테이너를 만들고 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 데이터를 업로드한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-192">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="2a1f7-193">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-193">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="2a1f7-194">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-194">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="2a1f7-195">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 emp 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-195">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="2a1f7-196">Azure 저장소 계정에 대한 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="2a1f7-197">이 단계에서는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-197">In this step, you link your Azure storage account to your data factory.</span></span>

1. <span data-ttu-id="2a1f7-198">다음 내용이 포함된 **AzureStorageLinkedService.json** JSON 파일을 **C:\ADFGetStartedPSH** 폴더에 만듭니다. (아직 없는 경우 ADFGetStartedPSH 폴더를 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="2a1f7-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2a1f7-199">파일을 저장하기 전에 &lt;accountname&gt;과 &lt;accountkey&gt;를 Azure 저장소 계정의 이름과 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving the file.</span></span> 

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
2. <span data-ttu-id="2a1f7-200">**Azure PowerShell**에서 **ADFGetStartedPSH** 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-200">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="2a1f7-201">**New-AzureRmDataFactoryLinkedService** cmdlet을 실행하여 **AzureStorageLinkedService** 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-201">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="2a1f7-202">이 자습서에서 사용하는 이 cmdlet 및 다른 Data Factory cmdlet을 사용하려면 **ResourceGroupName** 및 **DataFactoryName** 매개 변수에 대한 값을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="2a1f7-203">또는 cmdlet을 실행할 때마다 ResourceGroupName 및 DataFactoryName을 입력하지 않고 New-AzureRmDataFactory cmdlet에서 반환한 DataFactory 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-203">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="2a1f7-204">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-204">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="2a1f7-205">이 연결된 서비스를 만드는 다른 방법은 DataFactory 개체를 지정하는 대신 리소스 그룹 이름과 데이터 팩터리 이름을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-205">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="2a1f7-206">Azure SQL Database에 대한 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="2a1f7-207">이 단계에서는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-207">In this step, you link your Azure SQL database to your data factory.</span></span>

1. <span data-ttu-id="2a1f7-208">다음 내용이 포함된 AzureSqlLinkedService.json이라는 JSON 파일을 C:\ADFGetStartedPSH 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2a1f7-209">&lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; 및 &lt;password&gt;를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
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
2. <span data-ttu-id="2a1f7-210">다음 명령을 실행하여 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-210">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="2a1f7-211">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-211">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="2a1f7-212">SQL Database Server에 대해 **Azure 서비스 방문 허용** 설정이 켜져 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-212">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="2a1f7-213">이 설정을 확인하고 켜려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-213">To verify and turn it on, do the following steps:</span></span>

    1. <span data-ttu-id="2a1f7-214">[Azure Portal](https://portal.azure.com)에 로그인</span><span class="sxs-lookup"><span data-stu-id="2a1f7-214">Log in to the [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="2a1f7-215">왼쪽에 있는 **더 많은 서비스 >**를 클릭하고 **데이터베이스** 범주에서 **SQL 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-215">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span></span>
    3. <span data-ttu-id="2a1f7-216">SQL 서버 목록에서 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-216">Select your server in the list of SQL servers.</span></span>
    4. <span data-ttu-id="2a1f7-217">SQL 서버 블레이드에서 **방화벽 설정 표시** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-217">On the SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="2a1f7-218">**방화벽 설정** 블레이드에서 **Azure 서비스에 대한 액세스 허용**에 대해 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-218">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
    6. <span data-ttu-id="2a1f7-219">도구 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-219">Click **Save** on the toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="2a1f7-220">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-220">Create datasets</span></span>
<span data-ttu-id="2a1f7-221">이전 단계에서는 Azure Storage 계정과 Azure SQL Database를 데이터 팩터리에 연결하는 연결된 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-221">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="2a1f7-222">이 단계에서는 AzureStorageLinkedService 및 AzureSqlLinkedService에서 각각 참조하는 데이터 저장소에 저장된 입력 및 출력 데이터를 나타내는 InputDataset 및 OutputDataset이라는 두 개의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="2a1f7-223">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-223">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="2a1f7-224">그리고 입력 Blob 데이터 집합(InputDataset)은 입력 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-224">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="2a1f7-225">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-225">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="2a1f7-226">그리고 출력 SQL 테이블 데이터 집합(OututDataset)은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-226">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="2a1f7-227">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-227">Create an input dataset</span></span>
<span data-ttu-id="2a1f7-228">이 단계에서는 AzureStorageLinkedService 연결된 서비스에서 나타내는 Azure Storage의 Blob 컨테이너(adftutorial)의 루트 폴더에 있는 Blob 파일(emp.txt)을 가리키는 InputDataset이라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-228">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="2a1f7-229">fileName 값을 지정하지 않거나 건너뛰면 입력 폴더에 있는 모든 Blob의 데이터가 대상에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-229">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="2a1f7-230">이 자습서에서는 fileName 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-230">In this tutorial, you specify a value for the fileName.</span></span>  

1. <span data-ttu-id="2a1f7-231">다음 내용이 포함된 **InputDataset.json**이라는 JSON 파일을 **C:\ADFGetStartedPSH** 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-231">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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

    <span data-ttu-id="2a1f7-232">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-232">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="2a1f7-233">속성</span><span class="sxs-lookup"><span data-stu-id="2a1f7-233">Property</span></span> | <span data-ttu-id="2a1f7-234">설명</span><span class="sxs-lookup"><span data-stu-id="2a1f7-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2a1f7-235">type</span><span class="sxs-lookup"><span data-stu-id="2a1f7-235">type</span></span> | <span data-ttu-id="2a1f7-236">Azure Blob 저장소에 데이터가 있기 때문에 type 속성은 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-236">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="2a1f7-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2a1f7-237">linkedServiceName</span></span> | <span data-ttu-id="2a1f7-238">이전에 만든 **AzureStorageLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-238">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2a1f7-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="2a1f7-239">folderPath</span></span> | <span data-ttu-id="2a1f7-240">입력 Blob이 포함된 Blob **컨테이너**와 **폴더**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-240">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="2a1f7-241">이 자습서에서 adftutorial은 Blob 컨테이너이며, 폴더는 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-241">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="2a1f7-242">fileName</span><span class="sxs-lookup"><span data-stu-id="2a1f7-242">fileName</span></span> | <span data-ttu-id="2a1f7-243">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-243">This property is optional.</span></span> <span data-ttu-id="2a1f7-244">이 속성을 생략하면 folderPath의 모든 파일이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-244">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="2a1f7-245">이 자습서에서는 fileName에 대해 **emp.txt**를 지정하므로 해당 파일만 처리를 위해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-245">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="2a1f7-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="2a1f7-246">format -> type</span></span> |<span data-ttu-id="2a1f7-247">입력 파일은 텍스트 형식이므로 **TextFormat**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-247">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="2a1f7-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="2a1f7-248">columnDelimiter</span></span> | <span data-ttu-id="2a1f7-249">입력 파일의 열은 **쉼표(`,`)**로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-249">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="2a1f7-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2a1f7-250">frequency/interval</span></span> | <span data-ttu-id="2a1f7-251">frequency는 **Hour**로 설정되고, interval은 **1**로 설정됩니다. 즉 입력 조각이 **매시간** 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-251">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="2a1f7-252">다시 말하면, Data Factory 서비스가 지정한 Blob 컨테이너(**adftutorial**)의 루트 폴더에서 매 시간마다 입력 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-252">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="2a1f7-253">이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 내에 있는 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-253">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="2a1f7-254">external</span><span class="sxs-lookup"><span data-stu-id="2a1f7-254">external</span></span> | <span data-ttu-id="2a1f7-255">이 파이프라인에 의해 데이터가 생성되지 않는 경우 이 속성은 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-255">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="2a1f7-256">이 자습서의 입력 데이터는 이 파이프라인에 의해 생성되지 않는 emp.txt 파일에 있으므로 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-256">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="2a1f7-257">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="2a1f7-258">다음 명령을 실행하여 데이터 팩터리 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-258">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="2a1f7-259">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-259">Here is the sample output:</span></span>

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

### <a name="create-an-output-dataset"></a><span data-ttu-id="2a1f7-260">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="2a1f7-260">Create an output dataset</span></span>
<span data-ttu-id="2a1f7-261">이 단계의 일부에서는 **OutputDataset**라는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-261">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="2a1f7-262">이 데이터 집합은 **AzureSqlLinkedService**가 나타내는 Azure SQL Database에서 SQL 테이블을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-262">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="2a1f7-263">다음 내용이 포함된 **OutputDataset.json**이라는 JSON 파일을 **C:\ADFGetStartedPSH** 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-263">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

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

    <span data-ttu-id="2a1f7-264">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-264">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="2a1f7-265">속성</span><span class="sxs-lookup"><span data-stu-id="2a1f7-265">Property</span></span> | <span data-ttu-id="2a1f7-266">설명</span><span class="sxs-lookup"><span data-stu-id="2a1f7-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="2a1f7-267">type</span><span class="sxs-lookup"><span data-stu-id="2a1f7-267">type</span></span> | <span data-ttu-id="2a1f7-268">Azure SQL 데이터베이스의 테이블에 데이터가 복사되기 때문에 type 속성은 **AzureSqlTable**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="2a1f7-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2a1f7-269">linkedServiceName</span></span> | <span data-ttu-id="2a1f7-270">이전에 만든 **AzureSqlLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="2a1f7-271">tableName</span><span class="sxs-lookup"><span data-stu-id="2a1f7-271">tableName</span></span> | <span data-ttu-id="2a1f7-272">데이터가 복사되는 **테이블**을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-272">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="2a1f7-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="2a1f7-273">frequency/interval</span></span> | <span data-ttu-id="2a1f7-274">frequency는 **Hour**로 설정되고, interval은 **1**입니다. 즉 출력 조각이 이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 사이에서 **매시간** 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="2a1f7-275">데이터베이스의 emp 테이블에 **ID**, **FirstName** 및 **LastName**이라는 세 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="2a1f7-276">ID는 ID 열이므로 여기서 **FirstName** 및 **LastName**만 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="2a1f7-277">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="2a1f7-278">다음 명령을 실행하여 Data Factory 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-278">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="2a1f7-279">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-279">Here is the sample output:</span></span>

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

## <a name="create-a-pipeline"></a><span data-ttu-id="2a1f7-280">파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-280">Create a pipeline</span></span>
<span data-ttu-id="2a1f7-281">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="2a1f7-282">현재 출력 데이터 집합은 일정을 작동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-282">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="2a1f7-283">이 자습서에서는 출력 데이터 집합이 한 시간에 한 번씩 조각을 생성하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="2a1f7-284">이 파이프라인은 하루 24시간 간격, 즉 24시간 동안에 걸친 시작 시간과 종료 시간을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="2a1f7-285">따라서 24개의 출력 데이터 집합이 파이프라인에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 


1. <span data-ttu-id="2a1f7-286">**C:\ADFGetStartedPSH** 폴더에 다음과 같은 내용으로 **ADFTutorialPipeline.json**이라는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-286">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
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
    <span data-ttu-id="2a1f7-287">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-287">Note the following points:</span></span>
   
    - <span data-ttu-id="2a1f7-288">작업 섹션에는 **형식**이 **복사**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="2a1f7-289">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2a1f7-290">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="2a1f7-291">작업에 대한 입력을 **InputDataset**으로 설정하고 작업에 대한 출력을 **OutputDataset**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="2a1f7-292">**typeProperties** 섹션에서 **BlobSource**를 원본 유형으로 지정하고 **SqlSink**를 싱크 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="2a1f7-293">복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 전체 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2a1f7-294">지원되는 특정 데이터 저장소를 원본/싱크로 사용하는 방법을 알아보려면 표에 나와 있는 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="2a1f7-295">**시작** 속성 값을 현재 날짜로 바꾸고 **종료** 값을 다음 날짜로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-295">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="2a1f7-296">날짜 부분만 지정하고 날짜/시간의 시간 부분은 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-296">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="2a1f7-297">예를 들어, "2016-02-03"은 "2016-02-03T00:00:00Z"과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-297">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="2a1f7-298">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="2a1f7-299">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="2a1f7-300">**종료** 시간은 선택 사항이지만 이 자습서에서는 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-300">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="2a1f7-301">**종료** 속성 값을 지정하지 않는 경우 "**시작 + 48시간**"으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-301">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="2a1f7-302">파이프라인을 무기한 실행하려면 **종료** 속성 값으로 **9999-09-09**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-302">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="2a1f7-303">앞의 예에서는 각 데이터 조각이 1시간마다 생성되므로 24개 데이터 조각이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-303">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="2a1f7-304">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2a1f7-305">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="2a1f7-306">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="2a1f7-307">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="2a1f7-308">다음 명령을 실행하여 Data Factory 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-308">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="2a1f7-309">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-309">Here is the sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="2a1f7-310">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="2a1f7-310">**Congratulations!**</span></span> <span data-ttu-id="2a1f7-311">Azure Blob 저장소에서 Azure SQL 데이터베이스로 데이터를 복사하는 파이프라인이 있는 Azure 데이터 팩터리를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="2a1f7-312">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="2a1f7-312">Monitor the pipeline</span></span>
<span data-ttu-id="2a1f7-313">이 단계에서는 Azure PowerShell을 사용하여 Azure Data Factory에서 어떤 일이 일어나는지 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-313">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="2a1f7-314">&lt;DataFactoryName&gt;을 데이터 팩터리 이름으로 바꿔 **Get-AzureRmDataFactory**를 실행하고, 출력을 $df 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-314">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="2a1f7-315">예:</span><span class="sxs-lookup"><span data-stu-id="2a1f7-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="2a1f7-316">그런 다음 $df의 내용을 출력하도록(print) 실행하여 다음 출력을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-316">Then, run print the contents of $df to see the following output:</span></span> 
    
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
2. <span data-ttu-id="2a1f7-317">**Get-AzureRmDataFactorySlice**를 실행하여 파이프라인의 출력 데이터 집합인 **OutputDataset**의 모든 조각에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-317">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="2a1f7-318">이 설정은 파이프라인 JSON의 **시작** 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-318">This setting should match the **Start** value in the pipeline JSON.</span></span> <span data-ttu-id="2a1f7-319">현재 날짜의 오전 12시부터 다음 날짜의 오전 12시까지 각 시간마다 하나씩, 24개의 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-319">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="2a1f7-320">다음은 출력의 세 가지 샘플 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-320">Here are three sample slices from the output:</span></span> 

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
3. <span data-ttu-id="2a1f7-321">**Get-AzureRmDataFactoryRun**을 실행하여 **특정** 조각에 대한 작업 실행의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-321">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="2a1f7-322">이전 명령의 출력에서 날짜-시간 값을 복사하여 StartDateTime 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-322">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="2a1f7-323">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-323">Here is the sample output:</span></span> 

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

<span data-ttu-id="2a1f7-324">Data Factory cmdlet에 대한 포괄적인 설명서는 [Data Factory cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="2a1f7-325">요약</span><span class="sxs-lookup"><span data-stu-id="2a1f7-325">Summary</span></span>
<span data-ttu-id="2a1f7-326">이 자습서에서는 Azure Blob에서 Azure SQL 데이터베이스로 데이터를 복사하는 Azure Data Factory를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-326">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="2a1f7-327">PowerShell를 사용하여 데이터 팩터리, 연결된 서비스, 데이터 집합 및 파이프라인을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-327">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="2a1f7-328">이 자습서에서 수행한 단계를 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-328">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="2a1f7-329">Azure **Data Factory**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="2a1f7-330">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-330">Created **linked services**:</span></span>

   <span data-ttu-id="2a1f7-331">a.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-331">a.</span></span> <span data-ttu-id="2a1f7-332">입력 데이터를 보유하는 Azure Storage 계정을 연결하는 **Azure Storage**에 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-332">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="2a1f7-333">b.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-333">b.</span></span> <span data-ttu-id="2a1f7-334">출력 데이터를 보유하는 SQL Database를 연결하는 **Azure SQL** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-334">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
3. <span data-ttu-id="2a1f7-335">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="2a1f7-336">원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a1f7-337">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a1f7-337">Next steps</span></span>
<span data-ttu-id="2a1f7-338">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="2a1f7-339">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-339">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="2a1f7-340">데이터 저장소간에 데이터를 복사하는 방법에 대해 알아보려면 테이블에서 데이터 저장소에 대한 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1f7-340">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span> 

