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
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="56940-103">자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56940-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="56940-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="56940-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="56940-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="56940-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="56940-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="56940-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="56940-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="56940-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56940-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="56940-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="56940-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="56940-110">REST API</span><span class="sxs-lookup"><span data-stu-id="56940-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="56940-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="56940-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="56940-112">이 문서에서는 어떻게 toouse hello Microsoft Visual Studio toocreate Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인으로 데이터 팩터리 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="56940-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="56940-113">새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="56940-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="56940-115">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="56940-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="56940-117">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="56940-118">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="56940-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="56940-120">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="56940-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="56940-122">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="56940-123">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56940-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="56940-124">Prerequisites</span></span>
1. <span data-ttu-id="56940-125">자세히 읽고 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="56940-126">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="56940-127">Hello 다음이 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="56940-128">Visual Studio 2013 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="56940-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="56940-129">Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="56940-130">너무 이동[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/) 클릭 **VS 2013** 또는 **VS 2015** hello에 **.NET** 섹션.</span><span class="sxs-lookup"><span data-stu-id="56940-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="56940-131">Visual Studio에 대 한 hello 최신 Azure Data Factory 플러그 인을 다운로드: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="56940-132">Hello 다음 단계를 수행 하 여 hello 플러그 인을 업데이트할 수도 있습니다: hello 메뉴를 클릭 **도구** -> **확장명 및 업데이트** -> **온라인**  ->  **Visual Studio 갤러리** -> **Visual Studio 용 Microsoft Azure 데이터 팩터리 도구** -> **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="56940-133">단계</span><span class="sxs-lookup"><span data-stu-id="56940-133">Steps</span></span>
<span data-ttu-id="56940-134">이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="56940-135">만들 **연결 된 서비스** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="56940-136">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="56940-137">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="56940-138">컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="56940-139">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="56940-140">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="56940-141">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="56940-142">입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="56940-143">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="56940-144">고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="56940-145">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="56940-146">고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="56940-147">만들기는 **파이프라인** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="56940-148">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="56940-149">hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="56940-150">모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="56940-151">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="56940-152">Data Factory 엔터티(연결된 서비스, 데이터 집합/테이블 및 파이프라인)를 배포할 때 Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="56940-153">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="56940-154">**Visual Studio 2015**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="56940-155">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="56940-156">Hello 표시 되어야 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="56940-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="56940-157">Hello에 **새 프로젝트** 대화 상자에서 선택 hello **DataFactory** 템플릿과 클릭 **빈 데이터 팩터리 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![새 프로젝트 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="56940-159">Hello 이름 hello 프로젝트, hello 솔루션에 대 한 위치 및 hello 솔루션의 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![솔루션 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="56940-161">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-161">Create linked services</span></span>
<span data-ttu-id="56940-162">데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="56940-163">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="56940-164">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="56940-165">따라서 두 가지 연결된 서비스 유형, 즉 AzureStorage와 AzureSqlDatabase를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="56940-166">hello Azure 저장소는 Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="56940-167">이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="56940-168">Azure SQL Azure SQL 데이터베이스 toohello 데이터 팩터리 서비스 링크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="56940-169">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="56940-170">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="56940-171">연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="56940-172">참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="56940-173">참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="56940-174">이 자습서에서는 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="56940-175">Hello Azure 저장소 연결 된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="56940-176">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **연결 된 서비스**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="56940-177">Hello에 **새 항목 추가** 대화 상자에서 **Azure 저장소 연결 된 서비스** hello 목록 및 클릭에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![새 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="56940-179">대체 `<accountname>` 및 `<accountkey>`* Azure 저장소 계정 및 키의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Azure 저장소 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="56940-181">Hello 저장 **AzureStorageLinkedService1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="56940-182">연결 된 hello 서비스 정의에 JSON 속성에 대 한 자세한 내용은 참조 [Azure Blob 저장소 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서.</span><span class="sxs-lookup"><span data-stu-id="56940-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="56940-183">Hello Azure SQL 연결 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="56940-184">마우스 오른쪽 단추로 클릭 **연결 된 서비스** hello에 대 한 노드 **솔루션 탐색기** 다시 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="56940-185">이번에는 **Azure SQL 연결된 서비스**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="56940-186">Hello에 **AzureSqlLinkedService1.json 파일**, 대체 `<servername>`, `<databasename>`, `<username@servername>`, 및 `<password>` Azure SQL server, 데이터베이스, 사용자 계정 및 암호의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="56940-187">Hello 저장 **AzureSqlLinkedService1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="56940-188">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="56940-189">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-189">Create datasets</span></span>
<span data-ttu-id="56940-190">Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="56940-191">이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService1 및 AzureSqlLinkedService1에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="56940-192">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="56940-193">고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="56940-194">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="56940-195">및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="56940-196">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-196">Create input dataset</span></span>
<span data-ttu-id="56940-197">이 단계에서는 hello hello AzureStorageLinkedService1 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="56940-198">하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="56940-199">이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="56940-200">여기에서 "데이터 집합" 아닌 hello 용어 "tables"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="56940-201">사각형 데이터 집합은 테이블과 현재 지원 되는 데이터 집합의 hello만 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="56940-202">마우스 오른쪽 단추로 클릭 **테이블** hello에 **솔루션 탐색기**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="56940-203">Hello에 **새 항목 추가** 대화 상자에서 **Azure Blob**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="56940-204">텍스트 다음 hello로 hello JSON 텍스트를 바꾸고 hello 저장 **AzureBlobLocation1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="56940-205">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="56940-206">속성</span><span class="sxs-lookup"><span data-stu-id="56940-206">Property</span></span> | <span data-ttu-id="56940-207">설명</span><span class="sxs-lookup"><span data-stu-id="56940-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="56940-208">type</span><span class="sxs-lookup"><span data-stu-id="56940-208">type</span></span> | <span data-ttu-id="56940-209">hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="56940-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="56940-210">linkedServiceName</span></span> | <span data-ttu-id="56940-211">Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="56940-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="56940-212">folderPath</span></span> | <span data-ttu-id="56940-213">Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="56940-214">이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="56940-215">fileName</span><span class="sxs-lookup"><span data-stu-id="56940-215">fileName</span></span> | <span data-ttu-id="56940-216">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-216">This property is optional.</span></span> <span data-ttu-id="56940-217">이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="56940-218">이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="56940-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="56940-219">format -> type</span></span> |<span data-ttu-id="56940-220">사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="56940-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="56940-221">columnDelimiter</span></span> | <span data-ttu-id="56940-222">hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="56940-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="56940-223">frequency/interval</span></span> | <span data-ttu-id="56940-224">hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="56940-225">즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="56940-226">Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="56940-227">external</span><span class="sxs-lookup"><span data-stu-id="56940-227">external</span></span> | <span data-ttu-id="56940-228">이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="56940-229">이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="56940-230">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="56940-231">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-231">Create output dataset</span></span>
<span data-ttu-id="56940-232">이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="56940-233">이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService1**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="56940-234">마우스 오른쪽 단추로 클릭 **테이블** hello에 **솔루션 탐색기** 다시 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="56940-235">Hello에 **새 항목 추가** 대화 상자에서 **Azure SQL**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="56940-236">다음 JSON hello로 hello JSON 텍스트를 바꾸고 hello 저장 **AzureSqlTableLocation1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="56940-237">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="56940-238">속성</span><span class="sxs-lookup"><span data-stu-id="56940-238">Property</span></span> | <span data-ttu-id="56940-239">설명</span><span class="sxs-lookup"><span data-stu-id="56940-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="56940-240">type</span><span class="sxs-lookup"><span data-stu-id="56940-240">type</span></span> | <span data-ttu-id="56940-241">hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="56940-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="56940-242">linkedServiceName</span></span> | <span data-ttu-id="56940-243">Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="56940-244">tableName</span><span class="sxs-lookup"><span data-stu-id="56940-244">tableName</span></span> | <span data-ttu-id="56940-245">지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="56940-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="56940-246">frequency/interval</span></span> | <span data-ttu-id="56940-247">hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.</span><span class="sxs-lookup"><span data-stu-id="56940-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="56940-248">세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="56940-249">Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="56940-250">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="56940-251">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-251">Create pipeline</span></span>
<span data-ttu-id="56940-252">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="56940-253">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="56940-254">이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="56940-255">hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="56940-256">따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="56940-257">마우스 오른쪽 단추로 클릭 **파이프라인** hello에 **솔루션 탐색기**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="56940-258">선택 **복사본 데이터 파이프라인** hello에 **새 항목 추가** 대화 상자와 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="56940-259">다음 JSON hello hello JSON 바꾸고 hello 저장 **CopyActivity1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

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
    - <span data-ttu-id="56940-260">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="56940-261">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="56940-262">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="56940-263">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="56940-264">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="56940-265">원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="56940-266">소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="56940-267">Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="56940-268">Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="56940-269">예를 들어 "2016-02-03", 즉 너무 "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="56940-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="56940-270">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="56940-271">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="56940-272">hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="56940-273">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="56940-274">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="56940-275">앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="56940-276">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="56940-277">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="56940-278">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="56940-279">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="56940-280">데이터 팩터리 엔터티 게시/배포</span><span class="sxs-lookup"><span data-stu-id="56940-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="56940-281">이 단계에서는 이전에 만든 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="56940-282">또한 이러한 엔터티 toohold 만든 hello 새 데이터 팩터리 toobe의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="56940-283">Hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="56940-284">표시 되 면 **tooyour Microsoft 계정 로그인** 대화 상자에서 Azure 구독이 있는 hello 계정에 대 한 자격 증명을 입력 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="56940-285">대화 상자를 수행 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-285">You should see hello following dialog box:</span></span>
   
   ![게시 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="56940-287">Hello 구성 데이터 팩터리 페이지에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="56940-288">**새 데이터 팩터리 만들기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="56940-289">**이름**에 **VSTutorialFactory**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="56940-290">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="56940-291">게시 하는 경우 데이터 팩터리의 이름 hello에 대 한 오류가 나타나면 hello 이름 (예를 들어 yournameVSTutorialFactory) hello 데이터 팩터리 및 다시 게시 시도 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="56940-292">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="56940-293">Hello에 대 한 Azure 구독 선택 **구독** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="56940-294">모든 구독을 표시 되지 않으면 관리자 또는 hello 구독 공동 관리자 인 계정을 사용 하 여 로그인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="56940-295">선택 hello **리소스 그룹** hello 데이터 팩터리 toobe 생성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="56940-296">선택 hello **지역** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="56940-297">Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="56940-298">클릭 **다음** tooswitch toohello **게시 항목** 페이지.</span><span class="sxs-lookup"><span data-stu-id="56940-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![데이터 팩터리 페이지 구성](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="56940-300">Hello에 **게시 항목** 페이지에서 엔터티를 선택 하 고 클릭 하 여 데이터 팩터리를 hello 모든 **다음** tooswitch toohello **요약** 페이지.</span><span class="sxs-lookup"><span data-stu-id="56940-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![항목 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="56940-302">Hello 요약을 검토 하 고 클릭 **다음** toostart hello 배포 프로세스와 보기 hello **배포 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![요약 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="56940-304">Hello에 **배포 상태** 페이지 hello 배포 프로세스의 hello 상태 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="56940-305">Hello 배포를 완료 한 후 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-305">Click Finish after hello deployment is done.</span></span>
 
   ![배포 상태 페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="56940-307">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="56940-307">Note hello following points:</span></span> 

* <span data-ttu-id="56940-308">Hello 오류가 나타나면: "이이 등록은 등록된 toouse 네임 스페이스가 microsoft.datafactory가 아닙니다" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="56940-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="56940-309">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="56940-310">데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="56940-311">Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56940-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="56940-312">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="56940-313">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56940-314">관리자/공동 관리자의 Azure 구독 hello toobe 해야 toocreate 데이터 팩터리 인스턴스</span><span class="sxs-lookup"><span data-stu-id="56940-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="56940-315">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="56940-315">Monitor pipeline</span></span>
<span data-ttu-id="56940-316">데이터 팩토리에 대 한 toohello 홈 페이지를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="56940-317">로그 너무[Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="56940-318">클릭 **더 많은 서비스** 왼쪽된 메뉴 hello 되 고 클릭 **데이터 팩터리**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![데이터 팩터리 찾아보기](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="56940-320">데이터 팩터리의 hello 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-320">Start typing hello name of your data factory.</span></span>

    ![데이터 팩터리의 이름](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="56940-322">데이터 팩터리 hello 결과 목록 toosee hello 홈 페이지에서 데이터 팩터리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![데이터 팩터리 홈페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="56940-324">지침에 따라 [모니터링 데이터 집합 및 파이프라인](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) 이 자습서에서 만든 toomonitor hello 파이프라인 및 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="56940-325">Visual Studio는 현재 Data Factory 파이프라인 모니터링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="56940-326">요약</span><span class="sxs-lookup"><span data-stu-id="56940-326">Summary</span></span>
<span data-ttu-id="56940-327">이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="56940-328">Visual Studio toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="56940-329">이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="56940-330">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="56940-331">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="56940-332">**Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하 여 Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="56940-333">**Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="56940-334">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="56940-335">원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="56940-336">toouse Azure HDInsight 클러스터를 사용 하 여 HDInsight Hive 활동 tootransform 데이터를 확인 하려면 어떻게 toosee [ 자습서: Hadoop 클러스터를 사용 하 여 첫 번째 파이프라인 tootransform 데이터 빌드](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="56940-337">Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="56940-338">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56940-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="56940-339">서버 탐색기에서 모든 데이터 팩터리 보기</span><span class="sxs-lookup"><span data-stu-id="56940-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="56940-340">이 섹션에서는 toouse 모든 hello 데이터 팩터리에 Azure 구독에서 서버 탐색기에서 Visual Studio tooview hello 및 기존 데이터 팩토리를 기반으로 Visual Studio 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="56940-341">**Visual Studio**, 클릭 **보기** 메뉴 hello 되 고 클릭 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="56940-342">Hello 서버 탐색기 창에서 확장 **Azure** 확장 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="56940-343">표시 되 면 **tooVisual Studio에에서 로그인**, hello 입력 **계정** 연결 된 Azure 구독 및 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="56940-344">**암호**를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="56940-345">Visual Studio에는 구독에서 모든 Azure 데이터 팩토리에 대 한 정보 tooget 하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="56940-346">Hello에이 작업의 hello 상태를 확인할 **데이터 팩터리에 작업 목록** 창.</span><span class="sxs-lookup"><span data-stu-id="56940-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![서버 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="56940-348">기존 데이터 팩터리에 대한 Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="56940-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="56940-349">서버 탐색기에서 데이터 팩터리를 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 팩터리의 내보내기 tooNew 프로젝트** toocreate 기존 데이터 팩토리를 기반으로 한 Visual Studio 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![데이터 팩터리 tooa VS 프로젝트 내보내기](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="56940-351">Visual Studio용 데이터 팩터리 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="56940-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="56940-352">Visual Studio 용 Azure Data Factory 도구 tooupdate 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="56940-353">클릭 **도구** hello 메뉴를 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="56940-354">선택 **업데이트** 에 왼쪽된 창의 hello 선택한 후 **Visual Studio 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="56940-355">**Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="56940-356">이 항목을 표시 되지 않으면 최신 버전의 hello 도구 hello이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="56940-357">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="56940-357">Use configuration files</span></span>
<span data-ttu-id="56940-358">연결 된 서비스/테이블/파이프라인 각 환경에 대해 다른 방식에 대 한 Visual Studio tooconfigure 속성에서 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="56940-359">다음은 Azure 저장소 연결 서비스에 대 한 JSON 정의 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="56940-360">toospecify **connectionString** accountname 및 accountkey hello (프로덕션/개발/테스트) 환경 toowhich 기준에 대 한 값이 서로 다른 배포 하는 데이터 팩터리 엔터티.</span><span class="sxs-lookup"><span data-stu-id="56940-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="56940-361">각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="56940-362">구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="56940-362">Add a configuration file</span></span>
<span data-ttu-id="56940-363">Hello 다음 단계를 수행 하 여 각 환경에 대 한 구성 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="56940-364">Visual Studio 솔루션의 hello Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="56940-365">선택 **Config** hello hello 왼쪽에 설치 된 템플릿 목록에서 선택 **구성 파일**를 입력 한 **이름** hello 구성에 대 한 파일을 찾아 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="56940-367">형식에 따라 hello에 구성 매개 변수 및 해당 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="56940-368">이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="56940-369">Hello 구문 이름을 지정 하는 [JsonPath](http://goessner.net/articles/JsonPath/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="56940-370">JSON에 hello 코드 다음에 나와 있는 값의 배열을 포함 하는 속성:</span><span class="sxs-lookup"><span data-stu-id="56940-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="56940-371">다음 구성 파일 (사용 하 여 인덱스가 0부터 시작) hello에 표시 된 대로 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="56940-372">공백이 포함된 속성 이름</span><span class="sxs-lookup"><span data-stu-id="56940-372">Property names with spaces</span></span>
<span data-ttu-id="56940-373">속성 이름에 공백이 있으면, 다음 예제 (데이터베이스 서버 이름) hello와 같이 대괄호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="56940-374">구성을 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="56940-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="56940-375">Azure Data Factory 엔터티에 VS에서 게시 하는 hello 원하는 구성으로 toouse 해당 게시 작업에 대해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="56940-376">구성 파일을 사용 하 여 Azure Data Factory 프로젝트에서 toopublish 엔터티:</span><span class="sxs-lookup"><span data-stu-id="56940-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="56940-377">데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시** toosee hello **게시 항목** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="56940-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="56940-378">기존 데이터 팩토리를 선택 하거나 hello에 데이터 팩터리 만들기에 대 한 값을 지정할 **구성 데이터 팩터리의** 페이지를 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="56940-379">Hello에 **게시 항목** 페이지: hello에 대 한 사용 가능한 구성으로 드롭 다운 목록을 보려면 **배포 구성 선택** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="56940-381">선택 hello **구성 파일** 있는지 toouse 선택한 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="56940-382">Hello에 대 한 JSON 파일의 hello 이름 표시 되는지 확인 **요약** 페이지 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="56940-383">클릭 **마침** hello 배포 작업이 완료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="56940-384">를 배포할 때 hello 구성 파일에서 hello 값은 hello 엔터티는 배포 된 tooAzure 데이터 팩터리 서비스 전에 hello JSON 파일의 속성에 대 한 tooset 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="56940-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="56940-385">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="56940-385">Use Azure Key Vault</span></span>
<span data-ttu-id="56940-386">권장 및 종종 연결 문자열 toohello 코드 저장소와 같은 보안 정책 toocommit 중요 한 데이터에 대 한 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="56940-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="56940-387">참조 [ADF 게시 Secure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure 키 자격 증명 모음에 중요 한 정보를 저장 하 고 사용 하 여 데이터 팩터리 엔터티를 게시 하는 동안에 대 한 GitHub toolearn 샘플.</span><span class="sxs-lookup"><span data-stu-id="56940-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="56940-388">Visual Studio 용 확장명 게시 Secure hello hello 비밀 toobe 주요 자격 증명 모음에 저장 된 있으며 참조 toothem만 연결 된 서비스에 지정 된 / 배포 구성.</span><span class="sxs-lookup"><span data-stu-id="56940-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="56940-389">Data Factory 엔터티에 tooAzure를 게시 하는 경우 이러한 참조는 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56940-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="56940-390">이러한 파일 비밀이 노출 하지 않고 커밋된 toosource 리포지토리 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="56940-391">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56940-391">Next steps</span></span>
<span data-ttu-id="56940-392">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="56940-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="56940-393">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="56940-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="56940-394">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="56940-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
