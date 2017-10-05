---
title: "자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 Visual Studio를 사용하여 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="7c37b-103">자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c37b-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7c37b-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="7c37b-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="7c37b-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="7c37b-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7c37b-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="7c37b-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c37b-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="7c37b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c37b-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="7c37b-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="7c37b-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="7c37b-110">REST API</span><span class="sxs-lookup"><span data-stu-id="7c37b-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="7c37b-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="7c37b-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="7c37b-112">이 문서에서는 Microsoft Visual Studio를 사용하여 Azure Blob 저장소에서 Azure SQL 데이터베이스로 데이터를 복사하는 파이프라인이 있는 데이터 팩터리를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="7c37b-113">Azure Data Factory를 처음 사용하는 경우 이 자습서를 수행하기 전에 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="7c37b-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="7c37b-115">복사 작업은 지원되는 데이터 저장소에서 지원되는 싱크 데이터 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="7c37b-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7c37b-117">이 작업은 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7c37b-118">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="7c37b-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7c37b-120">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="7c37b-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="7c37b-122">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="7c37b-123">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c37b-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c37b-124">Prerequisites</span></span>
1. <span data-ttu-id="7c37b-125">[자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서를 살펴보고 **필수 구성 요소** 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="7c37b-126">데이터 팩터리 인스턴스를 만들려면 구독/리소스 그룹 수준에서 [데이터 팩터리 참여자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="7c37b-127">다음 항목이 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="7c37b-128">Visual Studio 2013 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7c37b-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="7c37b-129">Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="7c37b-130">[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)로 이동하고 **.NET** 섹션에서 **VS 2013** 또는 **VS 2015**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="7c37b-131">Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)용 최신 Azure Data Factory 플러그 인을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="7c37b-132">메뉴에서 **도구** -> **확장 및 업데이트** -> **온라인** -> **Visual Studio 갤러리** -> **Visual Studio용 Microsoft Azure Data Factory 도구** -> **업데이트**를 클릭하여 플러그 인을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="7c37b-133">단계</span><span class="sxs-lookup"><span data-stu-id="7c37b-133">Steps</span></span>
<span data-ttu-id="7c37b-134">이 자습서의 일부로 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="7c37b-135">데이터 팩터리에서 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="7c37b-136">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="7c37b-137">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7c37b-138">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 컨테이너를 만들고 이 저장소 계정에 데이터를 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="7c37b-139">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="7c37b-140">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="7c37b-141">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="7c37b-142">데이터 팩터리에서 입력 및 출력 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="7c37b-143">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="7c37b-144">그리고 입력 Blob 데이터 집합은 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="7c37b-145">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="7c37b-146">그리고 출력 SQL 테이블 데이터 집합은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="7c37b-147">데이터 팩터리에서 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="7c37b-148">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="7c37b-149">복사 활동은 Azure Blob 저장소의 Blob에서 Azure SQL 데이터베이스의 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="7c37b-150">파이프라인의 복사 활동을 사용하여 지원되는 모든 원본의 데이터를 지원되는 모든 대상으로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="7c37b-151">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="7c37b-152">Data Factory 엔터티(연결된 서비스, 데이터 집합/테이블 및 파이프라인)를 배포할 때 Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="7c37b-153">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="7c37b-154">**Visual Studio 2015**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="7c37b-155">**File**을 클릭하고 **New**를 가리킨 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="7c37b-156">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="7c37b-157">**새 프로젝트** 대화 상자에서 **DataFactory** 템플릿을 선택하고 **빈 데이터 팩터리 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![새 프로젝트 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="7c37b-159">프로젝트 이름, 솔루션 위치 및 솔루션 이름을 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![솔루션 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="7c37b-161">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-161">Create linked services</span></span>
<span data-ttu-id="7c37b-162">데이터 팩터리에서 연결된 서비스를 만들어 데이터 저장소를 연결하고 계산 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="7c37b-163">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="7c37b-164">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="7c37b-165">따라서 두 가지 연결된 서비스 유형, 즉 AzureStorage와 AzureSqlDatabase를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="7c37b-166">Azure Storage 연결된 서비스는 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7c37b-167">이 저장소 계정은 컨테이너를 만들고 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 데이터를 업로드한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="7c37b-168">Azure SQL 연결된 서비스는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="7c37b-169">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="7c37b-170">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 emp 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="7c37b-171">연결된 서비스는 데이터 저장소 또는 계산 서비스를 Azure Data Factory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="7c37b-172">복사 작업에서 지원하는 모든 원본 및 싱크는 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="7c37b-173">데이터 팩터리에서 지원하는 계산 서비스 목록은 [연결된 계산 서비스](data-factory-compute-linked-services.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="7c37b-174">이 자습서에서는 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="7c37b-175">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="7c37b-176">**솔루션 탐색기**에서 **연결된 서비스**를 마우스 오른쪽 단추로 클릭하고, **추가**를 가리킨 다음, **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="7c37b-177">**새 항목 추가** 대화 상자의 목록에서 **Azure Storage 연결된 서비스**를 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![새 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="7c37b-179">`<accountname>` 및 `<accountkey>`*를 Azure Storage 계정 이름 및 해당 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Azure 저장소 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="7c37b-181">**AzureStorageLinkedService1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="7c37b-182">연결된 서비스 정의의 JSON 속성에 대한 자세한 내용은 [Azure Blob Storage 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="7c37b-183">Azure SQL 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="7c37b-184">**솔루션 탐색기**에서 다시 **연결된 서비스** 노드를 마우스 오른쪽 단추로 다시 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="7c37b-185">이번에는 **Azure SQL 연결된 서비스**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="7c37b-186">**AzureSqlLinkedService1.json 파일**에서 `<servername>`, `<databasename>`, `<username@servername>` 및 `<password>`를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="7c37b-187">**AzureSqlLinkedService1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="7c37b-188">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="7c37b-189">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-189">Create datasets</span></span>
<span data-ttu-id="7c37b-190">이전 단계에서는 Azure Storage 계정과 Azure SQL Database를 데이터 팩터리에 연결하는 연결된 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="7c37b-191">이 단계에서는 AzureStorageLinkedService1 및 AzureSqlLinkedService1에서 각각 참조하는 데이터 저장소에 저장된 입력 및 출력 데이터를 나타내는 InputDataset 및 OutputDataset이라는 두 개의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="7c37b-192">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="7c37b-193">그리고 입력 Blob 데이터 집합(InputDataset)은 입력 데이터가 포함된 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="7c37b-194">마찬가지로 Azure SQL Database 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure SQL 데이터베이스에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="7c37b-195">그리고 출력 SQL 테이블 데이터 집합(OututDataset)은 Blob 저장소의 데이터가 복사되는 데이터베이스의 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="7c37b-196">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-196">Create input dataset</span></span>
<span data-ttu-id="7c37b-197">이 단계에서는 AzureStorageLinkedService1 연결된 서비스에서 나타내는 Azure Storage의 Blob 컨테이너(adftutorial)의 루트 폴더에 있는 Blob 파일(emp.txt)을 가리키는 InputDataset이라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="7c37b-198">fileName 값을 지정하지 않거나 건너뛰면 입력 폴더에 있는 모든 Blob의 데이터가 대상에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="7c37b-199">이 자습서에서는 fileName 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="7c37b-200">여기서는 "데이터 집합" 대신 "테이블"이라는 용어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="7c37b-201">테이블은 사각형 데이터 집합이며 현재 지원되는 유일한 데이터 집합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="7c37b-202">**솔루션 탐색기**에서 **테이블**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="7c37b-203">**새 항목 추가** 대화 상자에서 **Azure Blob**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="7c37b-204">JSON 텍스트를 다음 텍스트로 바꾸고 **AzureBlobLocation1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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
    <span data-ttu-id="7c37b-205">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="7c37b-206">속성</span><span class="sxs-lookup"><span data-stu-id="7c37b-206">Property</span></span> | <span data-ttu-id="7c37b-207">설명</span><span class="sxs-lookup"><span data-stu-id="7c37b-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7c37b-208">type</span><span class="sxs-lookup"><span data-stu-id="7c37b-208">type</span></span> | <span data-ttu-id="7c37b-209">Azure Blob 저장소에 데이터가 있기 때문에 type 속성은 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="7c37b-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7c37b-210">linkedServiceName</span></span> | <span data-ttu-id="7c37b-211">이전에 만든 **AzureStorageLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7c37b-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="7c37b-212">folderPath</span></span> | <span data-ttu-id="7c37b-213">입력 Blob이 포함된 Blob **컨테이너**와 **폴더**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="7c37b-214">이 자습서에서 adftutorial은 Blob 컨테이너이며, 폴더는 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="7c37b-215">fileName</span><span class="sxs-lookup"><span data-stu-id="7c37b-215">fileName</span></span> | <span data-ttu-id="7c37b-216">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-216">This property is optional.</span></span> <span data-ttu-id="7c37b-217">이 속성을 생략하면 folderPath의 모든 파일이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="7c37b-218">이 자습서에서는 fileName에 대해 **emp.txt**를 지정하므로 해당 파일만 처리를 위해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="7c37b-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="7c37b-219">format -> type</span></span> |<span data-ttu-id="7c37b-220">입력 파일은 텍스트 형식이므로 **TextFormat**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="7c37b-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7c37b-221">columnDelimiter</span></span> | <span data-ttu-id="7c37b-222">입력 파일의 열은 **쉼표(`,`)**로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="7c37b-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7c37b-223">frequency/interval</span></span> | <span data-ttu-id="7c37b-224">frequency는 **Hour**로 설정되고, interval은 **1**로 설정됩니다. 즉 입력 조각이 **매시간** 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="7c37b-225">다시 말하면, Data Factory 서비스가 지정한 Blob 컨테이너(**adftutorial**)의 루트 폴더에서 매 시간마다 입력 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="7c37b-226">이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 내에 있는 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="7c37b-227">external</span><span class="sxs-lookup"><span data-stu-id="7c37b-227">external</span></span> | <span data-ttu-id="7c37b-228">이 파이프라인에 의해 데이터가 생성되지 않는 경우 이 속성은 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="7c37b-229">이 자습서의 입력 데이터는 이 파이프라인에 의해 생성되지 않는 emp.txt 파일에 있으므로 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="7c37b-230">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="7c37b-231">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-231">Create output dataset</span></span>
<span data-ttu-id="7c37b-232">이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="7c37b-233">이 데이터 집합은 **AzureSqlLinkedService1**이 나타내는 Azure SQL Database에서 SQL 테이블을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="7c37b-234">**솔루션 탐색기**에서 다시 **테이블**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="7c37b-235">**새 항목 추가** 대화 상자에서 **Azure SQL**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="7c37b-236">JSON 텍스트를 다음 JSON으로 바꾸고 **AzureSqlTableLocation1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
       "linkedServiceName": "AzureSqlLinkedService1",
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
    <span data-ttu-id="7c37b-237">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="7c37b-238">속성</span><span class="sxs-lookup"><span data-stu-id="7c37b-238">Property</span></span> | <span data-ttu-id="7c37b-239">설명</span><span class="sxs-lookup"><span data-stu-id="7c37b-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7c37b-240">type</span><span class="sxs-lookup"><span data-stu-id="7c37b-240">type</span></span> | <span data-ttu-id="7c37b-241">Azure SQL 데이터베이스의 테이블에 데이터가 복사되기 때문에 type 속성은 **AzureSqlTable**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="7c37b-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7c37b-242">linkedServiceName</span></span> | <span data-ttu-id="7c37b-243">이전에 만든 **AzureSqlLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7c37b-244">tableName</span><span class="sxs-lookup"><span data-stu-id="7c37b-244">tableName</span></span> | <span data-ttu-id="7c37b-245">데이터가 복사되는 **테이블**을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="7c37b-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7c37b-246">frequency/interval</span></span> | <span data-ttu-id="7c37b-247">frequency는 **Hour**로 설정되고, interval은 **1**입니다. 즉 출력 조각이 이러한 시간 이전 또는 이후가 아니라 파이프라인의 시작 시간과 종료 시간 사이에서 **매시간** 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="7c37b-248">데이터베이스의 emp 테이블에 **ID**, **FirstName** 및 **LastName**이라는 세 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="7c37b-249">ID는 ID 열이므로 여기서 **FirstName** 및 **LastName**만 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="7c37b-250">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="7c37b-251">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-251">Create pipeline</span></span>
<span data-ttu-id="7c37b-252">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="7c37b-253">현재 출력 데이터 집합은 일정을 작동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="7c37b-254">이 자습서에서는 출력 데이터 집합이 한 시간에 한 번씩 조각을 생성하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="7c37b-255">이 파이프라인은 하루 24시간 간격, 즉 24시간 동안에 걸친 시작 시간과 종료 시간을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="7c37b-256">따라서 24개의 출력 데이터 집합이 파이프라인에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="7c37b-257">**솔루션 탐색기**에서 **파이프라인**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="7c37b-258">**새 항목 추가** 대화 상자에서 **데이터 파이프라인 복사**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="7c37b-259">JSON을 다음 JSON으로 바꾸고 **CopyActivity1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="7c37b-260">작업 섹션에는 **형식**이 **복사**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="7c37b-261">복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7c37b-262">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="7c37b-263">작업에 대한 입력을 **InputDataset**으로 설정하고 작업에 대한 출력을 **OutputDataset**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="7c37b-264">**typeProperties** 섹션에서 **BlobSource**를 원본 유형으로 지정하고 **SqlSink**를 싱크 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="7c37b-265">복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 전체 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7c37b-266">지원되는 특정 데이터 저장소를 원본/싱크로 사용하는 방법을 알아보려면 표에 나와 있는 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="7c37b-267">**시작** 속성 값을 현재 날짜로 바꾸고 **종료** 값을 다음 날짜로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="7c37b-268">날짜 부분만 지정하고 날짜/시간의 시간 부분은 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="7c37b-269">예를 들어, "2016-02-03"은 "2016-02-03T00:00:00Z"과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="7c37b-270">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="7c37b-271">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="7c37b-272">**종료** 시간은 선택 사항이지만 이 자습서에서는 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="7c37b-273">**종료** 속성 값을 지정하지 않는 경우 "**시작 + 48시간**"으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="7c37b-274">파이프라인을 무기한 실행하려면 **종료** 속성 값으로 **9999-09-09**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="7c37b-275">앞의 예에서는 각 데이터 조각이 1시간마다 생성되므로 24개 데이터 조각이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="7c37b-276">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7c37b-277">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7c37b-278">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="7c37b-279">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="7c37b-280">데이터 팩터리 엔터티 게시/배포</span><span class="sxs-lookup"><span data-stu-id="7c37b-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="7c37b-281">이 단계에서는 이전에 만든 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="7c37b-282">이러한 엔터티를 저장하기 위해 만들어진 새 데이터 팩터리의 이름을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="7c37b-283">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="7c37b-284">**Microsoft 계정에 로그인** 대화 상자가 표시되면 Azure 구독이 있는 계정의 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="7c37b-285">다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-285">You should see the following dialog box:</span></span>
   
   ![게시 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="7c37b-287">데이터 팩터리 구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="7c37b-288">**새 데이터 팩터리 만들기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="7c37b-289">**이름**에 **VSTutorialFactory**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="7c37b-290">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="7c37b-291">게시할 때 데이터 팩터리의 이름에 대한 오류를 받은 경우 데이터 팩터리의 이름(예: yournameVSTutorialFactory)을 변경하고 다시 게시하도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="7c37b-292">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="7c37b-293">**구독** 필드의 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="7c37b-294">모든 구독이 표시되지 않으면 구독의 관리자 또는 공동 관리자인 계정을 사용하여 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="7c37b-295">생성되는 데이터 팩터리의 **리소스 그룹** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="7c37b-296">데이터 팩터리의 **하위 지역** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="7c37b-297">Data Factory 서비스에서 지원하는 지역만 드롭다운 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="7c37b-298">**다음**을 클릭하여 **항목 게시** 페이지로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![데이터 팩터리 페이지 구성](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="7c37b-300">**항목 게시** 페이지에서 모든 데이터 팩터리 엔터티가 선택되었는지 확인하고 **다음**을 클릭하여 **요약** 페이지로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![항목 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="7c37b-302">요약을 검토한 후 **다음**을 클릭하여 배포 프로세스를 시작하고 **배포 상태**를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![요약 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="7c37b-304">**배포 상태** 페이지에 배포 프로세스의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="7c37b-305">배포가 완료되면 마침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-305">Click Finish after the deployment is done.</span></span>
 
   ![배포 상태 페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="7c37b-307">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-307">Note the following points:</span></span> 

* <span data-ttu-id="7c37b-308">“구독이 Microsoft.DataFactory 네임스페이스를 사용하도록 등록되어 있지 않습니다.” 오류를 수신하는 경우 다음 중 하나를 수행하고 다시 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="7c37b-309">Azure PowerShell에서 다음 명령을 실행하여 Data Factory 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="7c37b-310">데이터 팩터리 공급자가 등록되어 있는지 확인하려면 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="7c37b-311">Azure 구독을 사용하여 [Azure 포털](https://portal.azure.com) 에 로그인하고 데이터 팩터리 블레이드로 이동하거나 Azure 포털에 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="7c37b-312">이 작업은 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="7c37b-313">데이터 팩터리의 이름은 나중에 DNS 이름으로 표시되므로 공개적으로 등록될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c37b-314">Data Factory 인스턴스를 만들려면 Azure 구독의 관리자 또는 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="7c37b-315">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="7c37b-315">Monitor pipeline</span></span>
<span data-ttu-id="7c37b-316">데이터 팩터리의 홈 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="7c37b-317">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7c37b-318">왼쪽 메뉴에서 **추가 서비스**를 클릭하고 **데이터 팩터리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![데이터 팩터리 찾아보기](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="7c37b-320">데이터 팩터리의 이름을 입력하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-320">Start typing the name of your data factory.</span></span>

    ![데이터 팩터리의 이름](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="7c37b-322">데이터 팩터리의 홈 페이지를 보려면 결과 목록에서 데이터 팩터리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![데이터 팩터리 홈페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="7c37b-324">이 자습서에서 만든 파이프라인과 데이터 집합을 모니터링하려면 [데이터 집합 및 파이프라인 모니터링](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="7c37b-325">Visual Studio는 현재 Data Factory 파이프라인 모니터링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="7c37b-326">요약</span><span class="sxs-lookup"><span data-stu-id="7c37b-326">Summary</span></span>
<span data-ttu-id="7c37b-327">이 자습서에서는 Azure Blob에서 Azure SQL 데이터베이스로 데이터를 복사하는 Azure Data Factory를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="7c37b-328">Visual Studio를 사용하여 데이터 팩터리, 연결된 서비스, 데이터 집합 및 파이프라인을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="7c37b-329">이 자습서에서 수행한 단계를 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="7c37b-330">Azure **Data Factory**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="7c37b-331">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="7c37b-332">입력 데이터를 보유하는 Azure 저장소 계정을 연결하는 **Azure 저장소** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="7c37b-333">출력 데이터를 보유하는 Azure SQL 데이터베이스를 연결하는 **Azure SQL** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="7c37b-334">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="7c37b-335">원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="7c37b-336">Azure HDInsight 클러스터를 사용하여 HDInsight Hive 활동을 통해 데이터를 변환하는 방법을 알아보려면 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하는 첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="7c37b-337">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정하여 두 활동을 연결하면 해당 활동을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="7c37b-338">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="7c37b-339">서버 탐색기에서 모든 데이터 팩터리 보기</span><span class="sxs-lookup"><span data-stu-id="7c37b-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="7c37b-340">이 섹션에서는 Visual Studio의 [서버 탐색기]를 사용하여 Azure 구독의 모든 데이터 팩터리를 보고 기존 데이터 팩터리에 기반한 Visual Studio 프로젝트를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="7c37b-341">**Visual Studio**의 메뉴에서 **보기**를 클릭한 다음 **서버 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="7c37b-342">서버 탐색기 창에서 **Azure**를 확장한 다음 **Data Factory**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="7c37b-343">**Visual Studio에 로그인**이 표시되면 Azure 구독과 연결된 **계정**을 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="7c37b-344">**암호**를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="7c37b-345">Visual Studio에서는 구독에 있는 모든 Azure Data Factory에 대한 정보를 가져오려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="7c37b-346">**데이터 팩터리 작업 목록** 창에 이 작업의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![서버 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="7c37b-348">기존 데이터 팩터리에 대한 Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7c37b-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="7c37b-349">서버 탐색기에서 데이터 팩터리를 마우스 오른쪽 단추로 클릭하고 **새 프로젝트로 데이터 팩터리 내보내기**를 선택하여 기존 데이터 팩터리에 기반한 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![VS 프로젝트로 데이터 팩터리 내보내기](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="7c37b-351">Visual Studio용 데이터 팩터리 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c37b-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="7c37b-352">Visual Studio용 Azure Data Factory 도구를 업데이트하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="7c37b-353">메뉴에서 **도구**를 클릭하고 **확장 및 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="7c37b-354">왼쪽 창에서 **업데이트**를 선택한 다음 **Visual Studio 갤러리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="7c37b-355">**Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="7c37b-356">이 항목이 표시되지 않으면 이미 최신 버전의 도구가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="7c37b-357">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="7c37b-357">Use configuration files</span></span>
<span data-ttu-id="7c37b-358">각 환경마다 다르게 연결된 서비스/테이블/파이프라인에 대한 속성을 구성하기 위해 Visual Studio의 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="7c37b-359">Azure 저장소 연결 서비스에 대한 다음 JSON 정의를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="7c37b-360">데이터 팩터리 엔터티를 배포하는 환경(개발/테스트/프로덕션)에 따라 서로 다른 accountname 및 accountkey에 대한 값으로 **connectionString**을 지정하려면</span><span class="sxs-lookup"><span data-stu-id="7c37b-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="7c37b-361">각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="7c37b-362">구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="7c37b-362">Add a configuration file</span></span>
<span data-ttu-id="7c37b-363">다음 단계를 수행하여 각 환경에 대한 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="7c37b-364">Visual Studio 솔루션의 데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="7c37b-365">왼쪽에 있는 설치된 템플릿 목록에서 **구성**을 선택하고 **구성 파일**을 선택한 다음, 구성 파일의 **이름**을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="7c37b-367">다음 형식으로 구성 매개 변수와 해당 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-367">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="7c37b-368">이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="7c37b-369">이름을 지정하는 구문은 [JsonPath](http://goessner.net/articles/JsonPath/)입니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="7c37b-370">JSON에 다음 코드와 같은 값의 배열을 가진 속성이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="7c37b-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="7c37b-371">다음 구성 파일(0부터 시작되는 인덱스 사용)과 같은 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="7c37b-372">공백이 포함된 속성 이름</span><span class="sxs-lookup"><span data-stu-id="7c37b-372">Property names with spaces</span></span>
<span data-ttu-id="7c37b-373">속성 이름에 공백이 있으면 다음 예제(데이터베이스 서버 이름)와 같이 대괄호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="7c37b-374">구성을 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="7c37b-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="7c37b-375">VS에서 Azure 데이터 팩터리 엔터티를 게시하는 경우 해당 게시 작업에 사용하려는 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="7c37b-376">구성 파일을 사용하여 Azure 데이터 팩터리 프로젝트에서 엔터티를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="7c37b-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="7c37b-377">Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭하여 **게시 항목** 대화 상자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="7c37b-378">기존 데이터 팩터리를 선택하거나 **데이터 팩터리 구성** 페이지에서 데이터 팩터리를 만드는 값을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="7c37b-379">**항목 게시** 페이지에서 **배포 구성 선택** 필드에 사용 가능한 구성이 있는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="7c37b-381">사용하려는 **구성 파일**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="7c37b-382">**요약** 페이지에서 JSON 파일의 이름이 표시되는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="7c37b-383">배포 작업이 완료되면 **마침** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="7c37b-384">배포할 때 구성 파일의 값은 엔터티가 Azure Data Factory 서비스에 배포되기 전에 JSON 파일에서 속성 값을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="7c37b-385">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="7c37b-385">Use Azure Key Vault</span></span>
<span data-ttu-id="7c37b-386">연결 문자열과 같은 중요한 데이터를 코드 리포지토리에 커밋하는 것은 보안 정책에 위배되는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="7c37b-387">Azure Key Vault에 중요 정보를 저장하고 Data Factory 엔터티를 게시하면서 사용하는 방법에 대한 자세한 내용은 GitHub의 [ADF 보안 게시](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)(영문) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="7c37b-388">Visual Studio에 대한 보안 게시 확장을 통해 비밀이 Key Vault에 저장되도록 하고 이에 대한 참조만 연결된 서비스/배포 구성에 지정하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="7c37b-389">이러한 참조는 Data Factory 엔터티를 Azure에 게시할 때 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="7c37b-390">그런 다음 이러한 파일을 비밀을 노출하지 않고 원본 리포지토리에 커밋할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7c37b-391">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c37b-391">Next steps</span></span>
<span data-ttu-id="7c37b-392">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="7c37b-393">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c37b-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="7c37b-394">데이터 저장소간에 데이터를 복사하는 방법에 대해 알아보려면 테이블에서 데이터 저장소에 대한 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="7c37b-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>