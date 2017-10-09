---
title: "자습서: Azure 데이터 팩터리 파이프라인 toocopy 데이터 (Azure 포털) 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure blob 저장소 tooan Azure SQL 데이터베이스의 복사 작업 toocopy 데이터로 Azure 포털 toocreate Azure 데이터 팩터리 파이프라인을 사용합니다."
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
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="7baf2-103">자습서:를 사용 하 여 Azure 포털 toocreate 데이터 팩터리 파이프라인 toocopy 데이터</span><span class="sxs-lookup"><span data-stu-id="7baf2-103">Tutorial: Use Azure portal toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7baf2-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7baf2-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="7baf2-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="7baf2-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="7baf2-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7baf2-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="7baf2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7baf2-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="7baf2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7baf2-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="7baf2-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="7baf2-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="7baf2-110">REST API</span><span class="sxs-lookup"><span data-stu-id="7baf2-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="7baf2-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="7baf2-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="7baf2-112">이 문서에서는 설명 어떻게 toouse [Azure 포털](https://portal.azure.com) toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-112">In this article, you learn how toouse [Azure portal](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="7baf2-113">새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="7baf2-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="7baf2-115">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="7baf2-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7baf2-117">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7baf2-118">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="7baf2-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7baf2-120">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="7baf2-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="7baf2-122">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="7baf2-123">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7baf2-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7baf2-124">Prerequisites</span></span>
<span data-ttu-id="7baf2-125">Hello에 나온 필수 조건을 완료 [자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-125">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="7baf2-126">단계</span><span class="sxs-lookup"><span data-stu-id="7baf2-126">Steps</span></span>
<span data-ttu-id="7baf2-127">이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-127">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="7baf2-128">Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-128">Create an Azure **data factory**.</span></span> <span data-ttu-id="7baf2-129">이 단계에서는 ADFTutorialDataFactory라는 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-129">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="7baf2-130">만들 **연결 된 서비스** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-130">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="7baf2-131">이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-131">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="7baf2-132">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-132">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="7baf2-133">컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-133">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="7baf2-134">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-134">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="7baf2-135">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-135">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="7baf2-136">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-136">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="7baf2-137">입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-137">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="7baf2-138">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-138">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7baf2-139">고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-139">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="7baf2-140">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-140">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7baf2-141">고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-141">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="7baf2-142">만들기는 **파이프라인** hello data factory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-142">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="7baf2-143">이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-143">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="7baf2-144">hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-144">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="7baf2-145">모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-145">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="7baf2-146">지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-146">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="7baf2-147">모니터 hello 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-147">Monitor hello pipeline.</span></span> <span data-ttu-id="7baf2-148">이 단계에서는 있습니다 **모니터** Azure 포털을 사용 하 여 입력 및 출력 데이터 집합의 조각을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-148">In this step, you **monitor** hello slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="7baf2-149">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-149">Create data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7baf2-150">전체 [hello 자습서에 대 한 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7baf2-150">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="7baf2-151">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-151">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="7baf2-152">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-152">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="7baf2-153">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-153">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="7baf2-154">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-154">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="7baf2-155">Toohello 로그인 한 후 [Azure 포털](https://portal.azure.com/), 클릭 **새로** hello 왼쪽된 메뉴를 클릭 **데이터 + 분석**를 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-155">After logging in toohello [Azure portal](https://portal.azure.com/), click **New** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="7baf2-157">Hello에 **새 데이터 팩터리** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="7baf2-157">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="7baf2-158">입력 **ADFTutorialDataFactory** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-158">Enter **ADFTutorialDataFactory** for hello **name**.</span></span> 
      
         ![새 데이터 팩터리 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="7baf2-160">hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-160">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="7baf2-161">Hello 다음 오류가 표시 되 면 (예를 들어 yournameADFTutorialDataFactory) hello data factory와 다시 만들어 보십시오.의 hello 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-161">If you receive hello following error, change hello name of hello data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="7baf2-162">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-162">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="7baf2-164">Azure 선택 **구독** toocreate hello 데이터 팩터리 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-164">Select your Azure **subscription** in which you want toocreate hello data factory.</span></span> 
   3. <span data-ttu-id="7baf2-165">Hello에 대 한 **리소스 그룹**, hello 다음 단계 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-165">For hello **Resource Group**, do one of hello following steps:</span></span>
      
      - <span data-ttu-id="7baf2-166">선택 **기존 항목 사용**, hello 드롭 다운 목록에서 기존 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-166">Select **Use existing**, and select an existing resource group from hello drop-down list.</span></span> 
      - <span data-ttu-id="7baf2-167">선택 **새로 만들기**, 리소스 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-167">Select **Create new**, and enter hello name of a resource group.</span></span>   
         
          <span data-ttu-id="7baf2-168">이 자습서에서는 hello 단계 중 일부를 가정 hello 이름을 사용 합니다: **ADFTutorialResourceGroup** hello 리소스 그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-168">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="7baf2-169">리소스 그룹에 대 한 toolearn 참조 [toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-169">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="7baf2-170">선택 hello **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-170">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="7baf2-171">Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-171">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   5. <span data-ttu-id="7baf2-172">선택 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-172">Select **Pin toodashboard**.</span></span>     
   6. <span data-ttu-id="7baf2-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-173">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="7baf2-174">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-174">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
      > 
      > <span data-ttu-id="7baf2-175">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-175">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>                
      > 
      > 
3. <span data-ttu-id="7baf2-176">표시 상태와 함께 바둑판식으로 배열 하는 hello 다음 hello 대시보드에서: **배포 데이터 팩터리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-176">On hello dashboard, you see hello following tile with status: **Deploying data factory**.</span></span> 

    ![데이터 팩터리 배포 중 타일](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="7baf2-178">Hello 참조 hello 만들기가 완료 되 면 **Data Factory** 블레이드 hello 이미지에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-178">After hello creation is complete, you see hello **Data Factory** blade as shown in hello image.</span></span>
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="7baf2-180">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-180">Create linked services</span></span>
<span data-ttu-id="7baf2-181">데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-181">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="7baf2-182">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-182">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="7baf2-183">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-183">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="7baf2-184">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-184">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="7baf2-185">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-185">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="7baf2-186">이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-186">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="7baf2-187">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-187">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="7baf2-188">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-188">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="7baf2-189">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-189">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="7baf2-190">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-190">Create Azure Storage linked service</span></span>
<span data-ttu-id="7baf2-191">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-191">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="7baf2-192">이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-192">You specify hello name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="7baf2-193">Hello에 **Data Factory** 블레이드에서 클릭 **작성자 및 배포** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-193">In hello **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![작성 및 배포 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="7baf2-195">Hello 참조 **데이터 팩터리 편집기** hello 다음 이미지와 같이:</span><span class="sxs-lookup"><span data-stu-id="7baf2-195">You see hello **Data Factory Editor** as shown in hello following image:</span></span> 

    ![데이터 팩터리 편집기](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="7baf2-197">Hello 편집기 클릭 **새 데이터 저장소** hello 도구 모음을 선택 하는 단추 **Azure 저장소** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-197">In hello editor, click **New data store** button on hello toolbar and select **Azure storage** from hello drop-down menu.</span></span> <span data-ttu-id="7baf2-198">Hello 오른쪽 창에서 Azure 저장소 연결 서비스를 만들기 위한 hello JSON 템플릿이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-198">You should see hello JSON template for creating an Azure storage linked service in hello right pane.</span></span> 
   
    ![편집기 새 데이터 저장소 단추](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="7baf2-200">대체 `<accountname>` 및 `<accountkey>` hello 계정 이름 및 계정 키 값을 가진 Azure 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-200">Replace `<accountname>` and `<accountkey>` with hello account name and account key values for your Azure storage account.</span></span> 
   
    ![편집기 Blob 저장소 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="7baf2-202">클릭 **배포** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-202">Click **Deploy** on hello toolbar.</span></span> <span data-ttu-id="7baf2-203">배포 된 hello 표시 되어야 **AzureStorageLinkedService** hello 트리에 지금를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-203">You should see hello deployed **AzureStorageLinkedService** in hello tree view now.</span></span> 
   
    ![편집기 Blob 저장소 배포](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="7baf2-205">연결 된 hello 서비스 정의에 JSON 속성에 대 한 자세한 내용은 참조 [Azure Blob 저장소 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서.</span><span class="sxs-lookup"><span data-stu-id="7baf2-205">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a><span data-ttu-id="7baf2-206">Hello Azure SQL 데이터베이스에 대 한 연결 된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-206">Create a linked service for hello Azure SQL Database</span></span>
<span data-ttu-id="7baf2-207">이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-207">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="7baf2-208">이 섹션의 hello Azure SQL server 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-208">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="7baf2-209">Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** hello 도구 모음을 선택 하는 단추 **Azure SQL 데이터베이스** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-209">In hello **Data Factory Editor**, click **New data store** button on hello toolbar and select **Azure SQL Database** from hello drop-down menu.</span></span> <span data-ttu-id="7baf2-210">Hello 오른쪽 창에 hello Azure SQL 연결 서비스를 만들기 위한 hello JSON 템플릿이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-210">You should see hello JSON template for creating hello Azure SQL linked service in hello right pane.</span></span>
2. <span data-ttu-id="7baf2-211">`<servername>`, `<databasename>`, `<username>@<servername>` 및 `<password>`를 Azure SQL Server의 이름, 사용자 계정 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-211">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="7baf2-212">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **AzureSqlLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-212">Click **Deploy** on hello toolbar toocreate and deploy hello **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="7baf2-213">표시 되는지 확인 **AzureSqlLinkedService** 아래 hello 트리 보기에서 **연결 된 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-213">Confirm that you see **AzureSqlLinkedService** in hello tree view under **Linked services**.</span></span>  

    <span data-ttu-id="7baf2-214">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-214">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="7baf2-215">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-215">Create datasets</span></span>
<span data-ttu-id="7baf2-216">Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-216">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="7baf2-217">이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-217">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="7baf2-218">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-218">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7baf2-219">고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-219">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="7baf2-220">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-220">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7baf2-221">및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-221">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="7baf2-222">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-222">Create input dataset</span></span>
<span data-ttu-id="7baf2-223">이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-223">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="7baf2-224">하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-224">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="7baf2-225">이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-225">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="7baf2-226">Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 더 많은**, 클릭 **새 데이터 집합**를 클릭 하 고 **Azure Blob 저장소** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-226">In hello **Editor** for hello Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from hello drop-down menu.</span></span> 
   
    ![새 데이터 집합 메뉴](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="7baf2-228">JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-228">Replace JSON in hello right pane with hello following JSON snippet:</span></span> 
   
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

    <span data-ttu-id="7baf2-229">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-229">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="7baf2-230">속성</span><span class="sxs-lookup"><span data-stu-id="7baf2-230">Property</span></span> | <span data-ttu-id="7baf2-231">설명</span><span class="sxs-lookup"><span data-stu-id="7baf2-231">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7baf2-232">type</span><span class="sxs-lookup"><span data-stu-id="7baf2-232">type</span></span> | <span data-ttu-id="7baf2-233">hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-233">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="7baf2-234">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7baf2-234">linkedServiceName</span></span> | <span data-ttu-id="7baf2-235">Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-235">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7baf2-236">folderPath</span><span class="sxs-lookup"><span data-stu-id="7baf2-236">folderPath</span></span> | <span data-ttu-id="7baf2-237">Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-237">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="7baf2-238">이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-238">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="7baf2-239">fileName</span><span class="sxs-lookup"><span data-stu-id="7baf2-239">fileName</span></span> | <span data-ttu-id="7baf2-240">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-240">This property is optional.</span></span> <span data-ttu-id="7baf2-241">이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-241">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="7baf2-242">이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-242">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="7baf2-243">format -> type</span><span class="sxs-lookup"><span data-stu-id="7baf2-243">format -> type</span></span> |<span data-ttu-id="7baf2-244">사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-244">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="7baf2-245">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7baf2-245">columnDelimiter</span></span> | <span data-ttu-id="7baf2-246">hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-246">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="7baf2-247">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7baf2-247">frequency/interval</span></span> | <span data-ttu-id="7baf2-248">hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-248">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="7baf2-249">즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-249">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="7baf2-250">Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-250">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="7baf2-251">external</span><span class="sxs-lookup"><span data-stu-id="7baf2-251">external</span></span> | <span data-ttu-id="7baf2-252">이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-252">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="7baf2-253">이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-253">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="7baf2-254">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-254">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="7baf2-255">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **InputDataset** 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-255">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** dataset.</span></span> <span data-ttu-id="7baf2-256">Hello 표시 되는지 확인 **InputDataset** hello 트리 보기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-256">Confirm that you see hello **InputDataset** in hello tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="7baf2-257">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-257">Create output dataset</span></span>
<span data-ttu-id="7baf2-258">hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-258">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7baf2-259">hello 출력 SQL 테이블 데이터 집합 (OututDataset)이이 단계에서 만드는 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-259">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="7baf2-260">Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 더 많은**, 클릭 **새 데이터 집합**를 클릭 하 고 **Azure SQL** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-260">In hello **Editor** for hello Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from hello drop-down menu.</span></span> 
2. <span data-ttu-id="7baf2-261">JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-261">Replace JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="7baf2-262">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-262">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="7baf2-263">속성</span><span class="sxs-lookup"><span data-stu-id="7baf2-263">Property</span></span> | <span data-ttu-id="7baf2-264">설명</span><span class="sxs-lookup"><span data-stu-id="7baf2-264">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7baf2-265">type</span><span class="sxs-lookup"><span data-stu-id="7baf2-265">type</span></span> | <span data-ttu-id="7baf2-266">hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-266">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="7baf2-267">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7baf2-267">linkedServiceName</span></span> | <span data-ttu-id="7baf2-268">Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-268">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7baf2-269">tableName</span><span class="sxs-lookup"><span data-stu-id="7baf2-269">tableName</span></span> | <span data-ttu-id="7baf2-270">지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-270">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="7baf2-271">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7baf2-271">frequency/interval</span></span> | <span data-ttu-id="7baf2-272">hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.</span><span class="sxs-lookup"><span data-stu-id="7baf2-272">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="7baf2-273">세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-273">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="7baf2-274">Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-274">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="7baf2-275">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-275">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="7baf2-276">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **OutputDataset** 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-276">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset** dataset.</span></span> <span data-ttu-id="7baf2-277">Hello 표시 되는지 확인 **OutputDataset** 아래 hello 트리 보기에서 **데이터 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-277">Confirm that you see hello **OutputDataset** in hello tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="7baf2-278">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="7baf2-278">Create pipeline</span></span>
<span data-ttu-id="7baf2-279">이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-279">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="7baf2-280">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-280">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="7baf2-281">이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-281">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="7baf2-282">hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-282">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="7baf2-283">따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-283">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="7baf2-284">Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-284">In hello **Editor** for hello Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="7baf2-285">단추로 또는 **파이프라인** hello 트리 뷰 및 클릭 **새 파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-285">Alternatively, you can right-click **Pipelines** in hello tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="7baf2-286">JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-286">Replace JSON in hello right pane with hello following JSON snippet:</span></span> 

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
    
    <span data-ttu-id="7baf2-287">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="7baf2-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="7baf2-288">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="7baf2-289">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7baf2-290">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="7baf2-291">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="7baf2-292">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="7baf2-293">원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7baf2-294">소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>
    - <span data-ttu-id="7baf2-295">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-295">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="7baf2-296">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-296">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="7baf2-297">hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-297">hello **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="7baf2-298">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-298">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="7baf2-299">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-299">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="7baf2-300">앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-300">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="7baf2-301">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-301">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7baf2-302">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-302">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7baf2-303">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-303">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="7baf2-304">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-304">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="7baf2-305">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **ADFTutorialPipeline**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-305">Click **Deploy** on hello toolbar toocreate and deploy hello **ADFTutorialPipeline**.</span></span> <span data-ttu-id="7baf2-306">Hello 파이프라인 hello 트리 보기에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-306">Confirm that you see hello pipeline in hello tree view.</span></span> 
4. <span data-ttu-id="7baf2-307">Hello, 닫습니다 **편집기** 블레이드를 클릭 하 여 **X**합니다. 클릭 **X** 다시 toosee hello **Data Factory** hello에 대 한 홈 페이지 **ADFTutorialDataFactory**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-307">Now, close hello **Editor** blade by clicking **X**. Click **X** again toosee hello **Data Factory** home page for hello **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="7baf2-308">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="7baf2-308">**Congratulations!**</span></span> <span data-ttu-id="7baf2-309">Azure blob 저장소 tooan Azure SQL 데이터베이스의 파이프라인 toocopy 데이터로 Azure 데이터 팩터리에 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-309">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="7baf2-310">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="7baf2-310">Monitor pipeline</span></span>
<span data-ttu-id="7baf2-311">이 단계에서 진행 되는 상황에서 Azure 데이터 팩터리에 Azure 포털 toomonitor hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-311">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="7baf2-312">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="7baf2-312">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="7baf2-313">hello 다음 단계 보여 toomonitor data factory에 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 파이프라인 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="7baf2-313">hello following steps show you how toomonitor pipelines in your data factory by using hello Monitor & Manage application:</span></span> 

1. <span data-ttu-id="7baf2-314">클릭 **모니터링 및 관리** 데이터 팩토리에 대 한 hello 홈 페이지에 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-314">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>
   
    ![타일 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="7baf2-316">별도의 탭에서 **모니터링 및 관리 응용 프로그램**이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-316">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7baf2-317">해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 hello 다음 중 하나를 수행: 지우기 hello **타사 쿠키를 차단 하 고 사이트 데이터** 확인란 (또는)에 대 한 예외를 만들려면 **login.microsoftonline.com**, 후 tooopen hello 응용 프로그램을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7baf2-317">If you see that hello web browser is stuck at "Authorizing...", do one of hello following: clear hello **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="7baf2-319">변경 hello **시작 시간** 및 **종료 시간** tooinclude (2017-05-11)를 시작 및 종료 시간 (2017-05-12), 파이프라인의 고 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-319">Change hello **Start time** and **End time** tooinclude start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>     
3. <span data-ttu-id="7baf2-320">Hello 참조 **활동 창** 파이프라인 시작과 끝 사이의 매시간와 관련 된 hello 가운데 창에서 hello 목록에는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-320">You see hello **activity windows** associated with each hour between pipeline start and end times in hello list in hello middle pane.</span></span> 
4. <span data-ttu-id="7baf2-321">선택 활동 창에 대 한 세부 정보 toosee hello hello에서 작업 창을 **활동 창** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-321">toosee details about an activity window, select hello activity window in hello **Activity Windows** list.</span></span> 
    <span data-ttu-id="7baf2-322">![활동 창 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="7baf2-322">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="7baf2-323">Hello 오른쪽에 작업 창 탐색기에서 해당 hello toohello 현재 UTC 시간 조각이 표시 (오후 8시 12분) 모두 (녹색)으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-323">In Activity Window Explorer on hello right, you see that hello slices up toohello current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="7baf2-324">hello 8-오후 9, 9-10 PM, 10-11 오후, 오후 11-오전 12 시 분할 영역을 아직 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-324">hello 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="7baf2-325">hello **시도** hello hello 데이터 조각에 대 한 실행 hello 활동에 대 한 정보를 제공 하는 창 오른쪽에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-325">hello **Attempts** section in hello right pane provides information about hello activity run for hello data slice.</span></span> <span data-ttu-id="7baf2-326">오류가 경우 hello 오류에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-326">If there was an error, it provides details about hello error.</span></span> <span data-ttu-id="7baf2-327">예를 들어 hello 폴더 또는 컨테이너를 입력 하는 경우 하지 존재 않으며 hello 조각 처리 실패 하면 해당 hello 컨테이너 없다는 오류 메시지가 표시 또는 폴더가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-327">For example, if hello input folder or container does not exist and hello slice processing fails, you see an error message stating that hello container or folder does not exist.</span></span>

    ![활동 실행 시도](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="7baf2-329">시작 **SQL Server Management Studio**toohello Azure SQL 데이터베이스를 연결 하 고 hello 행 toohello에 넣었는지 확인 **emp** hello 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-329">Launch **SQL Server Management Studio**, connect toohello Azure SQL Database, and verify that hello rows are inserted in toohello **emp** table in hello database.</span></span>
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="7baf2-331">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baf2-331">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="7baf2-332">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="7baf2-332">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="7baf2-333">Hello 다이어그램 보기를 사용 하 여 모니터 데이터 파이프라인 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-333">You can also monitor data pipelines by using hello diagram view.</span></span>  

1. <span data-ttu-id="7baf2-334">Hello에 **Data Factory** 블레이드에서 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-334">In hello **Data Factory** blade, click **Diagram**.</span></span>
   
    ![데이터 팩터리 블레이드 - 다이어그램 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="7baf2-336">다음 이미지 hello 다이어그램 비슷한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-336">You should see hello diagram similar toohello following image:</span></span> 
   
    ![다이어그램 뷰](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="7baf2-338">Hello 다이어그램 보기에서 두 번 클릭 **InputDataset** hello 데이터 집합에 대 한 toosee 슬라이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-338">In hello diagram view, double-click **InputDataset** toosee slices for hello dataset.</span></span>  
   
    ![InputDataset을 선택한 데이터 집합](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="7baf2-340">클릭 **더 보려면** toosee 모든 hello에 대 한 데이터 분할 영역을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-340">Click **See more** link toosee all hello data slices.</span></span> <span data-ttu-id="7baf2-341">24시간의 매시간 조각 중 파이프라인의 시작 시간과 종료 시간 사이에 있는 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-341">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![모든 입력 데이터 조각](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="7baf2-343">데이터 조각이 toohello 현재 UTC 시간을 hello 모든 **준비** 때문에 hello **emp.txt** hello blob 컨테이너에 파일이 있는 모든 hello 시간: **adftutorial\input**.</span><span class="sxs-lookup"><span data-stu-id="7baf2-343">Notice that all hello data slices up toohello current UTC time are **Ready** because hello **emp.txt** file exists all hello time in hello blob container: **adftutorial\input**.</span></span> <span data-ttu-id="7baf2-344">hello 조각 hello 이후 시간에 대 한 준비 상태에 아직 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-344">hello slices for hello future times are not in ready state yet.</span></span> <span data-ttu-id="7baf2-345">조각이 없습니다 hello에 표시 되는지 확인 **최근에 실패 한 조각이** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="7baf2-345">Confirm that no slices show up in hello **Recently failed slices** section at hello bottom.</span></span>
6. <span data-ttu-id="7baf2-346">닫기 hello 블레이드 할 때까지 hello 다이어그램 보기 (또는) 스크롤 왼쪽된 toosee hello 다이어그램 보기를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7baf2-346">Close hello blades until you see hello diagram view (or) scroll left toosee hello diagram view.</span></span> <span data-ttu-id="7baf2-347">그런 다음 **OutputDataset**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-347">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="7baf2-348">클릭 **더 보려면** hello에 대 한 링크 **테이블** 블레이드 **OutputDataset** toosee 모든 분할 영역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-348">Click **See more** link on hello **Table** blade for **OutputDataset** toosee all hello slices.</span></span>

    ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="7baf2-350">Toohello 현재 UTC 시간을 분할 영역을 hello 모든 공지에서 이동 **실행 보류** 상태 = > **진행에서** ==> **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-350">Notice that all hello slices up toohello current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="7baf2-351">지난 hello 분할 영역 hello (현재 시간 전) 최신 toooldest에서 기본적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-351">hello slices from hello past (before current time) are processed from latest toooldest by default.</span></span> <span data-ttu-id="7baf2-352">예를 들어 hello 현재 시간이 오후 8시 12분 UTC 일 경우 hello 분할 영역에 대 한 오후 7 시-오후 8 시 hello 오후 6 시-오후 7 시 분할 영역 보다 먼저 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-352">For example, if hello current time is 8:12 PM UTC, hello slice for 7 PM - 8 PM is processed ahead of hello 6 PM - 7 PM slice.</span></span> <span data-ttu-id="7baf2-353">hello 오후 8 시-오후 9 시 분할 영역 hello 시간 간격의 hello 끝에 오후 9 시 뒤에 있는 기본적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-353">hello 8 PM - 9 PM slice is processed at hello end of hello time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="7baf2-354">Hello 목록에서 데이터 조각을 아무 것 이나 클릭 하 고 hello 표시 되어야 **데이터 조각을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-354">Click any data slice from hello list and you should see hello **Data slice** blade.</span></span> <span data-ttu-id="7baf2-355">활동 창과 연결된 데이터 부분을 조각이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-355">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="7baf2-356">조각은 하나의 파일이거나 여러 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-356">A slice can be one file or multiple files.</span></span>  
    
     ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="7baf2-358">Hello 조각 hello에 없는 경우 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않은 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-358">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="7baf2-359">Hello에 **데이터 조각을** 블레이드를 표시 되어야 hello 맨 아래에 hello 목록에서 모든 활동을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-359">In hello **DATA SLICE** blade, you should see all activity runs in hello list at hello bottom.</span></span> <span data-ttu-id="7baf2-360">클릭는 **작업 실행** toosee hello **활동 실행 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-360">Click an **activity run** toosee hello **Activity run details** blade.</span></span> 
    
    ![작업 실행 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="7baf2-362">이 블레이드에 표시 긴 hello 복사 작업을 진행 하려면 방법 어떤 출력은 데이터의 바이트 수 된 읽기 및 작성, 실행 시작 시간, 종료 시간 등을 실행 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-362">In this blade, you see how long hello copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="7baf2-363">클릭 **X** tooclose 할 때까지 모든 hello 블레이드에 돌아갈 hello에 대 한 홈 블레이드 toohello **ADFTutorialDataFactory**합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-363">Click **X** tooclose all hello blades until you get back toohello home blade for hello **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="7baf2-364">(선택 사항)을 클릭 hello **데이터 집합** 타일 또는 **파이프라인** 타일 tooget hello 블레이드 살펴본 hello 앞의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-364">(optional) click hello **Datasets** tile or **Pipelines** tile tooget hello blades you have seen hello preceding steps.</span></span> 
14. <span data-ttu-id="7baf2-365">시작 **SQL Server Management Studio**toohello Azure SQL 데이터베이스를 연결 하 고 hello 행 toohello에 넣었는지 확인 **emp** hello 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-365">Launch **SQL Server Management Studio**, connect toohello Azure SQL Database, and verify that hello rows are inserted in toohello **emp** table in hello database.</span></span>
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="7baf2-367">요약</span><span class="sxs-lookup"><span data-stu-id="7baf2-367">Summary</span></span>
<span data-ttu-id="7baf2-368">이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-368">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="7baf2-369">Hello Azure 포털 toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-369">You used hello Azure portal toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="7baf2-370">이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-370">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="7baf2-371">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-371">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="7baf2-372">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-372">Created **linked services**:</span></span>
   1. <span data-ttu-id="7baf2-373">**Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하 여 Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-373">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="7baf2-374">**Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-374">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="7baf2-375">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-375">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="7baf2-376">원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-376">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7baf2-377">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7baf2-377">Next steps</span></span>
<span data-ttu-id="7baf2-378">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-378">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="7baf2-379">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="7baf2-379">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="7baf2-380">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baf2-380">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
