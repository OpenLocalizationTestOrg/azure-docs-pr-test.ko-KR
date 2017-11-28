---
title: "자습서: 데이터를 복사하는 Azure Data Factory 파이프라인 만들기 (Azure Portal) | Microsoft Docs"
description: "이 자습서에서는 Azure Portal을 사용하여 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8072a863fab0b304ccbbba639aa56b403e8f37c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-portal-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="fb604-103">자습서: Azure Portal을 사용하여 데이터를 복사하는 Data Factory 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-103">Tutorial: Use Azure portal to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb604-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="fb604-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="fb604-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="fb604-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="fb604-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fb604-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="fb604-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb604-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="fb604-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb604-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="fb604-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="fb604-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="fb604-110">REST API</span><span class="sxs-lookup"><span data-stu-id="fb604-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="fb604-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="fb604-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="fb604-112">이 문서에서는 [Azure Portal](https://portal.azure.com)을 사용하여 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 파이프라인이 있는 데이터 팩터리를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-112">In this article, you learn how to use [Azure portal](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="fb604-113">Azure Data Factory를 처음 사용하는 경우 이 자습서를 수행하기 전에 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="fb604-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="fb604-115">복사 작업은 지원되는 데이터 저장소에서 지원되는 싱크 데이터 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="fb604-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fb604-117">이 작업은 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="fb604-118">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="fb604-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fb604-120">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="fb604-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="fb604-122">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="fb604-123">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb604-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fb604-124">Prerequisites</span></span>
<span data-ttu-id="fb604-125">이 자습서를 수행하기 전에 [자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서에서 나열하는 필수 구성 요소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-125">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="fb604-126">단계</span><span class="sxs-lookup"><span data-stu-id="fb604-126">Steps</span></span>
<span data-ttu-id="fb604-127">이 자습서의 일부로 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-127">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="fb604-128">Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-128">Create an Azure **data factory**.</span></span> <span data-ttu-id="fb604-129">이 단계에서는 ADFTutorialDataFactory라는 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-129">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="fb604-130">데이터 팩터리에서 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-130">Create **linked services** in the data factory.</span></span> <span data-ttu-id="fb604-131">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-131">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="fb604-132">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-132">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="fb604-133">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 컨테이너를 만들고 이 저장소 계정에 데이터를 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-133">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="fb604-134">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-134">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="fb604-135">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-135">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="fb604-136">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-136">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="fb604-137">데이터 팩터리에서 입력 및 출력 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-137">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="fb604-138">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-138">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="fb604-139">그리고 입력 Blob 데이터 집합은 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-139">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="fb604-140">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-140">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="fb604-141">그리고 출력 SQL 테이블 데이터 집합은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-141">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="fb604-142">데이터 팩터리에서 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-142">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="fb604-143">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-143">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="fb604-144">복사 활동은 Azure Blob 저장소의 Blob에서 Azure SQL 데이터베이스의 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-144">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="fb604-145">파이프라인의 복사 활동을 사용하여 지원되는 모든 원본의 데이터를 지원되는 모든 대상으로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-145">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="fb604-146">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-146">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="fb604-147">파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-147">Monitor the pipeline.</span></span> <span data-ttu-id="fb604-148">이 단계에서는 Azure Portal을 사용하여 입력 및 출력 데이터 집합의 조각을 **모니터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-148">In this step, you **monitor** the slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="fb604-149">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-149">Create data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fb604-150">아직 완료하지 않은 경우 [자습서의 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-150">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="fb604-151">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-151">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fb604-152">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-152">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fb604-153">예를 들어 원본에서 대상 데이터 저장소에 데이터를 복사하는 복사 작업 및 입력 데이터를 제품 출력 데이터로 변환하는 Hive 스크립트를 실행하는 HDInsight Hive 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-153">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="fb604-154">이 단계에서는 데이터 팩터리 만들기를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-154">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="fb604-155">[Azure Portal](https://portal.azure.com/)에 로그인한 후에 왼쪽 메뉴에서 **새로 만들기**를 클릭하고 **데이터 + 분석**을 클릭한 다음 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-155">After logging in to the [Azure portal](https://portal.azure.com/), click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="fb604-157">**새 데이터 팩터리** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-157">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="fb604-158">**ADFTutorialDataFactory**를 **이름**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-158">Enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
         ![새 데이터 팩터리 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="fb604-160">Azure Data Factory의 이름은 **전역적으로 고유**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-160">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="fb604-161">다음 오류가 표시되는 경우 데이터 팩터리 이름을 변경하고(예: yournameADFTutorialDataFactory) 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-161">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="fb604-162">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-162">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="fb604-164">데이터 팩터리를 만들려는 위치에 Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-164">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
   3. <span data-ttu-id="fb604-165">**리소스 그룹**에 대해 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-165">For the **Resource Group**, do one of the following steps:</span></span>
      
      - <span data-ttu-id="fb604-166">**기존 항목 사용**을 선택하고 드롭다운 목록에서 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-166">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="fb604-167">**새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-167">Select **Create new**, and enter the name of a resource group.</span></span>   
         
          <span data-ttu-id="fb604-168">이 자습서의 일부 단계에서는 리소스 그룹에 **ADFTutorialResourceGroup** 이라는 이름을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-168">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="fb604-169">리소스 그룹에 대한 자세한 내용은 [리소스 그룹을 사용하여 Azure 리소스 관리](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-169">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="fb604-170">데이터 팩터리의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-170">Select the **location** for the data factory.</span></span> <span data-ttu-id="fb604-171">Data Factory 서비스에서 지원하는 지역만 드롭다운 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-171">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   5. <span data-ttu-id="fb604-172">**대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-172">Select **Pin to dashboard**.</span></span>     
   6. <span data-ttu-id="fb604-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-173">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="fb604-174">데이터 팩터리 인스턴스를 만들려면 구독/리소스 그룹 수준에서 [데이터 팩터리 참여자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-174">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
      > 
      > <span data-ttu-id="fb604-175">데이터 팩터리의 이름은 나중에 DNS 이름으로 표시되므로 공개적으로 등록될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-175">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>                
      > 
      > 
3. <span data-ttu-id="fb604-176">대시보드에서 **데이터 팩터리 배포 중** 상태의 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-176">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![데이터 팩터리 배포 중 타일](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="fb604-178">만들기가 완료되면 이미지와 같이 **Data Factory** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-178">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span></span>
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="fb604-180">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-180">Create linked services</span></span>
<span data-ttu-id="fb604-181">데이터 팩터리에서 연결된 서비스를 만들어 데이터 저장소를 연결하고 계산 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-181">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="fb604-182">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-182">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="fb604-183">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-183">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="fb604-184">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-184">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="fb604-185">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-185">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="fb604-186">이 저장소 계정은 컨테이너를 만들고 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 데이터를 업로드한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-186">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="fb604-187">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-187">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="fb604-188">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-188">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="fb604-189">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 emp 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-189">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="fb604-190">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-190">Create Azure Storage linked service</span></span>
<span data-ttu-id="fb604-191">이 단계에서는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-191">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="fb604-192">이 섹션의 Azure 저장소 계정 이름 및 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-192">You specify the name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="fb604-193">**Data Factory** 블레이드에서 **작성자 및 배포** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-193">In the **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![작성 및 배포 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="fb604-195">다음 이미지와 같이 **Data Factory Editor**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-195">You see the **Data Factory Editor** as shown in the following image:</span></span> 

    ![데이터 팩터리 편집기](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="fb604-197">편집기의 도구 모음에서 **새 데이터 저장소** 단추를 클릭하고, 드롭다운 메뉴에서 **Azure 저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-197">In the editor, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span></span> <span data-ttu-id="fb604-198">오른쪽 창에 Azure 저장소 연결된 서비스를 만들기 위한 JSON 템플릿이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-198">You should see the JSON template for creating an Azure storage linked service in the right pane.</span></span> 
   
    ![편집기 새 데이터 저장소 단추](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="fb604-200">`<accountname>` 및 `<accountkey>`를 Azure Storage 계정의 계정 이름 및 계정 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-200">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span></span> 
   
    ![편집기 Blob 저장소 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="fb604-202">도구 모음에서 **배포** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-202">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="fb604-203">이제 트리 보기에서 배포된 **AzureStorageLinkedService** 가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-203">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span></span> 
   
    ![편집기 Blob 저장소 배포](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="fb604-205">연결된 서비스 정의의 JSON 속성에 대한 자세한 내용은 [Azure Blob Storage 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-205">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-the-azure-sql-database"></a><span data-ttu-id="fb604-206">Azure SQL 데이터베이스에 대한 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-206">Create a linked service for the Azure SQL Database</span></span>
<span data-ttu-id="fb604-207">이 단계에서는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-207">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="fb604-208">이 섹션에서 Azure SQL 서버 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-208">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="fb604-209">**Data Factory 편집기**의 도구 모음에서 **새 데이터 저장소** 단추를 클릭하고 드롭다운 메뉴에서 **Azure SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-209">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span></span> <span data-ttu-id="fb604-210">오른쪽 창에 Azure SQL 연결된 서비스를 만들기 위한 JSON 템플릿이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-210">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span></span>
2. <span data-ttu-id="fb604-211">`<servername>`, `<databasename>`, `<username>@<servername>` 및 `<password>`를 Azure SQL Server의 이름, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-211">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="fb604-212">도구 모음에서 **배포**를 클릭하여 **AzureSqlLinkedService**를 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-212">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="fb604-213">**연결된 서비스** 아래의 트리 보기에서 **AzureSqlLinkedService**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-213">Confirm that you see **AzureSqlLinkedService** in the tree view under **Linked services**.</span></span>  

    <span data-ttu-id="fb604-214">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-214">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="fb604-215">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-215">Create datasets</span></span>
<span data-ttu-id="fb604-216">이전 단계에서는 Azure Storage 계정과 Azure SQL Database를 데이터 팩터리에 연결하는 연결된 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-216">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="fb604-217">이 단계에서는 AzureStorageLinkedService 및 AzureSqlLinkedService에서 각각 참조하는 데이터 저장소에 저장된 입력 및 출력 데이터를 나타내는 InputDataset 및 OutputDataset이라는 두 개의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-217">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="fb604-218">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-218">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="fb604-219">그리고 입력 Blob 데이터 집합(InputDataset)은 입력 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-219">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="fb604-220">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-220">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="fb604-221">그리고 출력 SQL 테이블 데이터 집합(OututDataset)은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-221">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="fb604-222">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-222">Create input dataset</span></span>
<span data-ttu-id="fb604-223">이 단계에서는 AzureStorageLinkedService 연결된 서비스에서 나타내는 Azure Storage의 Blob 컨테이너(adftutorial)의 루트 폴더에 있는 Blob 파일(emp.txt)을 가리키는 InputDataset이라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-223">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="fb604-224">fileName 값을 지정하지 않거나 건너뛰면 입력 폴더에 있는 모든 Blob의 데이터가 대상에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-224">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="fb604-225">이 자습서에서는 fileName 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-225">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="fb604-226">Data Factor의 **편집기**에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 드롭 다운 메뉴에서 **Azure Blob Storage**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-226">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span></span> 
   
    ![새 데이터 집합 메뉴](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="fb604-228">오른쪽 창의 JSON을 다음 JSON 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-228">Replace JSON in the right pane with the following JSON snippet:</span></span> 
   
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
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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

    <span data-ttu-id="fb604-229">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-229">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="fb604-230">속성</span><span class="sxs-lookup"><span data-stu-id="fb604-230">Property</span></span> | <span data-ttu-id="fb604-231">설명</span><span class="sxs-lookup"><span data-stu-id="fb604-231">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fb604-232">type</span><span class="sxs-lookup"><span data-stu-id="fb604-232">type</span></span> | <span data-ttu-id="fb604-233">Azure Blob 저장소에 데이터가 있기 때문에 type 속성은 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-233">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="fb604-234">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fb604-234">linkedServiceName</span></span> | <span data-ttu-id="fb604-235">이전에 만든 **AzureStorageLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-235">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fb604-236">folderPath</span><span class="sxs-lookup"><span data-stu-id="fb604-236">folderPath</span></span> | <span data-ttu-id="fb604-237">입력 Blob이 포함된 Blob **컨테이너**와 **폴더**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-237">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="fb604-238">이 자습서에서 adftutorial은 Blob 컨테이너이며, 폴더는 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-238">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="fb604-239">fileName</span><span class="sxs-lookup"><span data-stu-id="fb604-239">fileName</span></span> | <span data-ttu-id="fb604-240">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-240">This property is optional.</span></span> <span data-ttu-id="fb604-241">이 속성을 생략하면 folderPath의 모든 파일이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-241">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="fb604-242">이 자습서에서는 fileName에 대해 **emp.txt**를 지정하므로 해당 파일만 처리를 위해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-242">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="fb604-243">format -> type</span><span class="sxs-lookup"><span data-stu-id="fb604-243">format -> type</span></span> |<span data-ttu-id="fb604-244">입력 파일은 텍스트 형식이므로 **TextFormat**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-244">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="fb604-245">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fb604-245">columnDelimiter</span></span> | <span data-ttu-id="fb604-246">입력 파일의 열은 **쉼표(`,`)**로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-246">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="fb604-247">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="fb604-247">frequency/interval</span></span> | <span data-ttu-id="fb604-248">frequency는 **Hour**로 설정되고, interval은 **1**로 설정됩니다. 즉 입력 조각이 **매시간** 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-248">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="fb604-249">다시 말하면, Data Factory 서비스가 지정한 Blob 컨테이너(**adftutorial**)의 루트 폴더에서 매 시간마다 입력 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-249">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="fb604-250">이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 내에 있는 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-250">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="fb604-251">external</span><span class="sxs-lookup"><span data-stu-id="fb604-251">external</span></span> | <span data-ttu-id="fb604-252">이 파이프라인에 의해 데이터가 생성되지 않는 경우 이 속성은 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-252">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="fb604-253">이 자습서의 입력 데이터는 이 파이프라인에 의해 생성되지 않는 emp.txt 파일에 있으므로 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-253">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="fb604-254">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-254">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="fb604-255">도구 모음에서 **배포**를 클릭하여 **InputDataset** 데이터 집합을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-255">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span></span> <span data-ttu-id="fb604-256">트리 뷰에 **InputDataset** 이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-256">Confirm that you see the **InputDataset** in the tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="fb604-257">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-257">Create output dataset</span></span>
<span data-ttu-id="fb604-258">Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL Database에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-258">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="fb604-259">이 단계에서 만든 출력 SQL 테이블 데이터 집합(OututDataset)은 Blob Storage의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-259">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="fb604-260">Data Factor의 **편집기**에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 드롭 다운 메뉴에서 **Azure SQL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-260">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span></span> 
2. <span data-ttu-id="fb604-261">오른쪽 창의 JSON을 다음 JSON 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-261">Replace JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="fb604-262">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-262">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="fb604-263">속성</span><span class="sxs-lookup"><span data-stu-id="fb604-263">Property</span></span> | <span data-ttu-id="fb604-264">설명</span><span class="sxs-lookup"><span data-stu-id="fb604-264">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fb604-265">type</span><span class="sxs-lookup"><span data-stu-id="fb604-265">type</span></span> | <span data-ttu-id="fb604-266">Azure SQL 데이터베이스의 테이블에 데이터가 복사되기 때문에 type 속성은 **AzureSqlTable**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-266">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="fb604-267">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fb604-267">linkedServiceName</span></span> | <span data-ttu-id="fb604-268">이전에 만든 **AzureSqlLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-268">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fb604-269">tableName</span><span class="sxs-lookup"><span data-stu-id="fb604-269">tableName</span></span> | <span data-ttu-id="fb604-270">데이터가 복사되는 **테이블**을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-270">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="fb604-271">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="fb604-271">frequency/interval</span></span> | <span data-ttu-id="fb604-272">frequency는 **Hour**로 설정되고, interval은 **1**입니다. 즉 출력 조각이 이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 사이에서 **매시간** 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-272">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="fb604-273">데이터베이스의 emp 테이블에 **ID**, **FirstName** 및 **LastName**이라는 세 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-273">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="fb604-274">ID는 ID 열이므로 여기서 **FirstName** 및 **LastName**만 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-274">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="fb604-275">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-275">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="fb604-276">도구 모음에서 **배포**를 클릭하여 **OutputDataset** 데이터 집합을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-276">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span></span> <span data-ttu-id="fb604-277">**데이터 집합**의 트리 보기에서 **OutputDataset**이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-277">Confirm that you see the **OutputDataset** in the tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="fb604-278">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="fb604-278">Create pipeline</span></span>
<span data-ttu-id="fb604-279">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-279">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="fb604-280">현재 출력 데이터 집합은 일정을 작동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-280">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="fb604-281">이 자습서에서는 출력 데이터 집합이 한 시간에 한 번씩 조각을 생성하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-281">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="fb604-282">이 파이프라인은 하루 24시간 간격, 즉 24시간 동안에 걸친 시작 시간과 종료 시간을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-282">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="fb604-283">따라서 24개의 출력 데이터 집합이 파이프라인에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-283">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="fb604-284">Data Factor의 **편집기**에서 **... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-284">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="fb604-285">또는 트리 뷰에서 **파이프라인**을 마우스 오른쪽 단추로 클릭하고 **새 파이프라인**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-285">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="fb604-286">오른쪽 창의 JSON을 다음 JSON 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-286">Replace JSON in the right pane with the following JSON snippet:</span></span> 

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
    
    <span data-ttu-id="fb604-287">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-287">Note the following points:</span></span>
   
    - <span data-ttu-id="fb604-288">작업 섹션에는 **형식**이 **복사**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="fb604-289">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fb604-290">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="fb604-291">작업에 대한 입력을 **InputDataset**으로 설정하고 작업에 대한 출력을 **OutputDataset**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="fb604-292">**typeProperties** 섹션에서 **BlobSource**를 원본 유형으로 지정하고 **SqlSink**를 싱크 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="fb604-293">복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 전체 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fb604-294">지원되는 특정 데이터 저장소를 원본/싱크로 사용하는 방법을 알아보려면 표에 나와 있는 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>
    - <span data-ttu-id="fb604-295">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-295">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="fb604-296">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-296">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="fb604-297">**종료** 시간은 선택 사항이지만 이 자습서에서는 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-297">The **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="fb604-298">**종료** 속성 값을 지정하지 않는 경우 "**시작 + 48시간**"으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-298">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="fb604-299">파이프라인을 무기한 실행하려면 **종료** 속성 값으로 **9999-09-09**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-299">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="fb604-300">앞의 예에서는 각 데이터 조각이 1시간마다 생성되므로 24개 데이터 조각이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-300">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="fb604-301">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-301">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fb604-302">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-302">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fb604-303">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-303">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="fb604-304">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-304">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="fb604-305">도구 모음에서 **배포**를 클릭하여 **ADFTutorialPipeline**을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-305">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span></span> <span data-ttu-id="fb604-306">트리 뷰에 파이프라인이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-306">Confirm that you see the pipeline in the tree view.</span></span> 
4. <span data-ttu-id="fb604-307">이제 **X**를 클릭하여 **편집기** 블레이드를 닫습니다. **X**를 다시 클릭하여 **ADFTutorialDataFactory**에 대한 **Data Factory** 홈페이지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-307">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="fb604-308">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="fb604-308">**Congratulations!**</span></span> <span data-ttu-id="fb604-309">Azure Blob 저장소에서 Azure SQL 데이터베이스로 데이터를 복사하는 파이프라인이 있는 Azure 데이터 팩터리를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-309">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="fb604-310">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="fb604-310">Monitor pipeline</span></span>
<span data-ttu-id="fb604-311">이 단계에서는 Azure 포털을 사용하여 Azure Data Factory에서 어떤 일이 일어나는지 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-311">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="fb604-312">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="fb604-312">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="fb604-313">다음 단계에서는 [모니터링 및 관리] 응용 프로그램을 사용하여 데이터 팩터리의 파이프라인을 모니터링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-313">The following steps show you how to monitor pipelines in your data factory by using the Monitor & Manage application:</span></span> 

1. <span data-ttu-id="fb604-314">데이터 팩터리의 홈페이지에서 **모니터링 및 관리** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-314">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>
   
    ![타일 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="fb604-316">별도의 탭에서 **모니터링 및 관리 응용 프로그램**이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-316">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="fb604-317">웹 브라우저가 "권한 부여 중..." 상태에서 갇혀 있음이 확인되면, **타사 쿠키 및 사이트 데이터 차단** 확인란의 선택을 해제하거나 **login.microsoftonline.com**에 대한 예외를 만든 다음, 앱을 다시 열어봅니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-317">If you see that the web browser is stuck at "Authorizing...", do one of the following: clear the **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="fb604-319">파이프라인의 시작 시간(2017-05-11) 및 종료 시간(2017-05-12)을 포함하도록 **시작 시간** 및 **종료 시간**을 변경하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-319">Change the **Start time** and **End time** to include start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>       
3. <span data-ttu-id="fb604-320">중간 창의 목록에서 파이프라인의 시작 시간과 종료 시간 사이의 각 시간과 연관된 **활동 창**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-320">You see the **activity windows** associated with each hour between pipeline start and end times in the list in the middle pane.</span></span> 
4. <span data-ttu-id="fb604-321">활동 창에 대한 세부 정보를 보려면 **활동 창** 목록에서 해당 활동 창을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-321">To see details about an activity window, select the activity window in the **Activity Windows** list.</span></span> 
    <span data-ttu-id="fb604-322">![활동 창 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="fb604-322">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="fb604-323">오른쪽의 [활동 창 탐색기]에서 현재 UTC 시간(오후 8시 12분)까지의 조각이 모두 처리됩니다(녹색으로 표시됨).</span><span class="sxs-lookup"><span data-stu-id="fb604-323">In Activity Window Explorer on the right, you see that the slices up to the current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="fb604-324">오후 8-9시, 오후 9-10시, 오후 10-11시, 오후 11-12시의 조각은 아직 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-324">The 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="fb604-325">오른쪽 창의 **시도** 섹션은 해당 데이터 조각에 대해 실행된 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-325">The **Attempts** section in the right pane provides information about the activity run for the data slice.</span></span> <span data-ttu-id="fb604-326">오류가 발생한 경우 오류에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-326">If there was an error, it provides details about the error.</span></span> <span data-ttu-id="fb604-327">예를 들어 입력된 폴더 또는 컨테이너가 존재하지 않고 조각 처리가 실패하면 해당 컨테이너 또는 폴더가 존재하지 않는다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-327">For example, if the input folder or container does not exist and the slice processing fails, you see an error message stating that the container or folder does not exist.</span></span>

    ![활동 실행 시도](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="fb604-329">**SQL Server Management Studio**를 시작하고 Azure SQL Database에 연결한 다음 데이터베이스의 **emp** 테이블에 행이 삽입되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-329">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="fb604-331">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-331">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="fb604-332">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="fb604-332">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="fb604-333">다이어그램 보기를 사용하여 데이터 파이프라인을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-333">You can also monitor data pipelines by using the diagram view.</span></span>  

1. <span data-ttu-id="fb604-334">**Data Factory** 블레이드에서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-334">In the **Data Factory** blade, click **Diagram**.</span></span>
   
    ![데이터 팩터리 블레이드 - 다이어그램 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="fb604-336">다음 이미지와 유사한 다이어그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-336">You should see the diagram similar to the following image:</span></span> 
   
    ![다이어그램 뷰](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="fb604-338">다이어그램 보기에서 **InputDataset**을 두 번 클릭하여 데이터 집합의 조각을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-338">In the diagram view, double-click **InputDataset** to see slices for the dataset.</span></span>  
   
    ![InputDataset을 선택한 데이터 집합](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="fb604-340">**자세히 보기**를 클릭하여 모든 데이터 조각을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-340">Click **See more** link to see all the data slices.</span></span> <span data-ttu-id="fb604-341">24시간의 매시간 조각 중 파이프라인의 시작 시간과 종료 시간 사이에 있는 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-341">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![모든 입력 데이터 조각](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="fb604-343">**emp.txt** 파일이 항상 **adftutorial\input** Blob 컨테이너에 있으므로 현재 UTC 시간까지의 모든 데이터 조각은 **준비** 상태로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-343">Notice that all the data slices up to the current UTC time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span></span> <span data-ttu-id="fb604-344">이후 시간의 조각은 아직 준비 상태에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-344">The slices for the future times are not in ready state yet.</span></span> <span data-ttu-id="fb604-345">맨 아래의 **Recently failed slices(최근에 실패한 조각)** 섹션에 표시되는 조각이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-345">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span></span>
6. <span data-ttu-id="fb604-346">다이어그램 보기를 표시할 때까지 블레이드를 닫거나 왼쪽으로 스크롤하여 다이어그램 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-346">Close the blades until you see the diagram view (or) scroll left to see the diagram view.</span></span> <span data-ttu-id="fb604-347">그런 다음 **OutputDataset**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-347">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="fb604-348">**OutputDataset**에 대한 **테이블** 블레이드에서 **자세히 보기** 링크를 클릭하여 모든 조각을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-348">Click **See more** link on the **Table** blade for **OutputDataset** to see all the slices.</span></span>

    ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="fb604-350">현재 UTC 시간까지의 모든 조각이 **실행 보류 중** 상태 => **진행 중** ==> **준비** 상태로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-350">Notice that all the slices up to the current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="fb604-351">과거(현재 시간 이전)의 조각은 기본적으로 최신 조각에서 가장 오래된 조각순으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-351">The slices from the past (before current time) are processed from latest to oldest by default.</span></span> <span data-ttu-id="fb604-352">예를 들어 현재 시간이 오후 8시 12분 UTC인 경우 오후 7-8시 조각이 오후 6-7시 조각보다 먼저 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-352">For example, if the current time is 8:12 PM UTC, the slice for 7 PM - 8 PM is processed ahead of the 6 PM - 7 PM slice.</span></span> <span data-ttu-id="fb604-353">오후 8-9시 조각은 기본적으로 시간 간격이 끝날 때, 즉 오후 9시 이후에 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-353">The 8 PM - 9 PM slice is processed at the end of the time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="fb604-354">목록에서 아무 데이터 조각이나 클릭하면 **데이터 조각** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-354">Click any data slice from the list and you should see the **Data slice** blade.</span></span> <span data-ttu-id="fb604-355">활동 창과 연결된 데이터 부분을 조각이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-355">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="fb604-356">조각은 하나의 파일이거나 여러 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-356">A slice can be one file or multiple files.</span></span>  
    
     ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="fb604-358">조각이 **준비** 상태가 아닌 경우 **준비되지 않은 업스트림 슬라이스** 목록에서 [준비] 상태가 아니고 현재 조각의 실행을 차단하는 업스트림 조각을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-358">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="fb604-359">**데이터 조각** 블레이드의 맨 아래 목록에 모든 작업 실행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-359">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span></span> <span data-ttu-id="fb604-360">**작업 실행**을 클릭하여 **작업 실행 세부 정보** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-360">Click an **activity run** to see the **Activity run details** blade.</span></span> 
    
    ![작업 실행 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="fb604-362">이 블레이드에서 복사 작업의 소요 시간, 처리량, 읽기/쓰기된 데이터의 바이트 크기, 실행 시작 시간, 실행 종료 시간 등을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-362">In this blade, you see how long the copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="fb604-363">**X**를 클릭하여 모든 블레이드를 닫아 **ADFTutorialDataFactory**의 홈 블레이드로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-363">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="fb604-364">(선택 사항) **데이터 집합** 타일 또는 **파이프라인** 타일을 클릭하여 이전 단계에서 표시한 블레이드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-364">(optional) click the **Datasets** tile or **Pipelines** tile to get the blades you have seen the preceding steps.</span></span> 
14. <span data-ttu-id="fb604-365">**SQL Server Management Studio**를 시작하고 Azure SQL Database에 연결한 다음 데이터베이스의 **emp** 테이블에 행이 삽입되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-365">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="fb604-367">요약</span><span class="sxs-lookup"><span data-stu-id="fb604-367">Summary</span></span>
<span data-ttu-id="fb604-368">이 자습서에서는 Azure Blob에서 Azure SQL 데이터베이스로 데이터를 복사하는 Azure Data Factory를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-368">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="fb604-369">Azure 포털을 사용하여 데이터 팩터리, 연결된 서비스, 데이터 집합 및 파이프라인을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-369">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="fb604-370">이 자습서에서 수행한 단계를 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-370">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="fb604-371">Azure **Data Factory**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-371">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fb604-372">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-372">Created **linked services**:</span></span>
   1. <span data-ttu-id="fb604-373">입력 데이터를 보유하는 Azure 저장소 계정을 연결하는 **Azure 저장소** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-373">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="fb604-374">출력 데이터를 보유하는 Azure SQL 데이터베이스를 연결하는 **Azure SQL** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-374">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="fb604-375">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-375">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="fb604-376">원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-376">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fb604-377">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb604-377">Next steps</span></span>
<span data-ttu-id="fb604-378">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-378">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="fb604-379">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb604-379">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="fb604-380">데이터 저장소간에 데이터를 복사하는 방법에 대해 알아보려면 테이블에서 데이터 저장소에 대한 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="fb604-380">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>