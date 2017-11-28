---
title: "Azure Blob 저장소에서 데이터를 aaaCopy | Microsoft Docs"
description: "어떻게 toocopy blob Azure Data Factory에는 데이터에 알아봅니다. 이 샘플을 사용 하 여: 어떻게 Azure Blob 저장소 및 Azure SQL 데이터베이스에서 데이터 tooand toocopy 합니다."
keywords: "Blob 데이터, Azure Blob 복사"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="221ea-105">Azure 데이터 팩터리를 사용 하 여 Azure Blob 저장소에서 데이터 tooor 복사</span><span class="sxs-lookup"><span data-stu-id="221ea-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="221ea-106">이 문서에서는 toouse 복사 작업에서 Azure Blob 저장소에서 Azure Data Factory toocopy 데이터 tooand hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="221ea-107">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="221ea-108">개요</span><span class="sxs-lookup"><span data-stu-id="221ea-108">Overview</span></span>
<span data-ttu-id="221ea-109">데이터 저장 tooAzure Blob 저장소 또는 저장소 지원 tooany 싱크 데이터를 Azure Blob 저장소에서 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="221ea-110">hello 다음 테이블 원본으로 지 원하는 데이터 저장소의 목록을 제공 하거나 hello 복사 작업에서 싱크 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="221ea-111">예를 들어 데이터를 SQL Server 데이터베이스 또는 Azure SQL 데이터베이스**에서** Azure Blob 저장소**로**로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="221ea-112">그리고 데이터를 Azure Blob Storage 저장소**에서** Azure SQL Data Warehouse 또는 Azure Cosmos DB 컬렉션**으로** 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="221ea-113">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="221ea-113">Supported scenarios</span></span>
<span data-ttu-id="221ea-114">데이터를 복사할 수 **Azure Blob 저장소에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="221ea-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="221ea-115">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure Blob 저장소**:</span><span class="sxs-lookup"><span data-stu-id="221ea-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="221ea-116">복사 작업의 데이터 복사를 지원 합니다. / tooboth 범용 Azure 저장소 계정 및 핫 냉각용/Blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="221ea-117">hello 활동 지원 **블록에서 읽기, 추가 또는 페이지 blob**를 지원 하지만 **tooonly 블록 blob 쓰기**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="221ea-118">Azure Premium Storage는 페이지 Blob으로 지원되므로 싱크로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="221ea-119">복사 활동 데이터를 성공적으로 hello toohello 대상 복사 후 hello 소스에서 데이터 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="221ea-120">성공적인 복사 후 toodelete 원본 데이터를 필요한 경우 만들는 [사용자 지정 활동](data-factory-use-custom-activities.md) toodelete 데이터 hello 및 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="221ea-121">예를 들어 참조 hello [GitHub에 Delete blob 또는 폴더 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="221ea-122">시작</span><span class="sxs-lookup"><span data-stu-id="221ea-122">Get started</span></span>
<span data-ttu-id="221ea-123">다른 도구/API를 사용하여 Azure Blob Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="221ea-124">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="221ea-125">이 기술 자료이 문서에는 [연습](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) 파이프라인 toocopy 데이터를 Azure Blob 저장소 위치 tooanother Azure Blob 저장소 위치에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="221ea-126">Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 파이프라인 toocopy 데이터를 만드는 방법에 대 한 자습서를 참조 하십시오. [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="221ea-127">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="221ea-128">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="221ea-129">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="221ea-130">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-130">Create a **data factory**.</span></span> <span data-ttu-id="221ea-131">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="221ea-132">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="221ea-133">예를 들어 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="221ea-134">연결 된 서비스를 속성에는 특정 tooAzure Blob 저장소에 대 한 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="221ea-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="221ea-135">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="221ea-136">Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="221ea-137">고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터베이스에서 다른 데이터 집합 toospecify hello SQL 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="221ea-138">특정 tooAzure Blob 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="221ea-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="221ea-139">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="221ea-140">앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlSink 싱크도 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="221ea-141">마찬가지로, Azure SQL 데이터베이스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlSource 및 사용 BlobSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="221ea-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="221ea-142">복사 활동 속성을 특정 tooAzure Blob 저장소를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="221ea-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="221ea-143">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="221ea-144">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="221ea-145">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="221ea-146">샘플은 Azure Blob 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-blob-storage  ) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="221ea-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="221ea-147">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure Blob 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="221ea-148">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="221ea-148">Linked service properties</span></span>
<span data-ttu-id="221ea-149">두 가지가 연결 된 서비스의 toolink tooan Azure 데이터 팩터리에 Azure 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="221ea-150">**AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="221ea-151">Azure 저장소 연결 서비스 hello 전역 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="221ea-152">반면 hello Azure 저장소 SAS (공유 액세스 서명) 연결 된 서비스 시간 제한/범위 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="221ea-153">이 두 연결된 서비스에는 다른 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="221ea-154">필요에 맞는 hello 연결 된 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="221ea-155">hello 다음 섹션에서는 더욱 자세히 설명에 두 개의 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="221ea-156">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="221ea-156">Dataset properties</span></span>
<span data-ttu-id="221ea-157">데이터 집합 toorepresent toospecify hello 데이터 집합의 hello 형식 속성을 설정 Azure Blob 저장소의 데이터 입력 또는 출력: **AzureBlob**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="221ea-158">집합 hello **linkedServiceName** hello Azure 저장소 서비스 또는 Azure 저장소 SAS의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="221ea-159">hello 데이터 집합의 hello 유형 속성 지정 hello **blob 컨테이너** 및 hello **폴더** hello blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="221ea-160">JSON 섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="221ea-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="221ea-161">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="221ea-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="221ea-162">데이터 팩터리의 지원 "구조" 읽기 스키마에 데이터 원본에 대 한 Azure blob 등의 형식 정보를 제공 하는 데 CLS 규격.NET 기반 유형 값을 다음 hello: Int16, Int32, Int64, Single, Double, Decimal, Byte, Bool, String, Guid, Datetime, Datetimeoffset, Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="221ea-163">데이터 팩터리 tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동할 때 자동으로 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="221ea-164">hello **typeProperties** 섹션 데이터 집합의 각 유형에 대해 서로 다른 이며 정보 제공 hello 위치에 대 한 서식을 지정 등을 hello 데이터 저장소에서 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="221ea-165">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **AzureBlob** 데이터 집합에 다음과 같은 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="221ea-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="221ea-166">속성</span><span class="sxs-lookup"><span data-stu-id="221ea-166">Property</span></span> | <span data-ttu-id="221ea-167">설명</span><span class="sxs-lookup"><span data-stu-id="221ea-167">Description</span></span> | <span data-ttu-id="221ea-168">필수</span><span class="sxs-lookup"><span data-stu-id="221ea-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="221ea-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="221ea-169">folderPath</span></span> |<span data-ttu-id="221ea-170">경로 toohello 컨테이너 및 blob 저장소 hello에에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="221ea-171">예제: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="221ea-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="221ea-172">예</span><span class="sxs-lookup"><span data-stu-id="221ea-172">Yes</span></span> |
| <span data-ttu-id="221ea-173">fileName</span><span class="sxs-lookup"><span data-stu-id="221ea-173">fileName</span></span> |<span data-ttu-id="221ea-174">Hello blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-174">Name of hello blob.</span></span> <span data-ttu-id="221ea-175">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="221ea-176">에 파일 이름, hello 작업 (복사본 포함) 작동을 지정한 경우에 특정 Blob을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="221ea-177">파일 이름을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath에 모든 Blob을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="221ea-178">때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 활동 싱크에 지정 되지 않은: 데이터.<Guid>합니다. txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="221ea-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="221ea-179">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-179">No</span></span> |
| <span data-ttu-id="221ea-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="221ea-180">partitionedBy</span></span> |<span data-ttu-id="221ea-181">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="221ea-182">사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="221ea-183">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="221ea-184">Hello 참조 [partitionedBy 속성 섹션을 사용 하 여](#using-partitionedBy-property) 자세한 내용 및 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="221ea-185">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-185">No</span></span> |
| <span data-ttu-id="221ea-186">format</span><span class="sxs-lookup"><span data-stu-id="221ea-186">format</span></span> | <span data-ttu-id="221ea-187">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="221ea-188">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="221ea-189">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="221ea-190">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="221ea-191">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-191">No</span></span> |
| <span data-ttu-id="221ea-192">압축</span><span class="sxs-lookup"><span data-stu-id="221ea-192">compression</span></span> | <span data-ttu-id="221ea-193">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="221ea-194">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="221ea-195">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="221ea-196">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="221ea-197">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="221ea-198">partitionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="221ea-198">Using partitionedBy property</span></span>
<span data-ttu-id="221ea-199">동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="221ea-200">시간 시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 및 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="221ea-201">샘플 1</span><span class="sxs-lookup"><span data-stu-id="221ea-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="221ea-202">이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="221ea-203">hello SliceStart hello 조각의 toostart 시간을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="221ea-204">hello folderPath 각 조각에 대 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="221ea-205">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다</span><span class="sxs-lookup"><span data-stu-id="221ea-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="221ea-206">샘플 2</span><span class="sxs-lookup"><span data-stu-id="221ea-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="221ea-207">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="221ea-208">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="221ea-208">Copy activity properties</span></span>
<span data-ttu-id="221ea-209">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="221ea-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="221ea-210">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="221ea-211">반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="221ea-212">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="221ea-213">Azure Blob 저장소에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**BlobSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="221ea-214">마찬가지로, 데이터 tooan Azure Blob 저장소를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="221ea-215">이 섹션에서는 BlobSource 및 BlobSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="221ea-216">**BlobSource** hello 다음과 같은 hello에 대 한 속성을 지 원하는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="221ea-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="221ea-217">속성</span><span class="sxs-lookup"><span data-stu-id="221ea-217">Property</span></span> | <span data-ttu-id="221ea-218">설명</span><span class="sxs-lookup"><span data-stu-id="221ea-218">Description</span></span> | <span data-ttu-id="221ea-219">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="221ea-219">Allowed values</span></span> | <span data-ttu-id="221ea-220">필수</span><span class="sxs-lookup"><span data-stu-id="221ea-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="221ea-221">recursive</span><span class="sxs-lookup"><span data-stu-id="221ea-221">recursive</span></span> |<span data-ttu-id="221ea-222">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="221ea-223">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="221ea-223">True (default value), False</span></span> |<span data-ttu-id="221ea-224">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-224">No</span></span> |

<span data-ttu-id="221ea-225">**BlobSink** hello 다음과 같은 속성을 지 원하는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="221ea-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="221ea-226">속성</span><span class="sxs-lookup"><span data-stu-id="221ea-226">Property</span></span> | <span data-ttu-id="221ea-227">설명</span><span class="sxs-lookup"><span data-stu-id="221ea-227">Description</span></span> | <span data-ttu-id="221ea-228">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="221ea-228">Allowed values</span></span> | <span data-ttu-id="221ea-229">필수</span><span class="sxs-lookup"><span data-stu-id="221ea-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="221ea-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="221ea-230">copyBehavior</span></span> |<span data-ttu-id="221ea-231">파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="221ea-232"><b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="221ea-233">hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="221ea-234"><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일에에서 있는 hello 먼저 대상 폴더의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="221ea-235">hello 대상 파일에는 자동 생성 된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="221ea-236"><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="221ea-237">Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="221ea-238">아니요</span><span class="sxs-lookup"><span data-stu-id="221ea-238">No</span></span> |

<span data-ttu-id="221ea-239">**BlobSource**에서도 이전 버전과의 호환성을 위해 이러한 두 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="221ea-240">**treatEmptyAsNull**:를 지정 하는지 여부를 null 값으로 tootreat null 또는 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="221ea-241">**skipHeaderLineCount** - 건너뛰어야 하는 줄 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="221ea-242">입력 데이터 집합이 TextFormat을 사용하는 경우에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="221ea-243">마찬가지로, **BlobSink** hello 다음 이전 버전과 호환성에 대 한 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="221ea-244">**blobWriterAddHeader**: tooadd tooan에 쓰는 동안 열 정의의 헤더 출력 데이터 집합 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="221ea-245">다음과 같은 속성을 구현 하는 데이터 집합 지금은 지원 hello hello 동일한 기능: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="221ea-246">hello 다음 표에서 지침에 대해 이러한 blob 원본/싱크 속성 대신 hello 새 데이터 집합 속성을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="221ea-247">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="221ea-247">Copy Activity property</span></span> | <span data-ttu-id="221ea-248">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="221ea-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="221ea-249">BlobSource에서 skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="221ea-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="221ea-250">skipLineCount 및 firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="221ea-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="221ea-251">줄은 먼저 건너뜁니다 고 hello 첫 번째 행을 머리글로 다음 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="221ea-252">BlobSource에서 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="221ea-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="221ea-253">입력 데이터 집합에서 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="221ea-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="221ea-254">BlobSink에서 blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="221ea-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="221ea-255">출력 데이터 집합에서 firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="221ea-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="221ea-256">이러한 속성에 대한 자세한 내용은 [TextFormat 지정](data-factory-supported-file-and-compression-formats.md#text-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="221ea-257">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="221ea-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="221ea-258">이 섹션에서는 hello 재귀 및 copyBehavior 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="221ea-259">recursive</span><span class="sxs-lookup"><span data-stu-id="221ea-259">recursive</span></span> | <span data-ttu-id="221ea-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="221ea-260">copyBehavior</span></span> | <span data-ttu-id="221ea-261">결과 동작</span><span class="sxs-lookup"><span data-stu-id="221ea-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="221ea-262">true</span><span class="sxs-lookup"><span data-stu-id="221ea-262">true</span></span> |<span data-ttu-id="221ea-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="221ea-263">preserveHierarchy</span></span> |<span data-ttu-id="221ea-264">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-265">Folder1</span></span><br/><span data-ttu-id="221ea-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-272">hello 대상 폴더가 Folder1 hello 소스로 구조체 같은 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="221ea-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-273">Folder1</span></span><br/><span data-ttu-id="221ea-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="221ea-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="221ea-280">true</span><span class="sxs-lookup"><span data-stu-id="221ea-280">true</span></span> |<span data-ttu-id="221ea-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="221ea-281">flattenHierarchy</span></span> |<span data-ttu-id="221ea-282">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-283">Folder1</span></span><br/><span data-ttu-id="221ea-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-290">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-291">Folder1</span></span><br/><span data-ttu-id="221ea-292">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="221ea-293">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="221ea-294">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="221ea-295">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="221ea-296">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="221ea-297">true</span><span class="sxs-lookup"><span data-stu-id="221ea-297">true</span></span> |<span data-ttu-id="221ea-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="221ea-298">mergeFiles</span></span> |<span data-ttu-id="221ea-299">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-300">Folder1</span></span><br/><span data-ttu-id="221ea-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-307">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-308">Folder1</span></span><br/><span data-ttu-id="221ea-309">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="221ea-310">false</span><span class="sxs-lookup"><span data-stu-id="221ea-310">false</span></span> |<span data-ttu-id="221ea-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="221ea-311">preserveHierarchy</span></span> |<span data-ttu-id="221ea-312">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="221ea-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-313">Folder1</span></span><br/><span data-ttu-id="221ea-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-320">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="221ea-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-321">Folder1</span></span><br/><span data-ttu-id="221ea-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="221ea-324">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="221ea-325">false</span><span class="sxs-lookup"><span data-stu-id="221ea-325">false</span></span> |<span data-ttu-id="221ea-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="221ea-326">flattenHierarchy</span></span> |<span data-ttu-id="221ea-327">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="221ea-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-328">Folder1</span></span><br/><span data-ttu-id="221ea-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-335">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="221ea-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-336">Folder1</span></span><br/><span data-ttu-id="221ea-337">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="221ea-338">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="221ea-339">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="221ea-340">false</span><span class="sxs-lookup"><span data-stu-id="221ea-340">false</span></span> |<span data-ttu-id="221ea-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="221ea-341">mergeFiles</span></span> |<span data-ttu-id="221ea-342">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="221ea-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="221ea-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-343">Folder1</span></span><br/><span data-ttu-id="221ea-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="221ea-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="221ea-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="221ea-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="221ea-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="221ea-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="221ea-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="221ea-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="221ea-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="221ea-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="221ea-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="221ea-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="221ea-350">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="221ea-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="221ea-351">Folder1</span></span><br/><span data-ttu-id="221ea-352">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="221ea-353">File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="221ea-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="221ea-354">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="221ea-355">연습: 복사 마법사를 사용 하 여 toocopy 한 데이터를 Blob 저장소에서</span><span class="sxs-lookup"><span data-stu-id="221ea-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="221ea-356">어떻게 tooquickly 복사 데이터는 Azure에서 blob 저장소에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="221ea-357">이 연습에 나오는 원본 및 대상 데이터 저장소의 유형은 모두 Azure Blob Storage입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="221ea-358">hello이 연습에는 파이프라인에서에서 데이터를 복사 hello에서 폴더 tooanother 동일한 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="221ea-359">이 연습에서는 의도적으로 간단한 tooshow 설정이 나 원본 또는 싱크도 Blob 저장소를 사용 하는 경우 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="221ea-360">필수 조건</span><span class="sxs-lookup"><span data-stu-id="221ea-360">Prerequisites</span></span>
1. <span data-ttu-id="221ea-361">아직 만들지 않은 경우 범용 **Azure Storage 계정**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="221ea-362">Hello blob 저장소를 사용 하 여 두 가지 모두 **소스** 및 **대상** 이 연습에 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="221ea-363">Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계 toocreate 하나에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="221ea-364">라는 blob 컨테이너 만들기 **adfblobconnector** hello 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="221ea-365">라는 폴더를 만듭니다 **입력** hello에 **adfblobconnector** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="221ea-366">라는 파일을 만들어 **emp.txt** 다음 hello로 콘텐츠 및 toohello 업로드 **입력** 폴더와 같은 도구를 사용 하 여 [Azure 저장소 탐색기](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="221ea-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="221ea-367">Hello 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="221ea-367">Create hello data factory</span></span>
1. <span data-ttu-id="221ea-368">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="221ea-369">클릭 **+ 새로 만들기** hello 왼쪽 위 모퉁이에서 클릭 **인텔리전스 + 분석**를 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="221ea-370">Hello에 **새 데이터 팩터리** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="221ea-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="221ea-371">입력 **ADFBlobConnectorDF** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="221ea-372">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="221ea-373">Hello 오류가 나타나면: `*Data factory name “ADFBlobConnectorDF” is not available`을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFBlobConnectorDF)을 변경 하 고 다시 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="221ea-374">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="221ea-375">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="221ea-376">리소스 그룹에 대 한 선택 **기존 항목 사용** tooselect 기존 리소스 그룹 (또는) 선택 **새로 만들기** tooenter 리소스 그룹에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="221ea-377">선택 된 **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="221ea-378">선택 **Pin toodashboard** hello hello 블레이드 맨 아래에 있는 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="221ea-379">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-379">Click **Create**.</span></span>
3. <span data-ttu-id="221ea-380">Hello 참조 hello 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 블레이드: ![데이터 팩터리 홈 페이지](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="221ea-381">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="221ea-381">Copy Wizard</span></span>
1. <span data-ttu-id="221ea-382">Hello Data Factory 홈 페이지에서 클릭 hello **[미리 보기] 데이터를 복사** toolaunch 타일 **복사 데이터 마법사** 별도 탭에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="221ea-383">해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 사용 안 함/취소 **타사 쿠키를 차단 하 고 사이트 데이터** 설정 (또는)에 사용 가능한 상태로 유지 하 고 예외를 만들 **login.microsoftonline.com**및 hello 마법사를 다시 시작 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="221ea-384">Hello에 **속성** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="221ea-385">**작업 이름**에 대해 **CopyPipeline**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="221ea-386">hello 작업 이름은 hello 데이터 팩터리에 파이프라인의 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="221ea-387">입력 한 **설명** hello 작업 (옵션)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="221ea-388">에 대 한 **작업 흐름 또는 작업 일정**, hello 유지 **일정에 따라 정기적으로 실행** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="221ea-389">Toorun 대신 한 번만이 작업 일정에 따라 반복적으로 실행 선택 **이제 한 번 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="221ea-390">**지금 한 번 실행** 옵션을 선택하면 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="221ea-391">에 대 한 hello 설정을 유지 **되풀이 패턴**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="221ea-392">Hello 다음 단계에서이 작업을 매일 실행 hello 사이의 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="221ea-393">변경 hello **시작 날짜 시간이** 너무**04/21/2017**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="221ea-394">변경 hello **종료 날짜 시간** 너무**04/25/2017**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="221ea-395">Hello 달력을 찾아보는 대신 tootype hello 날짜를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="221ea-396">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-396">Click **Next**.</span></span>
      <span data-ttu-id="221ea-397">![복사 도구 - 속성 페이지](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="221ea-398">Hello에 **소스 데이터 저장소** 페이지 **Azure Blob 저장소** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="221ea-399">이 페이지 toospecify hello 원본 데이터 저장소를 사용 하 여 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="221ea-400">기존 데이터 저장소 연결된 서비스를 사용하거나 새 데이터 저장소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="221ea-401">연결 된 서비스는 기존 toouse, 선택 **에서 기존 연결 된 서비스** 선택 hello 오른쪽 연결 된 서비스 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="221ea-402">![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="221ea-403">Hello에 **hello Azure Blob 저장소 계정을 지정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="221ea-404">Hello에 대 한 자동 생성 된 이름을 유지 **연결 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="221ea-405">hello 연결 이름은 hello 유형의 hello 연결 된 서비스 이름입니다: Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="221ea-406">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="221ea-407">Azure 구독을 선택하거나 **Azure 구독**에 대해 **모두 선택**을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="221ea-408">선택 된 **Azure 저장소 계정** hello에서 목록은 Azure 저장소 계정 선택 hello 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="221ea-409">선택할 수도 있습니다 tooenter 저장소 계정 설정을 수동으로 선택 하 여 **수동으로 입력** hello에 대 한 옵션 **계정 선택 방법을**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="221ea-410">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-410">Click **Next**.</span></span> 
      <span data-ttu-id="221ea-411">![도구에 복사-hello Azure Blob 저장소 계정을 지정 합니다.](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="221ea-412">**선택 hello 입력된 파일이 나 폴더** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="221ea-413">**adfblobcontainer**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="221ea-414">**input**을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="221ea-415">이 연습에서는 hello 입력된 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="221ea-416">선택할 수 있습니다 hello emp.txt 파일 hello 폴더에 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="221ea-417">![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="221ea-418">Hello에 **선택 hello 입력된 파일이 나 폴더** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="221ea-419">해당 hello 확인 **파일 또는 폴더** 너무 설정**adfblobconnector/입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="221ea-420">Hello 파일이 하위 폴더에 있는 경우 예를 들어 2017/04/01, 02, 2017/04/및, 값을 입력 adfblobconnector / / {year} / {month} / {day} 파일 또는 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="221ea-421">Hello 텍스트 상자에서 TAB 키를 누르는 경우 연도 (yyyy), (MM), 월 및 일 (dd)에 대 한 세 가지 드롭 다운 목록을 tooselect 형식 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="221ea-422">**파일을 재귀적으로 복사**는 설정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="221ea-423">이 옵션 toorecursively 트래버스 파일 toobe 복사한 toohello 대상 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="221ea-424">Hello 하지 않는 **이진 복사** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="221ea-425">이 옵션 tooperform 소스 파일 toohello 대상 이진 복사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="221ea-426">Hello 다음 페이지에 더 많은 옵션을 볼 수 있도록이 연습에 대 한 선택 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="221ea-427">해당 hello 확인 **압축 유형** 너무 설정**None**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="221ea-428">소스 파일 지원 hello 형식 중 하나에서 압축 된 경우이 옵션에 대 한 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="221ea-429">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-429">Click **Next**.</span></span>
    <span data-ttu-id="221ea-430">![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="221ea-431">Hello에 **파일 형식 설정** hello 구분 기호 및 hello 파일을 구문 분석 하 여 hello 마법사에 의해 자동으로 감지 있는 hello 스키마 참조 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="221ea-432">다음 옵션 hello 확인:는 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-432">Confirm hello following options: a.</span></span> <span data-ttu-id="221ea-433">hello **파일 형식** 너무 설정**텍스트 형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="221ea-434">Hello 드롭 다운 목록에서 모든 hello 지원 형식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="221ea-435">예: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="221ea-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="221ea-436">b.</span><span class="sxs-lookup"><span data-stu-id="221ea-436">b.</span></span> <span data-ttu-id="221ea-437">hello **열 구분 기호** 너무 설정`Comma (,)`합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="221ea-438">나타나면 hello hello 드롭 다운 목록에서 데이터 팩터리에서 지 원하는 다른 열 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="221ea-439">사용자 지정 구분 기호를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="221ea-440">c.</span><span class="sxs-lookup"><span data-stu-id="221ea-440">c.</span></span> <span data-ttu-id="221ea-441">hello **행 구분 기호** 너무 설정`Carriage Return + Line feed (\r\n)`합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="221ea-442">나타나면 hello hello 드롭 다운 목록에서 데이터 팩터리에서 지 원하는 다른 행 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="221ea-443">사용자 지정 구분 기호를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="221ea-444">d.</span><span class="sxs-lookup"><span data-stu-id="221ea-444">d.</span></span> <span data-ttu-id="221ea-445">hello **줄 수를 건너뛰고** 너무 설정**0**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="221ea-446">Hello 파일의 맨 위에 hello에서 건너뛰는 몇 줄 toobe 여기 hello 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="221ea-447">e.</span><span class="sxs-lookup"><span data-stu-id="221ea-447">e.</span></span>  <span data-ttu-id="221ea-448">hello **첫 번째 데이터 행에 열 이름이 포함** 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="221ea-449">Hello 소스 파일 hello 첫 번째 행에 열 이름이 없으면이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="221ea-450">f.</span><span class="sxs-lookup"><span data-stu-id="221ea-450">f.</span></span> <span data-ttu-id="221ea-451">hello **빈 열 값을 null로 취급** 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="221ea-452">확장 **고급 설정** toosee 고급 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="221ea-453">Hello 페이지의 hello 맨 아래에 참조 hello **미리 보기** hello emp.txt 파일의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="221ea-454">클릭 **스키마** hello 아래쪽 toosee hello 스키마에서 유추 hello 원본 파일의 hello 데이터 확인 하 여 해당 hello 복사 마법사를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="221ea-455">클릭 **다음** hello 구분 기호를 검토 하 고 데이터를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="221ea-456">![복사 도구 - 파일 형식 설정](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="221ea-457">Hello에 **대상 데이터 저장소 페이지**선택, **Azure Blob 저장소**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="221ea-458">이 연습에서는 두 hello 소스 및 대상 데이터 저장소로 hello Azure Blob 저장소를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="221ea-459">![복사 도구 - 대상 데이터 저장소 선택](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="221ea-460">**hello Azure Blob 저장소 계정을 지정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="221ea-461">입력 **AzureStorageLinkedService** hello에 대 한 **연결 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="221ea-462">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="221ea-463">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="221ea-464">Azure 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="221ea-465">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-465">Click **Next**.</span></span>     
10. <span data-ttu-id="221ea-466">Hello에 **선택 hello 출력 파일 또는 폴더** 페이지:</span><span class="sxs-lookup"><span data-stu-id="221ea-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="221ea-467">**폴더 경로**를 **adfblobconnector/output/{year}/{month}/{day}**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="221ea-468">**탭**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="221ea-469">Hello에 대 한 **연도**선택, **yyyy**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="221ea-470">Hello에 대 한 **월**, 너무 설정 되어 있는지 확인**MM**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="221ea-471">Hello에 대 한 **일**, 너무 설정 되어 있는지 확인**dd**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="221ea-472">해당 hello 확인 **압축 유형** 너무 설정**None**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="221ea-473">해당 hello 확인 **복사 동작** 너무 설정**파일을 병합**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="221ea-474">Hello 동일한 이름이 이미 존재 하는 hello로 파일을 출력으로 hello 새 콘텐츠 경우 동일한 파일 hello 끝에 추가 된 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="221ea-475">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-475">Click **Next**.</span></span>
    <span data-ttu-id="221ea-476">![복사 도구 - 출력 파일 또는 폴더 선택](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="221ea-477">Hello에 **파일 형식 설정** 페이지 hello 설정을 검토 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="221ea-478">Hello 추가 옵션 중 하나 tooadd 헤더 toohello 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="221ea-479">해당 옵션을 선택 하면 hello 열 이름을 사용 하 여 hello hello 소스 스키마에서 머리글 행이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="221ea-480">Hello 소스에 대 한 hello 스키마를 볼 때 hello 기본 열 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="221ea-481">예를 들어 hello 첫 번째 열 tooFirst 이름 및 두 번째 열 tooLast 이름 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="221ea-482">그런 다음 열 이름으로 이러한 이름 가진 헤더로 hello 출력 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="221ea-483">![복사 도구 - 대상의 파일 형식 설정](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="221ea-484">Hello에 **성능 설정** 페이지를 확인 하는 **단위 클라우드** 및 **복사본 병렬** 너무 설정**자동**, 고 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="221ea-485">이러한 설정에 대한 자세한 내용은 [복사 활동 성능 및 튜닝 가이드](data-factory-copy-activity-performance.md#parallel-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="221ea-486">![복사 도구 - 성능 설정](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="221ea-487">Hello에 **요약** 페이지 (작업 속성, 소스 및 대상에 대 한 설정 및 설정 복사) 하는 모든 설정을 검토 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="221ea-488">![복사 도구 - 요약 페이지](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="221ea-489">Hello에 대 한 정보를 검토 **요약** 페이지를 클릭 하 여 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="221ea-490">hello 마법사 (여기서 hello 복사 마법사를 실행)에서 hello data factory에 두 개의 연결 된 서비스, 두 개의 데이터 집합 (입력 및 출력) 및 하나의 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="221ea-491">![복사 도구 - 배포 페이지](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="221ea-492">모니터 hello 파이프라인 (복사 작업)</span><span class="sxs-lookup"><span data-stu-id="221ea-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="221ea-493">Hello 링크를 클릭 `Click here toomonitor copy pipeline` hello에 **배포** 페이지.</span><span class="sxs-lookup"><span data-stu-id="221ea-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="221ea-494">Hello 표시 되어야 **모니터링 하 고 응용 프로그램 관리** 별도 탭에 있습니다.  ![앱 모니터링 및 관리](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="221ea-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="221ea-495">변경 hello **시작** hello 위쪽에서 시간을 너무`04/19/2017` 및 **끝** 너무 시간`04/27/2017`, 클릭 하 고 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="221ea-496">Hello에 5 개 활동 창 표시 되어야 **활동 창** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="221ea-497">hello **WindowStart** 번 파이프라인 시작 toopipeline 종료 시간에서 모든 날짜를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="221ea-498">클릭 **새로 고침** hello에 대 한 단추 **활동 창** 를 여러 번 표시 될 때까지 모든 hello 활동 창의 hello 상태 목록 tooReady 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="221ea-499">이제, hello 출력 파일이 adfblobconnector 컨테이너의 hello 출력 폴더에 생성 되는 것으로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="221ea-500">Hello 출력 폴더의 폴더 구조를 다음 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="221ea-501">데이터 팩터리 모니터링 및 관리에 대한 자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="221ea-502">데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="221ea-502">Data Factory entities</span></span>
<span data-ttu-id="221ea-503">이제 hello Data Factory 홈 페이지를 뒤로 toohello 탭을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="221ea-504">현재 데이터 팩터리에는 두 개의 연결된 서비스, 두 개의 데이터 집합 및 한 개의 파이프라인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![엔터티가 있는 데이터 팩터리 홈 페이지](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="221ea-506">클릭 **작성자 및 배포** toolaunch 데이터 팩터리 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![데이터 팩터리 편집기](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="221ea-508">Data factory에 Data Factory 엔터티에 따라 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="221ea-509">두 개의 연결된 서비스.</span><span class="sxs-lookup"><span data-stu-id="221ea-509">Two linked services.</span></span> <span data-ttu-id="221ea-510">Hello 원본과 hello 대상에 대해 다른 노드로 hello에 대 한 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="221ea-511">두 연결 hello 서비스 참조 toohello이이 연습에서 동일한 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="221ea-512">두 개의 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-512">Two datasets.</span></span> <span data-ttu-id="221ea-513">입력 데이터 집합 및 출력 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="221ea-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="221ea-514">이 연습에서는 둘 다 사용 하 여 hello 컨테이너 blob 동일 하지만 toodifferent 폴더 (입력 및 출력)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="221ea-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="221ea-515">파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-515">A pipeline.</span></span> <span data-ttu-id="221ea-516">hello 파이프라인 blob 원본 및 Azure blob 위치 tooanother Azure blob 위치에서에서 blob 싱크 toocopy 데이터를 사용 하는 복사 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="221ea-517">hello 다음 섹션에서는 이러한 엔터티에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="221ea-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="221ea-518">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="221ea-518">Linked services</span></span>
<span data-ttu-id="221ea-519">두 개의 연결된 서비스가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-519">You should see two linked services.</span></span> <span data-ttu-id="221ea-520">Hello 원본과 hello 대상에 대해 다른 노드로 hello에 대 한 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="221ea-521">이 연습에서는 둘 다 정의 모양을 hello 동일 hello 이름을 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="221ea-522">hello **형식** hello 연결 된 서비스 설정 너무**AzureStorage**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="221ea-523">연결 된 hello 서비스 정의의 가장 중요 한 속성은 hello **connectionString**, Data Factory tooconnect tooyour 런타임 시 Azure 저장소 계정에서 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="221ea-524">Hello 정의 hello hubName 속성을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="221ea-525">원본 Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="221ea-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="221ea-526">대상 Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="221ea-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="221ea-527">Azure Storage 링크된 서비스에 대한 자세한 내용은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="221ea-528">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="221ea-528">Datasets</span></span>
<span data-ttu-id="221ea-529">입력 데이터 집합과 출력 데이터 집합의 두 가지 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="221ea-530">hello 데이터 집합의 hello 형식이 너무 설정**AzureBlob** 모두에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="221ea-531">입력된 데이터 집합 hello 가리키는 toohello **입력** hello의 폴더 **adfblobconnector** blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="221ea-532">hello **외부** 너무 속성이**true** hello로이 데이터 집합에 대 한 데이터 생성 되지 않을 hello 파이프라인에서이 데이터 집합을 입력으로 사용 하는 hello 복사 활동을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="221ea-533">출력 데이터 집합 포인트 toohello hello **출력** hello의 폴더 같은 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="221ea-534">hello 출력 데이터 집합 또한 사용 하 여 hello 연도, 월 및 일의 hello **SliceStart** 시스템 변수 toodynamically hello 출력 파일에 대 한 hello 경로 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="221ea-535">Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="221ea-536">hello **외부** 너무 속성이**false** (기본값)이 데이터이 집합은 hello 파이프라인에서 생성 된 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="221ea-537">Azure Blob 데이터 집합이 지원하는 속성에 대한 자세한 내용은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="221ea-538">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="221ea-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="221ea-539">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="221ea-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="221ea-540">파이프라인</span><span class="sxs-lookup"><span data-stu-id="221ea-540">Pipeline</span></span>
<span data-ttu-id="221ea-541">hello 파이프라인에는 하나의 활동을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="221ea-542">hello **형식** 활동 너무 설정의 hello**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="221ea-543">Hello 활동에 대 한 hello 형식 속성에 두 개의 섹션, 원본과 싱크에 대 한 다른 하나는 hello에 대 한 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="221ea-544">hello 원본 유형이 너무 설정 되어**BlobSource** 대로 hello 활동은 blob 저장소에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="221ea-545">hello 싱크 유형이 설정 되어 너무**BlobSink** hello 활동 데이터 tooa blob 저장소에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="221ea-546">hello 복사 활동 변수로 InputDataset z4y hello 입력과 OutputDataset z4y hello 출력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="221ea-547">BlobSource 및 BlobSink에서 지원하는 속성에 대한 자세한 내용은 [복사 활동 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="221ea-548">Blob 저장소에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="221ea-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="221ea-549">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="221ea-550">보여 줍니다 어떻게 Azure Blob 저장소 및 Azure SQL 데이터베이스에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="221ea-551">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="221ea-552">JSON의 예: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="221ea-553">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="221ea-553">hello following sample shows:</span></span>

1. <span data-ttu-id="221ea-554">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="221ea-555">[AzureStorage](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="221ea-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="221ea-556">[AzureBlob](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="221ea-557">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="221ea-558">[BlobSource](#copy-activity-properties) 및 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="221ea-559">hello 샘플 시계열 데이터 복사, Azure blob tooan Azure SQL 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="221ea-560">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="221ea-561">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="221ea-561">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="221ea-562">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="221ea-562">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="221ea-563">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="221ea-564">에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="221ea-565">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="221ea-566">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="221ea-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="221ea-567">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="221ea-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="221ea-568">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="221ea-569">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="221ea-570">"external": "true" 설정을 알리고 Data Factory hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="221ea-571">**Azure SQL 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="221ea-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="221ea-572">hello 예제는 Azure SQL 데이터베이스에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="221ea-573">Azure SQL 데이터베이스를와 hello 테이블 만들기 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="221ea-574">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-574">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="221ea-575">**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="221ea-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="221ea-576">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="221ea-577">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="221ea-578">JSON의 예: Azure SQL tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="221ea-579">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="221ea-579">hello following sample shows:</span></span>

1. <span data-ttu-id="221ea-580">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="221ea-581">[AzureStorage](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="221ea-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="221ea-582">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="221ea-583">[AzureBlob](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="221ea-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="221ea-584">[SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 및 [BlobSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="221ea-585">hello 샘플에 1 시간 마다 Azure SQL 테이블 tooan Azure blob에서에서 시계열 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="221ea-586">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="221ea-587">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="221ea-587">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="221ea-588">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="221ea-588">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="221ea-589">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="221ea-590">에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="221ea-591">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="221ea-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="221ea-592">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="221ea-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="221ea-593">hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="221ea-594">설정 "외부": "true" 알립니다 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="221ea-595">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="221ea-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="221ea-596">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="221ea-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="221ea-597">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="221ea-598">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="221ea-599">**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="221ea-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="221ea-600">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="221ea-601">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="221ea-602">hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

> [!NOTE]
> <span data-ttu-id="221ea-603">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="221ea-604">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="221ea-604">Performance and Tuning</span></span>
<span data-ttu-id="221ea-605">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="221ea-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
