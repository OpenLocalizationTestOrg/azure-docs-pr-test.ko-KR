---
title: "Azure Blob Storage 간 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory에서 Blob 데이터를 복사하는 방법을 알아봅니다. 샘플 사용: Azure Blob 저장소 및 Azure SQL 데이터베이스 간에 데이터를 복사하는 방법입니다."
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
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="b377e-105">Azure Data Factory를 사용하여 Azure Blob Storage 사이에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b377e-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="b377e-106">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure Blob Storage 사이에서 데이터를 복사하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="b377e-107">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="b377e-108">개요</span><span class="sxs-lookup"><span data-stu-id="b377e-108">Overview</span></span>
<span data-ttu-id="b377e-109">모든 지원되는 원본 데이터 저장소에서 Azure Blob Storage로 또는 Azure Blob Storage에서 모든 지원되는 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="b377e-110">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="b377e-111">예를 들어 데이터를 SQL Server 데이터베이스 또는 Azure SQL 데이터베이스**에서** Azure Blob 저장소**로**로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="b377e-112">그리고 데이터를 Azure Blob Storage 저장소**에서** Azure SQL Data Warehouse 또는 Azure Cosmos DB 컬렉션**으로** 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="b377e-113">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="b377e-113">Supported scenarios</span></span>
<span data-ttu-id="b377e-114">**Azure Blob Storage에서** 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b377e-115">다음 데이터 저장소에서 **Azure Blob Storage로** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="b377e-116">복사 작업은 범용 Azure Storage 계정 및 핫/쿨 Blob Storage 간의 데이터 복사를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="b377e-117">이 작업은 **블록에서 읽기, 추가 또는 페이지 Blob**를 지원하며 **블록 Blob에 쓰기만** 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="b377e-118">Azure Premium Storage는 페이지 Blob으로 지원되므로 싱크로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="b377e-119">복사 작업 시 데이터가 대상에 성공적으로 복사된 후 원본에서 데이터가 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="b377e-120">성공적으로 복사한 후에 원본 데이터를 삭제해야 하는 경우 데이터를 삭제하는 [사용자 지정 활동](data-factory-use-custom-activities.md)을 만들고 파이프라인에서 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="b377e-121">예를 들어 [GitHub의 blob 또는 폴더 삭제 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="b377e-122">시작</span><span class="sxs-lookup"><span data-stu-id="b377e-122">Get started</span></span>
<span data-ttu-id="b377e-123">다른 도구/API를 사용하여 Azure Blob Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="b377e-124">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b377e-125">이 문서에는 Azure Blob Storage 위치에서 다른 Azure Blob Storage 위치로 데이터를 복사하기 위한 파이프라인을 만드는 [연습](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) 과정이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="b377e-126">Azure Blob Storage에서 Azure SQL Server Database로 데이터를 복사하기 위한 파이프라인 생성에 대한 자습서를 보려면 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="b377e-127">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b377e-128">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="b377e-129">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b377e-130">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-130">Create a **data factory**.</span></span> <span data-ttu-id="b377e-131">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b377e-132">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="b377e-133">예를 들어 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 경우 Azure Storage 계정 및 Azure SQL Database를 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="b377e-134">Azure Blob Storage와 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="b377e-135">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="b377e-136">마지막 단계에서 설명한 예제에서는 입력 데이터가 포함된 BLOB 컨테이너 및 폴더를 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="b377e-137">그리고 Blob Storage에서 복사한 데이터를 포함하는 Azure SQL Database의 SQL 테이블을 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="b377e-138">Azure Blob Storage와 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="b377e-139">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b377e-140">앞에서 언급한 예에서는 BlobSource를 원본으로, SqlSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="b377e-141">마찬가지로, Azure SQL Database에서 Azure Blob Storage로 복사하는 경우 복사 작업에 SqlSource 및 BlobSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="b377e-142">Azure Blob Storage와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b377e-143">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="b377e-144">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b377e-145">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b377e-146">다른 곳에서 Azure Blob Storage로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-blob-storage  ) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="b377e-147">다음 섹션에서는 Azure Blob Storage에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b377e-148">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="b377e-148">Linked service properties</span></span>
<span data-ttu-id="b377e-149">Azure Storage를 Azure Data Factory에 연결하는 데 사용할 수 있는 두 가지 유형의 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="b377e-150">**AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="b377e-151">Azure 저장소 연결된 서비스는 Azure 저장소에 대한 전역 액세스로 Data Factory를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="b377e-152">반면 Azure 저장소 SAS(공유 액세스 서명) 연결된 서비스는 Azure 저장소에 대한 제한/시간 제한 액세스로 Data Factory를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="b377e-153">이 두 연결된 서비스에는 다른 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="b377e-154">필요에 맞는 연결된 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="b377e-155">다음 섹션에서는 이러한 두 연결된 서비스에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="b377e-156">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="b377e-156">Dataset properties</span></span>
<span data-ttu-id="b377e-157">Azure Blob Storage에서 입력 또는 출력 데이터를 표시할 데이터 집합을 지정하려면 데이터 집합의 형식 속성을 **AzureBlob**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="b377e-158">데이터 집합의 **linkedServiceName** 속성을 Azure Storage 또는 Azure Storage SAS 연결된 서비스의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="b377e-159">데이터 집합의 형식 속성은 Blob Storage에서 **Blob 컨테이너**와 **폴더**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="b377e-160">데이터 집합 정의에 사용할 수 있는 JSON 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b377e-161">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="b377e-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b377e-162">데이터 팩터리는 Azure Blob과 같은 읽기 데이터 원본의 스키마에 대해 "structure"에 형식 정보를 제공하기 위해 다음과 같은 CLS 규격 .NET 기반 형식 값을 지원합니다. Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="b377e-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="b377e-163">데이터 팩터리는 원본 데이터 저장소의 데이터를 싱크 데이터 저장소로 복사할 때 형식 변환을 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="b377e-164">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치, 서식 등에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="b377e-165">**AzureBlob** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="b377e-166">속성</span><span class="sxs-lookup"><span data-stu-id="b377e-166">Property</span></span> | <span data-ttu-id="b377e-167">설명</span><span class="sxs-lookup"><span data-stu-id="b377e-167">Description</span></span> | <span data-ttu-id="b377e-168">필수</span><span class="sxs-lookup"><span data-stu-id="b377e-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b377e-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="b377e-169">folderPath</span></span> |<span data-ttu-id="b377e-170">blob 저장소에서 컨테이너 및 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="b377e-171">예제: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="b377e-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="b377e-172">예</span><span class="sxs-lookup"><span data-stu-id="b377e-172">Yes</span></span> |
| <span data-ttu-id="b377e-173">fileName</span><span class="sxs-lookup"><span data-stu-id="b377e-173">fileName</span></span> |<span data-ttu-id="b377e-174">Blob의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-174">Name of the blob.</span></span> <span data-ttu-id="b377e-175">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="b377e-176">filename을 지정하는 경우 활동(복사 포함)은 특정 Blob에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="b377e-177">fileName을 지정하지 않으면 복사는 입력 데이터 집합에 대한 folderPath에 모든 Blob을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="b377e-178">**fileName**이 출력 데이터 집합에 대해 지정되지 않았고 **preserveHierarchy**가 활동 싱크에 지정되지 않은 경우 생성된 파일의 이름은 다음 형식을 사용합니다. Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="b377e-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="b377e-179">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-179">No</span></span> |
| <span data-ttu-id="b377e-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b377e-180">partitionedBy</span></span> |<span data-ttu-id="b377e-181">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="b377e-182">동적 folderPath 및 시계열 데이터에 대한 filename을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="b377e-183">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="b377e-184">자세한 내용과 예제는 [partitionedBy 속성 사용 섹션](#using-partitionedBy-property)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="b377e-185">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-185">No</span></span> |
| <span data-ttu-id="b377e-186">format</span><span class="sxs-lookup"><span data-stu-id="b377e-186">format</span></span> | <span data-ttu-id="b377e-187">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b377e-188">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="b377e-189">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="b377e-190">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="b377e-191">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-191">No</span></span> |
| <span data-ttu-id="b377e-192">압축</span><span class="sxs-lookup"><span data-stu-id="b377e-192">compression</span></span> | <span data-ttu-id="b377e-193">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="b377e-194">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b377e-195">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b377e-196">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b377e-197">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="b377e-198">partitionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="b377e-198">Using partitionedBy property</span></span>
<span data-ttu-id="b377e-199">이전 섹션에서 설명했듯이 **partitionedBy** 속성, [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 사용하여 시계열 데이터의 동적 folderPath와 filename을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="b377e-200">시간 시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 및 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="b377e-201">샘플 1</span><span class="sxs-lookup"><span data-stu-id="b377e-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="b377e-202">이 예제에서 {Slice}는 지정된 형식(YYYYMMDDHH)의 Data Factory 시스템 변수 SliceStart 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="b377e-203">SliceStart는 조각의 시작 시간을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="b377e-204">folderPath는 각 조각에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="b377e-205">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다</span><span class="sxs-lookup"><span data-stu-id="b377e-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="b377e-206">샘플 2</span><span class="sxs-lookup"><span data-stu-id="b377e-206">Sample 2</span></span>

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

<span data-ttu-id="b377e-207">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b377e-208">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="b377e-208">Copy activity properties</span></span>
<span data-ttu-id="b377e-209">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b377e-210">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="b377e-211">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="b377e-212">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="b377e-213">Azure Blob Storage에서 데이터를 이동하는 경우 복사 작업의 원본 유형을 **BlobSource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="b377e-214">마찬가지로 Azure Blob Storage로 데이터를 이동하는 경우 복사 작업의 싱크 유형을 **BlobSink**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="b377e-215">이 섹션에서는 BlobSource 및 BlobSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="b377e-216">**BlobSource**는 **typeProperties** 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="b377e-217">속성</span><span class="sxs-lookup"><span data-stu-id="b377e-217">Property</span></span> | <span data-ttu-id="b377e-218">설명</span><span class="sxs-lookup"><span data-stu-id="b377e-218">Description</span></span> | <span data-ttu-id="b377e-219">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b377e-219">Allowed values</span></span> | <span data-ttu-id="b377e-220">필수</span><span class="sxs-lookup"><span data-stu-id="b377e-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b377e-221">recursive</span><span class="sxs-lookup"><span data-stu-id="b377e-221">recursive</span></span> |<span data-ttu-id="b377e-222">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="b377e-223">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="b377e-223">True (default value), False</span></span> |<span data-ttu-id="b377e-224">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-224">No</span></span> |

<span data-ttu-id="b377e-225">**BlobSink**는 **typeProperties** 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="b377e-226">속성</span><span class="sxs-lookup"><span data-stu-id="b377e-226">Property</span></span> | <span data-ttu-id="b377e-227">설명</span><span class="sxs-lookup"><span data-stu-id="b377e-227">Description</span></span> | <span data-ttu-id="b377e-228">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b377e-228">Allowed values</span></span> | <span data-ttu-id="b377e-229">필수</span><span class="sxs-lookup"><span data-stu-id="b377e-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b377e-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b377e-230">copyBehavior</span></span> |<span data-ttu-id="b377e-231">원본이 BlobSource 또는 FileSystem인 경우 복사 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="b377e-232"><b>PreserveHierarchy</b>: 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="b377e-233">원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="b377e-234"><b>FlattenHierarchy</b>: 원본 폴더의 모든 파일은 대상 폴더의 첫 번째 수준에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="b377e-235">대상 파일은 자동 생성된 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="b377e-236"><b>MergeFiles</b>: 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="b377e-237">파일/Blob 이름이 지정된 경우 지정된 이름이 병합된 파일 이름이 됩니다. 그렇지 않으면 자동 생성된 파일 이름이 병합된 파일 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="b377e-238">아니요</span><span class="sxs-lookup"><span data-stu-id="b377e-238">No</span></span> |

<span data-ttu-id="b377e-239">**BlobSource**에서도 이전 버전과의 호환성을 위해 이러한 두 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="b377e-240">**treatEmptyAsNull**: Null 또는 빈 문자열을 null 값으로 처리할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="b377e-241">**skipHeaderLineCount** - 건너뛰어야 하는 줄 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="b377e-242">입력 데이터 집합이 TextFormat을 사용하는 경우에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="b377e-243">마찬가지로, **BlobSink**는 이전 버전과의 호환성을 위해 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="b377e-244">**blobWriterAddHeader**: 출력 데이터 집합에 쓰는 동안 열 정의의 헤더를 추가할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="b377e-245">이제 데이터 집합은 동일한 기능을 구현하는 다음 속성을 지원합니다. **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**</span><span class="sxs-lookup"><span data-stu-id="b377e-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="b377e-246">다음 표에서는 Blob 원본/싱크 속성 대신 새 데이터 집합 속성을 사용하는 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="b377e-247">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="b377e-247">Copy Activity property</span></span> | <span data-ttu-id="b377e-248">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="b377e-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="b377e-249">BlobSource에서 skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="b377e-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="b377e-250">skipLineCount 및 firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="b377e-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="b377e-251">줄을 먼저 건너뛴 다음 첫 번째 행을 헤더로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="b377e-252">BlobSource에서 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="b377e-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="b377e-253">입력 데이터 집합에서 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="b377e-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="b377e-254">BlobSink에서 blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="b377e-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="b377e-255">출력 데이터 집합에서 firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="b377e-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="b377e-256">이러한 속성에 대한 자세한 내용은 [TextFormat 지정](data-factory-supported-file-and-compression-formats.md#text-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="b377e-257">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="b377e-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="b377e-258">이 섹션에서는 다양한 recursive 및 copyBehavior 값 조합에 대한 복사 작업의 결과 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="b377e-259">recursive</span><span class="sxs-lookup"><span data-stu-id="b377e-259">recursive</span></span> | <span data-ttu-id="b377e-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b377e-260">copyBehavior</span></span> | <span data-ttu-id="b377e-261">결과 동작</span><span class="sxs-lookup"><span data-stu-id="b377e-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b377e-262">true</span><span class="sxs-lookup"><span data-stu-id="b377e-262">true</span></span> |<span data-ttu-id="b377e-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b377e-263">preserveHierarchy</span></span> |<span data-ttu-id="b377e-264">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-265">Folder1</span></span><br/><span data-ttu-id="b377e-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-272">Folder1 대상 폴더가 다음과 같이 원본 폴더와 동일한 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="b377e-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-273">Folder1</span></span><br/><span data-ttu-id="b377e-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="b377e-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="b377e-280">true</span><span class="sxs-lookup"><span data-stu-id="b377e-280">true</span></span> |<span data-ttu-id="b377e-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b377e-281">flattenHierarchy</span></span> |<span data-ttu-id="b377e-282">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-283">Folder1</span></span><br/><span data-ttu-id="b377e-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-290">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-291">Folder1</span></span><br/><span data-ttu-id="b377e-292">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b377e-293">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="b377e-294">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="b377e-295">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="b377e-296">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="b377e-297">true</span><span class="sxs-lookup"><span data-stu-id="b377e-297">true</span></span> |<span data-ttu-id="b377e-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b377e-298">mergeFiles</span></span> |<span data-ttu-id="b377e-299">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-300">Folder1</span></span><br/><span data-ttu-id="b377e-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-307">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-308">Folder1</span></span><br/><span data-ttu-id="b377e-309">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="b377e-310">false</span><span class="sxs-lookup"><span data-stu-id="b377e-310">false</span></span> |<span data-ttu-id="b377e-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b377e-311">preserveHierarchy</span></span> |<span data-ttu-id="b377e-312">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="b377e-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-313">Folder1</span></span><br/><span data-ttu-id="b377e-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-320">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b377e-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-321">Folder1</span></span><br/><span data-ttu-id="b377e-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="b377e-324">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b377e-325">false</span><span class="sxs-lookup"><span data-stu-id="b377e-325">false</span></span> |<span data-ttu-id="b377e-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b377e-326">flattenHierarchy</span></span> |<span data-ttu-id="b377e-327">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b377e-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-328">Folder1</span></span><br/><span data-ttu-id="b377e-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-335">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b377e-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-336">Folder1</span></span><br/><span data-ttu-id="b377e-337">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b377e-338">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="b377e-339">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="b377e-340">false</span><span class="sxs-lookup"><span data-stu-id="b377e-340">false</span></span> |<span data-ttu-id="b377e-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b377e-341">mergeFiles</span></span> |<span data-ttu-id="b377e-342">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="b377e-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="b377e-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-343">Folder1</span></span><br/><span data-ttu-id="b377e-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="b377e-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b377e-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="b377e-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b377e-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="b377e-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b377e-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="b377e-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b377e-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="b377e-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b377e-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="b377e-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b377e-350">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="b377e-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="b377e-351">Folder1</span></span><br/><span data-ttu-id="b377e-352">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="b377e-353">File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="b377e-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="b377e-354">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="b377e-355">연습: 복사 마법사를 사용하여 Blob 저장소 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b377e-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="b377e-356">Azure Blob 저장소 간에 데이터를 빠르게 복사하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="b377e-357">이 연습에 나오는 원본 및 대상 데이터 저장소의 유형은 모두 Azure Blob Storage입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="b377e-358">이 연습의 파이프라인은 한 폴더의 데이터를 동일한 Blob 컨테이너의 다른 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="b377e-359">이 연습에서는 Blob Storage를 원본 또는 싱크로 사용할 때 설정 또는 속성을 표시하는 것이 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="b377e-360">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b377e-360">Prerequisites</span></span>
1. <span data-ttu-id="b377e-361">아직 만들지 않은 경우 범용 **Azure Storage 계정**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="b377e-362">이 연습에서는 Blob 저장소를 **원본** 및 **대상** 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="b377e-363">Azure Storage 계정이 없는 경우 새로 만드는 단계는 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="b377e-364">저장소 계정에 **adfblobconnector**라는 Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="b377e-365">**adfblobconnector** 컨테이너에 **input**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="b377e-366">[Azure Storage 탐색기](https://azurestorageexplorer.codeplex.com/)와 같은 도구를 사용하여 다음 내용이 포함된 **emp.txt**라는 파일을 만들어 **input** 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="b377e-367">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="b377e-367">Create the data factory</span></span>
1. <span data-ttu-id="b377e-368">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b377e-369">왼쪽 위 모서리에서 **+ 새로 만들기**를 클릭하고 **인텔리전스 + 분석**을 클릭하고 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="b377e-370">**새 데이터 팩터리** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="b377e-371">**이름**으로 **ADFBlobConnectorDF** 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="b377e-372">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="b377e-373">`*Data factory name “ADFBlobConnectorDF” is not available` 오류가 표시되면 데이터 팩터리 이름을 변경하고(예: yournameADFBlobConnectorDF) 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="b377e-374">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="b377e-375">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="b377e-376">리소스 그룹에 대해 **기존 리소스 그룹 사용**을 선택하고 기존 리소스 그룹을 선택하거나 **새로 만들기**를 선택하여 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="b377e-377">Data Factory의 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="b377e-378">블레이드 하단에서 **대시보드에 고정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="b377e-379">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-379">Click **Create**.</span></span>
3. <span data-ttu-id="b377e-380">작성이 완료되면 다음 이미지와 같이 **데이터 팩터리** 블레이드가 나타납니다. ![데이터 팩터리 홈 페이지](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="b377e-381">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="b377e-381">Copy Wizard</span></span>
1. <span data-ttu-id="b377e-382">데이터 팩터리 홈 페이지에서 **데이터 복사[미리 보기]** 타일을 클릭하여 **데이터 복사 마법사**를 별도의 탭에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="b377e-383">웹 브라우저가 "권한 부여..." 상태로 중지된 것을 확인하면 **타사 쿠키 및 사이트 데이터 차단** 설정을 사용 안 함/선택 취소하고 (또는) 계속 사용하지 않습니다. 그리고 **login.microsoftonline.com**에 대한 예외를 만든 다음 마법사를 다시 시작해봅니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="b377e-384">**속성** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="b377e-385">**작업 이름**에 대해 **CopyPipeline**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="b377e-386">태스크 이름은 데이터 팩터리의 파이프라인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="b377e-387">작업에 대한 **설명**을 입력합니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="b377e-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="b377e-388">**작업 흐름 또는 작업 일정**에 대해서는  **일정에 따라 정기적으로 실행** 옵션을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="b377e-389">스케줄에서 반복적으로 실행하는 대신 이 태스크를 한 번만 실행하려면 **지금 한 번 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="b377e-390">**지금 한 번 실행** 옵션을 선택하면 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="b377e-391">**되풀이 패턴**에 대한 설정을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="b377e-392">이 작업은 다음 단계에서 지정한 시작 시간과 종료 시간 사이에 매일 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="b377e-393">**시작 날짜 시간**을 **04/21/2017**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="b377e-394">**종료 날짜 시간**을 **04/25/2017**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="b377e-395">캘린더를 탐색하는 대신 날짜를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="b377e-396">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-396">Click **Next**.</span></span>
      <span data-ttu-id="b377e-397">![복사 도구 - 속성 페이지](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="b377e-398">**원본 데이터 저장소** 페이지에서 **Azure Blob Storage** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="b377e-399">이 페이지를 사용하여 복사 작업에 사용할 원본 데이터 저장소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="b377e-400">기존 데이터 저장소 연결된 서비스를 사용하거나 새 데이터 저장소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="b377e-401">기존의 연결된 서비스를 사용하려면 **기존의 연결된 서비스에서**를 클릭하고 올바로 연결된 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="b377e-402">![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="b377e-403">**Azure Blob 저장소 계정 지정** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="b377e-404">**연결 이름**에 대해 자동 생성된 이름을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="b377e-405">연결 이름은 Azure Storage 유형의 링크된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="b377e-406">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="b377e-407">Azure 구독을 선택하거나 **Azure 구독**에 대해 **모두 선택**을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="b377e-408">선택한 구독에서 사용할 수 있는 Azure Storage 계정 목록에서 **Azure Storage 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="b377e-409">**계정 선택 방법**으로 **수동으로 입력** 옵션을 선택하여 저장소 계정 설정을 수동으로 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="b377e-410">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-410">Click **Next**.</span></span> 
      <span data-ttu-id="b377e-411">![복사 도구 - Azure Blob 저장소 계정 지정](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="b377e-412">**입력 파일 또는 폴더 선택** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="b377e-413">**adfblobcontainer**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="b377e-414">**input**을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="b377e-415">이 연습에서는 입력 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="b377e-416">대신 폴더에서 emp.txt 파일을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="b377e-417">![복사 도구 - 입력 파일 또는 폴더 선택](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="b377e-418">**입력 파일 또는 폴더 선택** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="b377e-419">**파일 또는 폴더**가 **adfblobconnector/input**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="b377e-420">파일이 하위 폴더(예: 2017/04/01, 2017/04/02)에 있는 경우 파일 또는 폴더에 대해 adfblobconnector/input/{year}/{month}/{day}를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="b377e-421">텍스트 상자 밖으로 TAB을 누르면 연도(yyyy), 월(MM) 및 일(dd)의 형식을 선택하는 세 개의 드롭다운 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="b377e-422">**파일을 재귀적으로 복사**는 설정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b377e-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="b377e-423">대상에 복사할 파일의 폴더를 반복적으로 탐색하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="b377e-424">**이진 복사** 옵션을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b377e-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="b377e-425">원본 파일을 대상으로 이진 복사본을 수행하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="b377e-426">이 연습을 선택하지 마십시오. 다음 페이지에서 더 많은 옵션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="b377e-427">**압축 유형**이 **없음**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="b377e-428">소스 파일이 지원되는 형식 중 하나로 압축된 경우 이 옵션의 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="b377e-429">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-429">Click **Next**.</span></span>
    <span data-ttu-id="b377e-430">![복사 도구 - 입력 파일 또는 폴더 선택](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="b377e-431">**파일 형식 설정** 페이지에 파일을 구문 분석하여 마법사에 의해 자동으로 감지되는 구분 기호와 스키마가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="b377e-432">다음 옵션을 확인합니다. a.</span><span class="sxs-lookup"><span data-stu-id="b377e-432">Confirm the following options: a.</span></span> <span data-ttu-id="b377e-433">**파일 형식**이 **텍스트 형식**으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="b377e-434">드롭다운 목록에서 지원되는 모든 형식을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="b377e-435">예: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="b377e-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="b377e-436">b.</span><span class="sxs-lookup"><span data-stu-id="b377e-436">b.</span></span> <span data-ttu-id="b377e-437">**열 구분 기호**가 `Comma (,)`로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="b377e-438">드롭다운 목록에서 Data Factory가 지원하는 다른 열 구분 기호를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="b377e-439">사용자 지정 구분 기호를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="b377e-440">c.</span><span class="sxs-lookup"><span data-stu-id="b377e-440">c.</span></span> <span data-ttu-id="b377e-441">**행 구분 기호**가 `Carriage Return + Line feed (\r\n)`로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="b377e-442">드롭다운 목록에서 Data Factory가 지원하는 다른 행 구분 기호를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="b377e-443">사용자 지정 구분 기호를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="b377e-444">d.</span><span class="sxs-lookup"><span data-stu-id="b377e-444">d.</span></span> <span data-ttu-id="b377e-445">**건너뛸 줄 수**가 **0**으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="b377e-446">파일 맨 위에서 몇 줄을 건너뛰려면 여기에 숫자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="b377e-447">e.</span><span class="sxs-lookup"><span data-stu-id="b377e-447">e.</span></span>  <span data-ttu-id="b377e-448">**첫 번째 데이터 행에 열 이름 포함**이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="b377e-449">원본 파일에 첫 번째 행에 열 이름이 있으면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="b377e-450">f.</span><span class="sxs-lookup"><span data-stu-id="b377e-450">f.</span></span> <span data-ttu-id="b377e-451">**빈 열 값을 Null로 간주합니다** 옵션이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="b377e-452">**고급 설정**을 확장하여 사용 가능한 고급 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="b377e-453">페이지 맨 아래에서 emp.txt 파일의 데이터 **미리 보기**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="b377e-454">아래쪽의 **스키마** 탭을 클릭하면 원본 파일의 데이터를 보고 복사 마법사가 추론한 스키마를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="b377e-455">구분 기호를 검토하고 데이터를 미리 본 후에 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="b377e-456">![복사 도구 - 파일 형식 설정](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="b377e-457">**대상 데이터 저장소 페이지**에서 **Azure Blob Storage**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="b377e-458">이 연습에서는 Azure Blob 저장소를 원본 및 대상 데이터 저장소로 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="b377e-459">![복사 도구 - 대상 데이터 저장소 선택](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="b377e-460">**Azure Blob 저장소 계정 지정** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="b377e-461">**연결 이름** 필드에 **AzureStorageLinkedService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="b377e-462">**계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="b377e-463">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="b377e-464">Azure 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="b377e-465">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-465">Click **Next**.</span></span>     
10. <span data-ttu-id="b377e-466">**출력 파일 또는 폴더 선택** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="b377e-467">**폴더 경로**를 **adfblobconnector/output/{year}/{month}/{day}**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="b377e-468">**탭**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="b377e-469">**년**에 대해 **yyyy**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="b377e-470">**월**에 대해 **MM**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="b377e-471">**일**에 대해 **dd**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="b377e-472">**압축 유형**이 **없음**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="b377e-473">**복사 동작**이 **파일 병합**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="b377e-474">같은 이름의 출력 파일이 이미 존재하면 새로운 내용이 끝에 동일한 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="b377e-475">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-475">Click **Next**.</span></span>
    <span data-ttu-id="b377e-476">![복사 도구 - 출력 파일 또는 폴더 선택](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="b377e-477">**파일 형식 설정** 페이지에서 설정을 검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="b377e-478">추가 옵션 중 하나는 출력 파일에 헤더를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="b377e-479">이 옵션을 선택하면 원본의 스키마에서 열 이름과 함께 머리글 행이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="b377e-480">원본에 대한 스키마를 볼 때 기본 열 이름의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="b377e-481">예를 들어 첫 번째 열을 이름으로, 두 번째 열을 성으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="b377e-482">그런 다음 출력 파일은 이러한 이름을 가진 머리글을 열 이름으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="b377e-483">![복사 도구 - 대상의 파일 형식 설정](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="b377e-484">**성능 설정** 페이지에서 **클라우드 단위** 및 **병렬 사본**이 **자동**으로 설정되었는지 확인하고 다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="b377e-485">이러한 설정에 대한 자세한 내용은 [복사 활동 성능 및 튜닝 가이드](data-factory-copy-activity-performance.md#parallel-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="b377e-486">![복사 도구 - 성능 설정](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="b377e-487">**요약** 페이지에서 모든 설정(작업 속성, 원본 및 대상 설정 및 복사 설정)을 검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="b377e-488">![복사 도구 - 요약 페이지](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="b377e-489">**요약** 페이지에서 정보를 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="b377e-490">마법사는 데이터 팩터리(복사 마법사를 실행한 위치)에 두 개의 연결된 서비스, 두 개의 데이터 집합(입력 및 출력), 하나의 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="b377e-491">![복사 도구 - 배포 페이지](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="b377e-492">파이프라인(복사 활동) 모니터링</span><span class="sxs-lookup"><span data-stu-id="b377e-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="b377e-493">**배포** 페이지에서 `Click here to monitor copy pipeline` 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="b377e-494">별도의 탭에서 **응용 프로그램 모니터링 및 관리**를 보아야 합니다.  ![앱 모니터링 및 관리](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="b377e-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="b377e-495">상단의 **시작** 시간을 `04/19/2017` 및 **종료** 시간을 `04/27/2017`로 변경한 다음 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="b377e-496">**활동 창** 목록에 5개의 활동 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="b377e-497">**WindowStart** 시간은 파이프라인 시작부터 파이프라인 종료 시간까지의 모든 날을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="b377e-498">모든 활동 창의 상태가 준비로 설정될 때까지 **활동 창** 목록에 대한 **새로 고침** 단추를 몇 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="b377e-499">이제 출력 파일이 adfblobconnector 컨테이너의 출력 폴더에 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="b377e-500">출력 폴더에 다음 폴더 구조가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="b377e-501">데이터 팩터리 모니터링 및 관리에 대한 자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="b377e-502">데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="b377e-502">Data Factory entities</span></span>
<span data-ttu-id="b377e-503">이제 데이터 팩터리 홈 페이지로 다시 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="b377e-504">현재 데이터 팩터리에는 두 개의 연결된 서비스, 두 개의 데이터 집합 및 한 개의 파이프라인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![엔터티가 있는 데이터 팩터리 홈 페이지](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="b377e-506">**작성자를 클릭하고 배포**하여 데이터 팩터리 편집기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![데이터 팩터리 편집기](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="b377e-508">데이터 팩터리에 다음과 같은 데이터 팩터리 엔티티가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="b377e-509">두 개의 연결된 서비스.</span><span class="sxs-lookup"><span data-stu-id="b377e-509">Two linked services.</span></span> <span data-ttu-id="b377e-510">하나는 원본을 위한 것이고 다른 하나는 목적지를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="b377e-511">연결된 서비스는 모두 이 연습에서 동일한 Azure Storage 계정을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="b377e-512">두 개의 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-512">Two datasets.</span></span> <span data-ttu-id="b377e-513">입력 데이터 집합 및 출력 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="b377e-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="b377e-514">이 연습에서는 둘 다 동일한 Blob 컨테이너를 사용하지만 다른 폴더(입력 및 출력)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="b377e-515">파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-515">A pipeline.</span></span> <span data-ttu-id="b377e-516">파이프라인에는 Blob 원본 및 Blob 싱크를 사용하여 Azure Blob 위치에서 다른 Azure Blob 위치로 데이터를 복사하는 복사 활동이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="b377e-517">다음 섹션에서는 이러한 요소에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="b377e-518">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b377e-518">Linked services</span></span>
<span data-ttu-id="b377e-519">두 개의 연결된 서비스가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-519">You should see two linked services.</span></span> <span data-ttu-id="b377e-520">하나는 원본을 위한 것이고 다른 하나는 목적지를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="b377e-521">이 연습에서는 이름을 제외하고 두 정의가 모두 동일하게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="b377e-522">연결된 서비스의 **형식**이 **AzureStorage**로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="b377e-523">연결된 서비스 정의의 가장 중요한 속성은 **connectionString**입니다. 이는 Data Factory에서 런타임에 Azure Storage 계정에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="b377e-524">정의에서 hubName 특성을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="b377e-525">원본 Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b377e-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="b377e-526">대상 Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b377e-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="b377e-527">Azure Storage 링크된 서비스에 대한 자세한 내용은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="b377e-528">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b377e-528">Datasets</span></span>
<span data-ttu-id="b377e-529">입력 데이터 집합과 출력 데이터 집합의 두 가지 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="b377e-530">데이터 집합의 유형은 둘 다 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="b377e-531">입력 데이터 집합은 **adfblobconnector** Blob 컨테이너의 **input** 폴더를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="b377e-532">이 데이터 집합을 입력으로 사용하는 복사 활동으로 파이프라인에서 데이터를 생성하지 않으므로 이 데이터 집합에 대해 **external** 속성이 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="b377e-533">출력 데이터 집합은 동일한 Blob 컨테이너의 **output** 폴더를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="b377e-534">출력 데이터 집합은 **SliceStart** 시스템 변수의 년, 월, 일을 사용하여 출력 파일의 경로를 동적으로 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="b377e-535">Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="b377e-536">이 데이터 집합이 파이프라인에 의해 생성되기 때문에 **external** 속성은 **false**(기본값)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="b377e-537">Azure Blob 데이터 집합이 지원하는 속성에 대한 자세한 내용은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="b377e-538">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b377e-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="b377e-539">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b377e-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="b377e-540">파이프라인</span><span class="sxs-lookup"><span data-stu-id="b377e-540">Pipeline</span></span>
<span data-ttu-id="b377e-541">파이프라인에는 하나의 활동만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-541">The pipeline has just one activity.</span></span> <span data-ttu-id="b377e-542">활동의 **type**은 **Copy**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="b377e-543">활동의 유형 특성에는 원본과 싱크에 대한 두 개의 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="b377e-544">활동 유형이 Blob 저장 영역에서 데이터를 복사할 때 원본 유형은 **BlobSource**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="b377e-545">싱크 유형은 **BlobSink**로 설정되어 데이터를 Blob 저장소에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="b377e-546">복사 활동은 InputDataset-z4y를 입력으로, OutputDataset-z4y를 출력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="b377e-547">BlobSource 및 BlobSink에서 지원하는 속성에 대한 자세한 내용은 [복사 활동 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="b377e-548">Blob Storage로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="b377e-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="b377e-549">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b377e-550">Azure Blob 저장소 및 Azure SQL 데이터베이스 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="b377e-551">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="b377e-552">JSON 예제: Blob Storage에서 SQL Database로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b377e-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="b377e-553">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-553">The following sample shows:</span></span>

1. <span data-ttu-id="b377e-554">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="b377e-555">[AzureStorage](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b377e-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="b377e-556">[AzureBlob](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="b377e-557">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b377e-558">[BlobSource](#copy-activity-properties) 및 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b377e-559">샘플은 Azure Blob에서 Azure SQL 테이블로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="b377e-560">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b377e-561">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="b377e-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="b377e-562">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="b377e-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="b377e-563">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b377e-564">첫 번째 것의 경우 계정 키를 포함하는 연결 문자열을 지정하고 이후 것의 경우 SAS(공유 액세스 서명) Uri를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b377e-565">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="b377e-566">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="b377e-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="b377e-567">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="b377e-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b377e-568">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b377e-569">폴더 경로에는 시작 시간의 년/월/일 부분이 사용되고 파일 이름에는 시작 시간의 시간 부분이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="b377e-570">"external": "true"를 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="b377e-571">**Azure SQL 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="b377e-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="b377e-572">샘플은 Azure SQL 데이터베이스의 "MyTable"이라는 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="b377e-573">Blob CSV 파일을 포함하려 하면 같은 수의 열을 사용하여 Azure SQL 데이터베이스에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="b377e-574">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-574">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="b377e-575">**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="b377e-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="b377e-576">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b377e-577">파이프라인 JSON 정의에서 **원본** 형식은 **BlobSource**로 설정되고 **싱크** 형식은 **SqlSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="b377e-578">JSON 예제: Azure SQL에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b377e-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="b377e-579">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-579">The following sample shows:</span></span>

1. <span data-ttu-id="b377e-580">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="b377e-581">[AzureStorage](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b377e-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="b377e-582">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b377e-583">[AzureBlob](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="b377e-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="b377e-584">[SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 및 [BlobSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b377e-585">샘플은 Azure SQL 테이블에서 Azure Blob으로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="b377e-586">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b377e-587">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="b377e-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="b377e-588">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="b377e-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="b377e-589">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b377e-590">첫 번째 것의 경우 계정 키를 포함하는 연결 문자열을 지정하고 이후 것의 경우 SAS(공유 액세스 서명) Uri를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b377e-591">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="b377e-592">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="b377e-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="b377e-593">샘플은 Azure SQL에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn"라는 열이 포함되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="b377e-594">"external": "true"를 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="b377e-595">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="b377e-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b377e-596">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="b377e-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b377e-597">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b377e-598">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="b377e-599">**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="b377e-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="b377e-600">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b377e-601">파이프라인 JSON 정의에서 **source** 형식은 **SqlSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b377e-602">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b377e-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="b377e-603">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b377e-604">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="b377e-604">Performance and Tuning</span></span>
<span data-ttu-id="b377e-605">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b377e-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
