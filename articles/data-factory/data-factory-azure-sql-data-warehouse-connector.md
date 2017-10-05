---
title: "Azure SQL Data Warehouse 간 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Azure SQL Data Warehouse 간 데이터를 복사하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="861af-103">Azure Data Factory를 사용하여 Azure SQL Data Warehouse 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="861af-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="861af-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure SQL Data Warehouse 간에 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="861af-106">최상의 성능을 얻으려면 PolyBase를 사용하여 Azure SQL Data Warehouse에 데이터를 로드하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-107">자세한 내용은 [PolyBase를 사용하여 Azure SQL 데이터 웨어하우스에 데이터 로드](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="861af-108">사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="861af-109">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="861af-109">Supported scenarios</span></span>
<span data-ttu-id="861af-110">**Azure SQL Data Warehouse**에서 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="861af-111">다음 데이터 저장소에서 **Azure SQL Data Warehouse로** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="861af-112">SQL Server 또는 Azure SQL Database에서 Azure SQL Data Warehouse로 데이터를 복사할 때 대상 저장소에 테이블이 없으면 Data Factory가 소스 데이터 저장소에 있는 테이블의 스키마를 사용하여SQL Data Warehouse에 테이블을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="861af-113">자세한 내용은 [자동 테이블 만들기](#auto-table-creation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="861af-114">지원되는 인증 유형</span><span class="sxs-lookup"><span data-stu-id="861af-114">Supported authentication type</span></span>
<span data-ttu-id="861af-115">Azure SQL Data Warehouse 커넥터는 기본 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="861af-116">시작</span><span class="sxs-lookup"><span data-stu-id="861af-116">Getting started</span></span>
<span data-ttu-id="861af-117">다른 도구/API를 사용하여 Azure SQL Data Warehouse 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="861af-118">Azure SQL 데이터 웨어하우스 간에 데이터를 복사하는 파이프라인을 만드는 가장 쉬운 방법은 데이터 복사 마법사를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="861af-119">데이터 복사 마법사를 사용한 파이프라인 작성에 대한 연습은 [자습서: 데이터 팩터리를 통해 SQL Data Warehouse에 데이터 로드](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="861af-120">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="861af-121">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="861af-122">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="861af-123">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-123">Create a **data factory**.</span></span> <span data-ttu-id="861af-124">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="861af-125">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="861af-126">예를 들어 Azure Blob Storage에서 Azure SQL Data Warehouse로 데이터를 복사하는 경우 Azure Storage 계정 및 Azure SQL Data Warehouse를 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="861af-127">Azure SQL Data Warehouse와 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="861af-128">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="861af-129">마지막 단계에서 설명한 예제에서는 입력 데이터가 포함된 BLOB 컨테이너 및 폴더를 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="861af-130">그리고 Blob Storage에서 복사한 데이터를 포함하는 Azure SQL Data Warehouse의 테이블을 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="861af-131">Azure SQL Data Warehouse와 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="861af-132">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="861af-133">앞에서 언급한 예에서는 BlobSource를 원본으로, SqlDWSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="861af-134">마찬가지로, Azure SQL Data Warehouse에서 Azure Blob Storage로 복사하는 경우 복사 작업에 SqlDWSource 및 BlobSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="861af-135">Azure SQL Data Warehouse와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="861af-136">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="861af-137">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="861af-138">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="861af-139">다른 곳에서 Azure SQL Data Warehouse로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="861af-140">다음 섹션에서는 Azure SQL Data Warehouse에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="861af-141">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="861af-141">Linked service properties</span></span>
<span data-ttu-id="861af-142">다음 테이블은 Azure SQL 데이터 웨어하우스 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="861af-143">속성</span><span class="sxs-lookup"><span data-stu-id="861af-143">Property</span></span> | <span data-ttu-id="861af-144">설명</span><span class="sxs-lookup"><span data-stu-id="861af-144">Description</span></span> | <span data-ttu-id="861af-145">필수</span><span class="sxs-lookup"><span data-stu-id="861af-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="861af-146">type</span><span class="sxs-lookup"><span data-stu-id="861af-146">type</span></span> |<span data-ttu-id="861af-147">형식 속성은 **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="861af-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="861af-148">예</span><span class="sxs-lookup"><span data-stu-id="861af-148">Yes</span></span> |
| <span data-ttu-id="861af-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="861af-149">connectionString</span></span> |<span data-ttu-id="861af-150">connectionString 속성에 대한 Azure SQL 데이터 웨어하우스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="861af-151">기본 인증만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="861af-152">예</span><span class="sxs-lookup"><span data-stu-id="861af-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="861af-153">[Azure SQL Database 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)과 데이터베이스 서버를 구성하여 [Azure 서비스가 서버에 액세스할 수 있도록](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="861af-154">또한 데이터 팩터리 게이트웨이를 사용하여 온-프레미스 데이터 원본을 포함한 Azure 외부에서 Azure SQL 데이터 웨어하우스로 데이터를 복사하는 경우 데이터를 Azure SQL Data Warehouse로 보내는 컴퓨터에 대한 적절한 IP 주소 범위를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="861af-155">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="861af-155">Dataset properties</span></span>
<span data-ttu-id="861af-156">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="861af-157">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="861af-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="861af-158">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="861af-159">**AzureSqlDWTable** 형식의 데이터 집합에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="861af-160">속성</span><span class="sxs-lookup"><span data-stu-id="861af-160">Property</span></span> | <span data-ttu-id="861af-161">설명</span><span class="sxs-lookup"><span data-stu-id="861af-161">Description</span></span> | <span data-ttu-id="861af-162">필수</span><span class="sxs-lookup"><span data-stu-id="861af-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="861af-163">tableName</span><span class="sxs-lookup"><span data-stu-id="861af-163">tableName</span></span> |<span data-ttu-id="861af-164">연결된 서비스에서 참조하는 Azure SQL Data Warehouse 데이터베이스에 있는 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="861af-165">예</span><span class="sxs-lookup"><span data-stu-id="861af-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="861af-166">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="861af-166">Copy activity properties</span></span>
<span data-ttu-id="861af-167">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="861af-168">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="861af-169">복사 작업은 하나의 입력을 가지고 하나의 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="861af-170">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="861af-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="861af-171">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="861af-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="861af-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="861af-172">SqlDWSource</span></span>
<span data-ttu-id="861af-173">원본이 **SqlDWSource** 형식인 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="861af-174">속성</span><span class="sxs-lookup"><span data-stu-id="861af-174">Property</span></span> | <span data-ttu-id="861af-175">설명</span><span class="sxs-lookup"><span data-stu-id="861af-175">Description</span></span> | <span data-ttu-id="861af-176">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="861af-176">Allowed values</span></span> | <span data-ttu-id="861af-177">필수</span><span class="sxs-lookup"><span data-stu-id="861af-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="861af-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="861af-178">sqlReaderQuery</span></span> |<span data-ttu-id="861af-179">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-179">Use the custom query to read data.</span></span> |<span data-ttu-id="861af-180">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="861af-180">SQL query string.</span></span> <span data-ttu-id="861af-181">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="861af-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="861af-182">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-182">No</span></span> |
| <span data-ttu-id="861af-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="861af-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="861af-184">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="861af-185">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-185">Name of the stored procedure.</span></span> <span data-ttu-id="861af-186">마지막 SQL 문은 저장 프로시저의 SELECT 문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="861af-187">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-187">No</span></span> |
| <span data-ttu-id="861af-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="861af-188">storedProcedureParameters</span></span> |<span data-ttu-id="861af-189">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="861af-190">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-190">Name/value pairs.</span></span> <span data-ttu-id="861af-191">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="861af-192">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-192">No</span></span> |

<span data-ttu-id="861af-193">**sqlReaderQuery** 가 SqlDWSource에 지정되면 복사 작업은 데이터를 가져오는 Azure SQL 데이터 웨어하우스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="861af-194">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="861af-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="861af-195">sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정하지 않으면 JSON 데이터 집합의 구조 섹션에 정의된 열은 쿼리를 작성하는 데 사용되어 Azure SQL Data Warehouse에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-196">예: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="861af-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="861af-197">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="861af-198">SqlDWSource 예제</span><span class="sxs-lookup"><span data-stu-id="861af-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="861af-199">**저장 프로시저 정의:**</span><span class="sxs-lookup"><span data-stu-id="861af-199">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="861af-200">파이프라인</span><span class="sxs-lookup"><span data-stu-id="861af-200">SqlDWSink</span></span>
<span data-ttu-id="861af-201">**SqlDWSink** 는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="861af-202">속성</span><span class="sxs-lookup"><span data-stu-id="861af-202">Property</span></span> | <span data-ttu-id="861af-203">설명</span><span class="sxs-lookup"><span data-stu-id="861af-203">Description</span></span> | <span data-ttu-id="861af-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="861af-204">Allowed values</span></span> | <span data-ttu-id="861af-205">필수</span><span class="sxs-lookup"><span data-stu-id="861af-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="861af-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="861af-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="861af-207">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="861af-208">자세한 내용은 [반복성 섹션](#repeatability-during-copy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="861af-209">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-209">A query statement.</span></span> |<span data-ttu-id="861af-210">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-210">No</span></span> |
| <span data-ttu-id="861af-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="861af-211">allowPolyBase</span></span> |<span data-ttu-id="861af-212">BULKINSERT 메커니즘 대신 PolyBase(있는 경우)를 사용할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="861af-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="861af-213">**SQL Data Warehouse로 데이터를 로드하는 데 PolyBase를 사용하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="861af-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="861af-214">제약 조건 및 세부 정보는 [PolyBase를 사용하여 Azure SQL 데이터 웨어하우스로 데이터 로드](#use-polybase-to-load-data-into-azure-sql-data-warehouse) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="861af-215">True </span><span class="sxs-lookup"><span data-stu-id="861af-215">True</span></span> <br/><span data-ttu-id="861af-216">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="861af-216">False (default)</span></span> |<span data-ttu-id="861af-217">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-217">No</span></span> |
| <span data-ttu-id="861af-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="861af-218">polyBaseSettings</span></span> |<span data-ttu-id="861af-219">**allowPolybase** 속성이 **true**로 설정된 경우 지정될 수 있는 속성의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="861af-220">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-220">No</span></span> |
| <span data-ttu-id="861af-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="861af-221">rejectValue</span></span> |<span data-ttu-id="861af-222">쿼리가 실패하기 전에 거부될 수 있는 행의 수 또는 백분율을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="861af-223">**외부 테이블 만들기(Transact-SQL)** 토픽의 [인수](https://msdn.microsoft.com/library/dn935021.aspx) 섹션에 있는 PolyBase의 거부 옵션에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="861af-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="861af-224">0(기본값), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="861af-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="861af-225">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-225">No</span></span> |
| <span data-ttu-id="861af-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="861af-226">rejectType</span></span> |<span data-ttu-id="861af-227">rejectValue 옵션을 리터럴 값 또는 백분율로 지정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="861af-228">값(기본값), 백분율</span><span class="sxs-lookup"><span data-stu-id="861af-228">Value (default), Percentage</span></span> |<span data-ttu-id="861af-229">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-229">No</span></span> |
| <span data-ttu-id="861af-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="861af-230">rejectSampleValue</span></span> |<span data-ttu-id="861af-231">PolyBase가 거부된 행의 비율을 다시 계산하기 전에 검색할 행 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="861af-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="861af-232">1, 2, …</span></span> |<span data-ttu-id="861af-233">예. **rejectType**이 **백분율**인 경우</span><span class="sxs-lookup"><span data-stu-id="861af-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="861af-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="861af-234">useTypeDefault</span></span> |<span data-ttu-id="861af-235">PolyBase가 텍스트 파일에서 데이터를 검색할 경우 구분된 텍스트 파일에서 누락된 값을 처리하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="861af-236">[외부 파일 서식 만들기(Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)를 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="861af-237">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="861af-237">True, False (default)</span></span> |<span data-ttu-id="861af-238">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-238">No</span></span> |
| <span data-ttu-id="861af-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="861af-239">writeBatchSize</span></span> |<span data-ttu-id="861af-240">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="861af-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="861af-241">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="861af-241">Integer (number of rows)</span></span> |<span data-ttu-id="861af-242">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="861af-242">No (default: 10000)</span></span> |
| <span data-ttu-id="861af-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="861af-243">writeBatchTimeout</span></span> |<span data-ttu-id="861af-244">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="861af-245">timespan</span><span class="sxs-lookup"><span data-stu-id="861af-245">timespan</span></span><br/><br/> <span data-ttu-id="861af-246">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="861af-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="861af-247">아니요</span><span class="sxs-lookup"><span data-stu-id="861af-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="861af-248">SqlDWSink 예제</span><span class="sxs-lookup"><span data-stu-id="861af-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="861af-249">PolyBase를 사용하여 Azure SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="861af-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="861af-250">**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**를 사용하는 것은 처리량이 높은 많은 양의 데이터를 Azure SQL Data Warehouse에 로드하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="861af-251">기본 BULKINSERT 메커니즘 대신 PolyBase를 사용하여 처리량의 증가를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="861af-252">자세히 비교하려면 [복사 성능 참조 번호](data-factory-copy-activity-performance.md#performance-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="861af-253">사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="861af-254">원본 데이터 형식이 **Azure Blob 또는 Azure Data Lake Store**에 있고 형식이 PolyBase와 호환될 경우 PolyBase를 사용하여 Azure SQL Data Warehouse로 직접 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="861af-255">자세한 내용은 **[PolyBase를 사용하여 직접 복사](#direct-copy-using-polybase)**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="861af-256">원본 데이터 저장소와 형식이 PolyBase에서 원래 지원되지 않는 경우 대신 **[PolyBase를 사용하여 준비한 복사본](#staged-copy-using-polybase)** 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="861af-257">데이터를 PolyBase 호환 형식으로 자동으로 변환하고 Azure Blob Storage에 저장하여 향상된 처리량을 제공하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="861af-258">그런 다음 SQL Data Warehouse에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="861af-259">Azure Data Factory에 대한 다음 예와 같이 `allowPolyBase` 속성을 **true**로 설정하여 Azure SQL Data Warehouse로 데이터를 복사하기 위해 PolyBase를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-260">allowPolyBase를 true로 설정하면 `polyBaseSettings` 속성 그룹을 사용하여 PolyBase 특정 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="861af-261">polyBaseSettings에 사용할 수 있는 속성에 대한 세부 정보는 [SqlDWSink](#SqlDWSink) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="861af-262">PolyBase를 사용하여 직접 복사</span><span class="sxs-lookup"><span data-stu-id="861af-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="861af-263">SQL Data Warehouse PolyBase는 Azure Blob 및 Azure Data Lake Store(서비스 주체 사용)를 원본으로 직접 지원하며 특정 파일 형식 요구 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="861af-264">원본 데이터가 이 섹션에 설명된 조건을 충족하는 경우 PolyBase를 사용하여 원본 데이터 저장소에서 Azure SQL Data Warehouse로 직접 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="861af-265">그렇지 않을 경우, [PolyBase를 사용하여 준비한 복사본](#staged-copy-using-polybase)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="861af-266">Data Lake Store에서 SQL Data Warehouse로 데이터를 효율적으로 복사하려면 [SQL Data Warehouse와 함께 Data Lake Store를 사용할 경우 Azure Data Factory에서 데이터의 정보를 쉽고 편리하게 발견할 수 있음](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="861af-267">조건을 충족하지 않는 경우 Azure 데이터 팩터리는 설정을 확인한 후 데이터 이동을 위한 BULKINSERT 메커니즘으로 자동으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="861af-268">**원본에 연결된 서비스**의 형식은 **AzureStorage** 또는 **서비스 주체 인증이 적용된 AzureDataLakeStore**입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="861af-269">**입력 데이터 집합**은 **AzureBlob** 또는 **AzureDataLakeStore** 형식이고 `type` 속성의 서식 형식은 다음 구성이 포함된 **OrcFormat** 또는 **TextFormat**입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="861af-270">`rowDelimiter`는 **\n**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="861af-271">`nullValue`가 **빈 문자열**("")으로 설정되어 있거나 `treatEmptyAsNull`이 **true**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="861af-272">`encodingName`이 **기본값**인 **utf-8**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="861af-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` 및 `skipLineCount`는 지정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="861af-274">`compression`은 **no compression**, **GZip** 또는 **Deflate**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="861af-275">파이프라인에서 복사 작업에 대한 **BlobSource** 또는 **AzureDataLakeStore**에는 `skipHeaderLineCount` 설정이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="861af-276">파이프라인에서 복사 작업에 대한 **SqlDWSink**에는 `sliceIdentifierColumnName` 설정이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="861af-277">(PolyBase는 한 번의 실행으로 모든 데이터를 업데이트하거나 아무 것도 업데이트하지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="861af-278">**반복성**을 달성하려면 `sqlWriterCleanupScript`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="861af-279">`columnMapping`은 연결된 복사 작업에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="861af-280">PolyBase를 사용하여 준비한 복사본</span><span class="sxs-lookup"><span data-stu-id="861af-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="861af-281">원본 데이터가 이전 섹션에서 도입된 조건을 충족하지 않는 경우 일시적으로 스테이징한 Azure Blob Storage를 통해 데이터를 복사하도록 설정할 수 있습니다(Premium Storage일 수 없음).</span><span class="sxs-lookup"><span data-stu-id="861af-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="861af-282">이 경우 Azure Data Factory는 PolyBase의 데이터 형식 요구 사항을 충족시키기 위해 데이터에 변환을 수행한 다음 PolyBase를 사용하여 SQL Data Warehouse로 데이터를 로드하고 마지막으로 Blob Storage에서 임시 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="861af-283">스테이징 Azure Blob을 통해 데이터를 복사하는 방법에 대한 자세한 내용은 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="861af-284">PolyBase와 스테이징을 사용하여 온-프레미스 데이터 저장소에서 Azure SQL Data Warehouse로 데이터를 복사할 때 데이터 관리 게이트웨이 버전이 2.4 미만이면 원본 데이터를 적절한 형식으로 변환하는 데 사용되는 JRE(Java Runtime Environment)가 게이트웨이 컴퓨터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="861af-285">이러한 종속성을 방지하려면 게이트웨이를 최신으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="861af-286">이 기능을 사용하려면 중간 Blob Storage가 있는 Azure Storage 계정을 나타내는 [Azure Storage 연결된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service)를 만든 후 다음 코드에 표시된 복사 작업에 대해 `enableStaging` 및 `stagingSettings` 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="861af-287">PolyBase를 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="861af-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="861af-288">다음 섹션에서는 [Azure SQL Data Warehouse에 대한 모범 사례](../sql-data-warehouse/sql-data-warehouse-best-practices.md)에 나와 있는 추가 모범 사례를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="861af-289">필수 데이터베이스 권한</span><span class="sxs-lookup"><span data-stu-id="861af-289">Required database permission</span></span>
<span data-ttu-id="861af-290">PolyBase를 사용하려면 SQL Data Warehouse에 데이터를 로드하는 데 사용되는 사용자에게 대상 데이터베이스에 대한 ["CONTROL" 권한](https://msdn.microsoft.com/library/ms191291.aspx)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="861af-291">이를 달성하기 위한 한 가지 방법으로 해당 사용자를 "db_owner" 역할의 구성원으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="861af-292">이를 수행하는 방법에 대해서는 [이 섹션](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="861af-293">행 크기 및 데이터 형식 제한 사항</span><span class="sxs-lookup"><span data-stu-id="861af-293">Row size and data type limitation</span></span>
<span data-ttu-id="861af-294">Polybase 부하는 **1MB**보다 작고 VARCHR(MAX), NVARCHAR(MAX) 또는 VARBINARY(MAX)로 로드할 수 없는 행을 로드할 때만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="861af-295">[여기](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="861af-296">1MB보다 큰 크기의 행을 포함한 원본 데이터가 있는 경우 각 항목의 최대 행 크기가 제한을 초과하지 않는 정도의 작은 테이블로 원본 테이블을 수직으로 분할하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="861af-297">작은 테이블은 PolyBase를 사용하여 로드될 수 있고 Azure SQL 데이터 웨어하우스에서 병합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="861af-298">SQL Data Warehouse 리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="861af-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="861af-299">가능한 최상의 처리량을 달성하려면 PolyBase를 통해 SQL Data Warehouse에 데이터를 로드하는 데 사용되는 사용자에게 더 큰 리소스 클래스를 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="861af-300">[사용자 리소스 클래스 변경 예제](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)에 따라 이 작업을 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="861af-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="861af-301">Azure SQL 데이터 웨어하우스의 tableName</span><span class="sxs-lookup"><span data-stu-id="861af-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="861af-302">다음 테이블은 스키마와 테이블 이름의 다양한 조합에 대한 JSON 데이터 집합에서 **tableName** 속성을 지정하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="861af-303">DB 스키마</span><span class="sxs-lookup"><span data-stu-id="861af-303">DB Schema</span></span> | <span data-ttu-id="861af-304">테이블 이름</span><span class="sxs-lookup"><span data-stu-id="861af-304">Table name</span></span> | <span data-ttu-id="861af-305">tableName JSON 속성</span><span class="sxs-lookup"><span data-stu-id="861af-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="861af-306">dbo</span><span class="sxs-lookup"><span data-stu-id="861af-306">dbo</span></span> |<span data-ttu-id="861af-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="861af-307">MyTable</span></span> |<span data-ttu-id="861af-308">MyTable 또는 dbo.MyTable 또는 [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="861af-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="861af-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="861af-309">dbo1</span></span> |<span data-ttu-id="861af-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="861af-310">MyTable</span></span> |<span data-ttu-id="861af-311">dbo1.MyTable 또는 [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="861af-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="861af-312">dbo</span><span class="sxs-lookup"><span data-stu-id="861af-312">dbo</span></span> |<span data-ttu-id="861af-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="861af-313">My.Table</span></span> |<span data-ttu-id="861af-314">[My.Table] 또는 [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="861af-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="861af-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="861af-315">dbo1</span></span> |<span data-ttu-id="861af-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="861af-316">My.Table</span></span> |<span data-ttu-id="861af-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="861af-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="861af-318">다음 오류가 표시하는 경우 tableName 속성에 지정한 값에 관한 문제일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="861af-319">tableName JSON 속성에 대한 값을 지정하는 올바른 방법은 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="861af-320">기본값이 있는 열</span><span class="sxs-lookup"><span data-stu-id="861af-320">Columns with default values</span></span>
<span data-ttu-id="861af-321">현재 데이터 팩터리의 PolyBase 기능은 대상 테이블과 동일한 열 수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="861af-322">가령 네 개의 열이 있고 그 중 한 열이 기본 값으로 정의된 테이블이 있다고 합시다.</span><span class="sxs-lookup"><span data-stu-id="861af-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="861af-323">입력 데이터는 여전히 네 개의 열을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-323">The input data should still contain four columns.</span></span> <span data-ttu-id="861af-324">3열 입력 데이터 집합을 제공하면 다음 메시지와 비슷한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="861af-325">NULL 값은 특별한 형태의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="861af-326">열이 null을 허용하면 해당 열에 대한 입력 데이터(Blob)는 비어 있을 수 있습니다(입력 데이터 집합에서 누락될 수 없음).</span><span class="sxs-lookup"><span data-stu-id="861af-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="861af-327">PolyBase는 Azure SQL Data Warehouse의 해당 항목에 NULL을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="861af-328">자동 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="861af-328">Auto table creation</span></span>
<span data-ttu-id="861af-329">복사 마법사를 사용하여 SQL Server 또는 Azure SQL Database에서 Azure SQL Data Warehouse로 데이터를 복사하는 경우 원본 테이블에 해당하는 테이블이 대상 저장소에 없으면 Data Factory는 원본 테이블 스키마를 사용하여 데이터 웨어하우스에 테이블을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="861af-330">Data Factory는 원본 데이터 저장소와 동일한 테이블 이름으로 대상 저장소에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="861af-331">열에 대한 데이터 형식은 다음 형식 매핑을 기반으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="861af-332">필요한 경우 원본과 대상 저장소 사이의 비호환성을 해결하기 위해 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="861af-333">라운드 로빈 테이블 배포를 사용하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="861af-334">원본 SQL Database 열 형식</span><span class="sxs-lookup"><span data-stu-id="861af-334">Source SQL Database column type</span></span> | <span data-ttu-id="861af-335">대상 SQL DW 열 유형(크기 제한)</span><span class="sxs-lookup"><span data-stu-id="861af-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="861af-336">int</span><span class="sxs-lookup"><span data-stu-id="861af-336">Int</span></span> | <span data-ttu-id="861af-337">int</span><span class="sxs-lookup"><span data-stu-id="861af-337">Int</span></span> |
| <span data-ttu-id="861af-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="861af-338">BigInt</span></span> | <span data-ttu-id="861af-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="861af-339">BigInt</span></span> |
| <span data-ttu-id="861af-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="861af-340">SmallInt</span></span> | <span data-ttu-id="861af-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="861af-341">SmallInt</span></span> |
| <span data-ttu-id="861af-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="861af-342">TinyInt</span></span> | <span data-ttu-id="861af-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="861af-343">TinyInt</span></span> |
| <span data-ttu-id="861af-344">Bit</span><span class="sxs-lookup"><span data-stu-id="861af-344">Bit</span></span> | <span data-ttu-id="861af-345">Bit</span><span class="sxs-lookup"><span data-stu-id="861af-345">Bit</span></span> |
| <span data-ttu-id="861af-346">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-346">Decimal</span></span> | <span data-ttu-id="861af-347">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-347">Decimal</span></span> |
| <span data-ttu-id="861af-348">숫자</span><span class="sxs-lookup"><span data-stu-id="861af-348">Numeric</span></span> | <span data-ttu-id="861af-349">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-349">Decimal</span></span> |
| <span data-ttu-id="861af-350">Float</span><span class="sxs-lookup"><span data-stu-id="861af-350">Float</span></span> | <span data-ttu-id="861af-351">Float</span><span class="sxs-lookup"><span data-stu-id="861af-351">Float</span></span> |
| <span data-ttu-id="861af-352">Money</span><span class="sxs-lookup"><span data-stu-id="861af-352">Money</span></span> | <span data-ttu-id="861af-353">Money</span><span class="sxs-lookup"><span data-stu-id="861af-353">Money</span></span> |
| <span data-ttu-id="861af-354">Real</span><span class="sxs-lookup"><span data-stu-id="861af-354">Real</span></span> | <span data-ttu-id="861af-355">Real</span><span class="sxs-lookup"><span data-stu-id="861af-355">Real</span></span> |
| <span data-ttu-id="861af-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="861af-356">SmallMoney</span></span> | <span data-ttu-id="861af-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="861af-357">SmallMoney</span></span> |
| <span data-ttu-id="861af-358">이진</span><span class="sxs-lookup"><span data-stu-id="861af-358">Binary</span></span> | <span data-ttu-id="861af-359">이진</span><span class="sxs-lookup"><span data-stu-id="861af-359">Binary</span></span> |
| <span data-ttu-id="861af-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="861af-360">Varbinary</span></span> | <span data-ttu-id="861af-361">Varbinary(최대 8000)</span><span class="sxs-lookup"><span data-stu-id="861af-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="861af-362">Date</span><span class="sxs-lookup"><span data-stu-id="861af-362">Date</span></span> | <span data-ttu-id="861af-363">Date</span><span class="sxs-lookup"><span data-stu-id="861af-363">Date</span></span> |
| <span data-ttu-id="861af-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-364">DateTime</span></span> | <span data-ttu-id="861af-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-365">DateTime</span></span> |
| <span data-ttu-id="861af-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="861af-366">DateTime2</span></span> | <span data-ttu-id="861af-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="861af-367">DateTime2</span></span> |
| <span data-ttu-id="861af-368">Time</span><span class="sxs-lookup"><span data-stu-id="861af-368">Time</span></span> | <span data-ttu-id="861af-369">Time</span><span class="sxs-lookup"><span data-stu-id="861af-369">Time</span></span> |
| <span data-ttu-id="861af-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="861af-370">DateTimeOffset</span></span> | <span data-ttu-id="861af-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="861af-371">DateTimeOffset</span></span> |
| <span data-ttu-id="861af-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="861af-372">SmallDateTime</span></span> | <span data-ttu-id="861af-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="861af-373">SmallDateTime</span></span> |
| <span data-ttu-id="861af-374">텍스트</span><span class="sxs-lookup"><span data-stu-id="861af-374">Text</span></span> | <span data-ttu-id="861af-375">Varchar(최대 8000)</span><span class="sxs-lookup"><span data-stu-id="861af-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="861af-376">NText</span><span class="sxs-lookup"><span data-stu-id="861af-376">NText</span></span> | <span data-ttu-id="861af-377">NVarChar(최대 4000)</span><span class="sxs-lookup"><span data-stu-id="861af-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="861af-378">이미지</span><span class="sxs-lookup"><span data-stu-id="861af-378">Image</span></span> | <span data-ttu-id="861af-379">VarBinary(최대 8000)</span><span class="sxs-lookup"><span data-stu-id="861af-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="861af-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="861af-380">UniqueIdentifier</span></span> | <span data-ttu-id="861af-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="861af-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="861af-382">Char</span><span class="sxs-lookup"><span data-stu-id="861af-382">Char</span></span> | <span data-ttu-id="861af-383">Char</span><span class="sxs-lookup"><span data-stu-id="861af-383">Char</span></span> |
| <span data-ttu-id="861af-384">NChar</span><span class="sxs-lookup"><span data-stu-id="861af-384">NChar</span></span> | <span data-ttu-id="861af-385">NChar</span><span class="sxs-lookup"><span data-stu-id="861af-385">NChar</span></span> |
| <span data-ttu-id="861af-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="861af-386">VarChar</span></span> | <span data-ttu-id="861af-387">VarChar(최대 8000)</span><span class="sxs-lookup"><span data-stu-id="861af-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="861af-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="861af-388">NVarChar</span></span> | <span data-ttu-id="861af-389">NVarChar(최대 4000)</span><span class="sxs-lookup"><span data-stu-id="861af-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="861af-390">xml</span><span class="sxs-lookup"><span data-stu-id="861af-390">Xml</span></span> | <span data-ttu-id="861af-391">Varchar(최대 8000)</span><span class="sxs-lookup"><span data-stu-id="861af-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="861af-392">Azure SQL 데이터 웨어하우스에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="861af-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="861af-393">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="861af-394">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="861af-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="861af-395">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="861af-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="861af-396">Azure SQL Data Warehouse 간에 데이터를 이동할 때는 다음과 같은 매핑이 SQL 형식에서 .NET 형식으로 또는 그 반대로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="861af-397">매핑은 [ADO.NET에 대한 SQL Server 데이터 형식 매핑](https://msdn.microsoft.com/library/cc716729.aspx)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="861af-398">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="861af-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="861af-399">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="861af-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="861af-400">bigint</span><span class="sxs-lookup"><span data-stu-id="861af-400">bigint</span></span> |<span data-ttu-id="861af-401">Int64</span><span class="sxs-lookup"><span data-stu-id="861af-401">Int64</span></span> |
| <span data-ttu-id="861af-402">binary</span><span class="sxs-lookup"><span data-stu-id="861af-402">binary</span></span> |<span data-ttu-id="861af-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-403">Byte[]</span></span> |
| <span data-ttu-id="861af-404">bit</span><span class="sxs-lookup"><span data-stu-id="861af-404">bit</span></span> |<span data-ttu-id="861af-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="861af-405">Boolean</span></span> |
| <span data-ttu-id="861af-406">char</span><span class="sxs-lookup"><span data-stu-id="861af-406">char</span></span> |<span data-ttu-id="861af-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-407">String, Char[]</span></span> |
| <span data-ttu-id="861af-408">date</span><span class="sxs-lookup"><span data-stu-id="861af-408">date</span></span> |<span data-ttu-id="861af-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-409">DateTime</span></span> |
| <span data-ttu-id="861af-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-410">Datetime</span></span> |<span data-ttu-id="861af-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-411">DateTime</span></span> |
| <span data-ttu-id="861af-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="861af-412">datetime2</span></span> |<span data-ttu-id="861af-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-413">DateTime</span></span> |
| <span data-ttu-id="861af-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="861af-414">Datetimeoffset</span></span> |<span data-ttu-id="861af-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="861af-415">DateTimeOffset</span></span> |
| <span data-ttu-id="861af-416">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-416">Decimal</span></span> |<span data-ttu-id="861af-417">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-417">Decimal</span></span> |
| <span data-ttu-id="861af-418">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="861af-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="861af-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-419">Byte[]</span></span> |
| <span data-ttu-id="861af-420">Float</span><span class="sxs-lookup"><span data-stu-id="861af-420">Float</span></span> |<span data-ttu-id="861af-421">Double</span><span class="sxs-lookup"><span data-stu-id="861af-421">Double</span></span> |
| <span data-ttu-id="861af-422">이미지</span><span class="sxs-lookup"><span data-stu-id="861af-422">image</span></span> |<span data-ttu-id="861af-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-423">Byte[]</span></span> |
| <span data-ttu-id="861af-424">int</span><span class="sxs-lookup"><span data-stu-id="861af-424">int</span></span> |<span data-ttu-id="861af-425">Int32</span><span class="sxs-lookup"><span data-stu-id="861af-425">Int32</span></span> |
| <span data-ttu-id="861af-426">money</span><span class="sxs-lookup"><span data-stu-id="861af-426">money</span></span> |<span data-ttu-id="861af-427">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-427">Decimal</span></span> |
| <span data-ttu-id="861af-428">nchar</span><span class="sxs-lookup"><span data-stu-id="861af-428">nchar</span></span> |<span data-ttu-id="861af-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-429">String, Char[]</span></span> |
| <span data-ttu-id="861af-430">ntext</span><span class="sxs-lookup"><span data-stu-id="861af-430">ntext</span></span> |<span data-ttu-id="861af-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-431">String, Char[]</span></span> |
| <span data-ttu-id="861af-432">numeric</span><span class="sxs-lookup"><span data-stu-id="861af-432">numeric</span></span> |<span data-ttu-id="861af-433">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-433">Decimal</span></span> |
| <span data-ttu-id="861af-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="861af-434">nvarchar</span></span> |<span data-ttu-id="861af-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-435">String, Char[]</span></span> |
| <span data-ttu-id="861af-436">real</span><span class="sxs-lookup"><span data-stu-id="861af-436">real</span></span> |<span data-ttu-id="861af-437">단일</span><span class="sxs-lookup"><span data-stu-id="861af-437">Single</span></span> |
| <span data-ttu-id="861af-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="861af-438">rowversion</span></span> |<span data-ttu-id="861af-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-439">Byte[]</span></span> |
| <span data-ttu-id="861af-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="861af-440">smalldatetime</span></span> |<span data-ttu-id="861af-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="861af-441">DateTime</span></span> |
| <span data-ttu-id="861af-442">smallint</span><span class="sxs-lookup"><span data-stu-id="861af-442">smallint</span></span> |<span data-ttu-id="861af-443">Int16</span><span class="sxs-lookup"><span data-stu-id="861af-443">Int16</span></span> |
| <span data-ttu-id="861af-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="861af-444">smallmoney</span></span> |<span data-ttu-id="861af-445">10진수</span><span class="sxs-lookup"><span data-stu-id="861af-445">Decimal</span></span> |
| <span data-ttu-id="861af-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="861af-446">sql_variant</span></span> |<span data-ttu-id="861af-447">개체 *</span><span class="sxs-lookup"><span data-stu-id="861af-447">Object *</span></span> |
| <span data-ttu-id="861af-448">텍스트</span><span class="sxs-lookup"><span data-stu-id="861af-448">text</span></span> |<span data-ttu-id="861af-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-449">String, Char[]</span></span> |
| <span data-ttu-id="861af-450">실시간</span><span class="sxs-lookup"><span data-stu-id="861af-450">time</span></span> |<span data-ttu-id="861af-451">timespan</span><span class="sxs-lookup"><span data-stu-id="861af-451">TimeSpan</span></span> |
| <span data-ttu-id="861af-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="861af-452">timestamp</span></span> |<span data-ttu-id="861af-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-453">Byte[]</span></span> |
| <span data-ttu-id="861af-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="861af-454">tinyint</span></span> |<span data-ttu-id="861af-455">Byte</span><span class="sxs-lookup"><span data-stu-id="861af-455">Byte</span></span> |
| <span data-ttu-id="861af-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="861af-456">uniqueidentifier</span></span> |<span data-ttu-id="861af-457">Guid</span><span class="sxs-lookup"><span data-stu-id="861af-457">Guid</span></span> |
| <span data-ttu-id="861af-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="861af-458">varbinary</span></span> |<span data-ttu-id="861af-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="861af-459">Byte[]</span></span> |
| <span data-ttu-id="861af-460">varchar</span><span class="sxs-lookup"><span data-stu-id="861af-460">varchar</span></span> |<span data-ttu-id="861af-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="861af-461">String, Char[]</span></span> |
| <span data-ttu-id="861af-462">xml</span><span class="sxs-lookup"><span data-stu-id="861af-462">xml</span></span> |<span data-ttu-id="861af-463">Xml</span><span class="sxs-lookup"><span data-stu-id="861af-463">Xml</span></span> |

<span data-ttu-id="861af-464">복사 작업 정의에서 원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="861af-465">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="861af-466">SQL Data Warehouse로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="861af-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="861af-467">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="861af-468">Azure SQL 데이터 웨어하우스 및 Blob 저장소 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="861af-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="861af-469">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="861af-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="861af-470">예제: Azure SQL Data Warehouse에서 Azure Blob에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="861af-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="861af-471">샘플이 다음 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="861af-472">[AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="861af-473">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="861af-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="861af-474">[AzureSqlDWTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="861af-475">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="861af-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="861af-476">[SqlDWSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="861af-477">샘플은 Azure SQL Data Warehouse의 테이블에서 Blob으로 (매시간, 매일 등) 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="861af-478">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="861af-479">**Azure SQL 데이터 웨어하우스 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="861af-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="861af-480">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="861af-480">**Azure Blob storage linked service:**</span></span>

```JSON
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
<span data-ttu-id="861af-481">**Azure SQL 데이터 웨어하우스 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="861af-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="861af-482">샘플은 Azure SQL 데이터 웨어하우스에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn" 라는 열이 포함되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="861af-483">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="861af-484">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="861af-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="861af-485">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="861af-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="861af-486">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="861af-487">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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

<span data-ttu-id="861af-488">**SqlDWSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="861af-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="861af-489">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="861af-490">파이프라인 JSON 정의에서 **source** 형식은 **SqlDWSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="861af-491">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> <span data-ttu-id="861af-492">예에서 **sqlReaderQuery**는 SqlDWSource에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="861af-493">복사 작업은 데이터를 가져오는 Azure SQL 데이터 웨어하우스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="861af-494">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="861af-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="861af-495">sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정하지 않으면 JSON 데이터 집합의 구조 섹션에 정의된 열은 쿼리를 작성하는 데 사용되어 Azure SQL 데이터 웨어하우스에 대해 실행합니다.(mytable에서 column1, column2 선택)</span><span class="sxs-lookup"><span data-stu-id="861af-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-496">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="861af-497">예제: Azure Blob에서 Azure SQL Data Warehouse에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="861af-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="861af-498">샘플이 다음 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="861af-499">[AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="861af-500">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="861af-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="861af-501">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="861af-502">[AzureSqlDWTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="861af-503">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlDWSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="861af-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="861af-504">샘플은 Azure blob에서 Azure SQL Data Warehouse의 테이블로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="861af-505">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="861af-506">**Azure SQL 데이터 웨어하우스 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="861af-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="861af-507">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="861af-507">**Azure Blob storage linked service:**</span></span>

```JSON
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
<span data-ttu-id="861af-508">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="861af-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="861af-509">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="861af-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="861af-510">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="861af-511">폴더 경로는 연도, 월 및 일 일부 시작 시간을 사용하고 파일 이름은 시작 시간의 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="861af-512">"external": "true" 설정은 데이터 팩터리 서비스에 이 테이블이 데이터 팩터리의 외부에 있으며 데이터 팩터리의 작업에 의해 생성되지 않는다는 점을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="861af-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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
<span data-ttu-id="861af-513">**Azure SQL 데이터 웨어하우스 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="861af-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="861af-514">샘플은 Azure SQL 데이터 웨어하우스의 "MyTable"이라는 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="861af-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="861af-515">Blob CSV 파일을 포함하려 하면 같은 수의 열을 사용하여 Azure SQL Data Warehouse의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="861af-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="861af-516">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-516">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="861af-517">**BlobSource 및 SqlDWSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="861af-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="861af-518">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="861af-519">파이프라인 JSON 정의에서 **source** 형식은 **BlobSource**로 설정되고 **sink** 형식은 **SqlDWSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="861af-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="861af-520">연습을 진행하려면 Azure SQL Data Warehouse 설명서에서 [Azure Data Factory를 사용하여 15분 내에 Azure SQL Data Warehouse에 1TB 로드](data-factory-load-sql-data-warehouse.md) 및 [Azure Data Factory를 사용하여 데이터 로드](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="861af-521">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="861af-521">Performance and Tuning</span></span>
<span data-ttu-id="861af-522">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="861af-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
