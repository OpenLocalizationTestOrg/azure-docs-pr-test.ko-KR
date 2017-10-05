---
title: "Azure 테이블 간 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Azure 테이블 저장소 간 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="435b5-103">Azure Data Factory를 사용하여 Azure 테이블 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="435b5-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="435b5-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure Table Storage 간에 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="435b5-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="435b5-106">모든 지원되는 원본 데이터 저장소에서 Azure Table Storage로 또는 Azure Blob Storage에서 모든 지원되는 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="435b5-107">복사 작업의 원본 또는 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="435b5-108">시작</span><span class="sxs-lookup"><span data-stu-id="435b5-108">Getting started</span></span>
<span data-ttu-id="435b5-109">다른 도구/API를 사용하여 Azure Table Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="435b5-110">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="435b5-111">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="435b5-112">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="435b5-113">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="435b5-114">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="435b5-115">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="435b5-116">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="435b5-117">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="435b5-118">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="435b5-119">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="435b5-120">다른 곳에서 Azure Table Storage로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="435b5-121">다음 섹션에서는 Azure Table Storage에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="435b5-122">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="435b5-122">Linked service properties</span></span>
<span data-ttu-id="435b5-123">Azure Blob 저장소를 Azure Data Factory에 연결하는 데 사용할 수 있는 두 가지 유형의 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="435b5-124">**AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="435b5-125">Azure 저장소 연결된 서비스는 Azure 저장소에 대한 전역 액세스로 Data Factory를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="435b5-126">반면 Azure 저장소 SAS(공유 액세스 서명) 연결된 서비스는 Azure 저장소에 대한 제한/시간 제한 액세스로 Data Factory를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="435b5-127">이 두 연결된 서비스에는 다른 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="435b5-128">필요에 맞는 연결된 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="435b5-129">다음 섹션에서는 이러한 두 연결된 서비스에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="435b5-130">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="435b5-130">Dataset properties</span></span>
<span data-ttu-id="435b5-131">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="435b5-132">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="435b5-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="435b5-133">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="435b5-134">**AzureTable** 데이터 집합 형식에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="435b5-135">속성</span><span class="sxs-lookup"><span data-stu-id="435b5-135">Property</span></span> | <span data-ttu-id="435b5-136">설명</span><span class="sxs-lookup"><span data-stu-id="435b5-136">Description</span></span> | <span data-ttu-id="435b5-137">필수</span><span class="sxs-lookup"><span data-stu-id="435b5-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="435b5-138">tableName</span><span class="sxs-lookup"><span data-stu-id="435b5-138">tableName</span></span> |<span data-ttu-id="435b5-139">연결된 서비스가 참조하는 Azure 테이블 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="435b5-140">예.</span><span class="sxs-lookup"><span data-stu-id="435b5-140">Yes.</span></span> <span data-ttu-id="435b5-141">azureTableSourceQuery 없이 tableName을 지정하면 테이블의 모든 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="435b5-142">또한 azureTableSourceQuery를 지정하면 쿼리를 만족 하는 테이블의 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="435b5-143">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="435b5-143">Schema by Data Factory</span></span>
<span data-ttu-id="435b5-144">Azure 테이블과 같은 스키마 없는 데이터 저장소의 경우 Data Factory 서비스는 다음 방법 중 하나로 스키마를 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="435b5-145">데이터 집합 정의에서 **구조** 속성을 사용하여 데이터의 구조를 지정하는 경우 Data Factory 서비스는 이 구조를 스키마로 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="435b5-146">이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="435b5-147">데이터 집합 정의에서 **구조** 속성을 사용하여 데이터의 구조를 지정하지 않는 경우 Data Factory는 데이터의 첫 번째 행을 사용하여 스키마를 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="435b5-148">이 경우 첫 번째 행에 전체 스키마가 포함되어 있지 않으면 일부 열이 복사 작업의 결과에서 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="435b5-149">따라서 스키마 없는 데이터 원본에 대한 모범 사례는 **구조** 속성을 사용하여 데이터의 구조를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="435b5-150">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="435b5-150">Copy activity properties</span></span>
<span data-ttu-id="435b5-151">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="435b5-152">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="435b5-153">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="435b5-154">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="435b5-155">**AzureTableSource** 는 typeProperties 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="435b5-156">속성</span><span class="sxs-lookup"><span data-stu-id="435b5-156">Property</span></span> | <span data-ttu-id="435b5-157">설명</span><span class="sxs-lookup"><span data-stu-id="435b5-157">Description</span></span> | <span data-ttu-id="435b5-158">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="435b5-158">Allowed values</span></span> | <span data-ttu-id="435b5-159">필수</span><span class="sxs-lookup"><span data-stu-id="435b5-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="435b5-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="435b5-160">azureTableSourceQuery</span></span> |<span data-ttu-id="435b5-161">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-161">Use the custom query to read data.</span></span> |<span data-ttu-id="435b5-162">Azure 테이블 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="435b5-162">Azure table query string.</span></span> <span data-ttu-id="435b5-163">다음 섹션의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-163">See examples in the next section.</span></span> |<span data-ttu-id="435b5-164">아니요.</span><span class="sxs-lookup"><span data-stu-id="435b5-164">No.</span></span> <span data-ttu-id="435b5-165">azureTableSourceQuery 없이 tableName을 지정하면 테이블의 모든 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="435b5-166">또한 azureTableSourceQuery를 지정하면 쿼리를 만족 하는 테이블의 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="435b5-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="435b5-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="435b5-168">존재하지 않는 테이블의 예외를 받아들이는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="435b5-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="435b5-169">TRUE</span></span><br/><span data-ttu-id="435b5-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="435b5-170">FALSE</span></span> |<span data-ttu-id="435b5-171">아니요</span><span class="sxs-lookup"><span data-stu-id="435b5-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="435b5-172">azureTableSourceQuery 예제</span><span class="sxs-lookup"><span data-stu-id="435b5-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="435b5-173">Azure 테이블 열이 문자열 형식인 경우:</span><span class="sxs-lookup"><span data-stu-id="435b5-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="435b5-174">Azure 테이블 열이 날짜/시간 형식인 경우:</span><span class="sxs-lookup"><span data-stu-id="435b5-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="435b5-175">**AzureTableSink** 는 typeProperties 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="435b5-176">속성</span><span class="sxs-lookup"><span data-stu-id="435b5-176">Property</span></span> | <span data-ttu-id="435b5-177">설명</span><span class="sxs-lookup"><span data-stu-id="435b5-177">Description</span></span> | <span data-ttu-id="435b5-178">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="435b5-178">Allowed values</span></span> | <span data-ttu-id="435b5-179">필수</span><span class="sxs-lookup"><span data-stu-id="435b5-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="435b5-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="435b5-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="435b5-181">싱크에서 사용할 수 있는 기본 파티션 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="435b5-182">문자열 값</span><span class="sxs-lookup"><span data-stu-id="435b5-182">A string value.</span></span> |<span data-ttu-id="435b5-183">아니요</span><span class="sxs-lookup"><span data-stu-id="435b5-183">No</span></span> |
| <span data-ttu-id="435b5-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="435b5-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="435b5-185">해당 값이 파티션 키로 사용되는 열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="435b5-186">지정하지 않으면 AzureTableDefaultPartitionKeyValue가 파티션 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="435b5-187">열 이름</span><span class="sxs-lookup"><span data-stu-id="435b5-187">A column name.</span></span> |<span data-ttu-id="435b5-188">아니요</span><span class="sxs-lookup"><span data-stu-id="435b5-188">No</span></span> |
| <span data-ttu-id="435b5-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="435b5-189">azureTableRowKeyName</span></span> |<span data-ttu-id="435b5-190">해당 열 값이 행 키로 사용되는 열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="435b5-191">지정하지 않으면 각 행에 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="435b5-192">열 이름</span><span class="sxs-lookup"><span data-stu-id="435b5-192">A column name.</span></span> |<span data-ttu-id="435b5-193">아니요</span><span class="sxs-lookup"><span data-stu-id="435b5-193">No</span></span> |
| <span data-ttu-id="435b5-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="435b5-194">azureTableInsertType</span></span> |<span data-ttu-id="435b5-195">Azure 테이블에 데이터를 삽입하는 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="435b5-196">이 속성은 출력 테이블에서 파티션 및 행 키가 일치하는 기존 행의 값을 바꿀지 또는 병합할지 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="435b5-197">이러한 설정(병합 및 바꾸기)이 작동하는 방법을 알아보려면 [엔터티 삽입 또는 병합](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [엔터티 삽입 또는 바꾸기](https://msdn.microsoft.com/library/azure/hh452242.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="435b5-198">이 설정은 테이블 수준이 아니라 행 수준에서 적용되며, 두 옵션 모두 출력 테이블에서 입력에 존재하지 않는 행을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="435b5-199">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="435b5-199">merge (default)</span></span><br/><span data-ttu-id="435b5-200">바꾸기</span><span class="sxs-lookup"><span data-stu-id="435b5-200">replace</span></span> |<span data-ttu-id="435b5-201">아니요</span><span class="sxs-lookup"><span data-stu-id="435b5-201">No</span></span> |
| <span data-ttu-id="435b5-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="435b5-202">writeBatchSize</span></span> |<span data-ttu-id="435b5-203">WriteBatchSize 또는 writeBatchTimeout에 도달하면 Azure 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="435b5-204">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="435b5-204">Integer (number of rows)</span></span> |<span data-ttu-id="435b5-205">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="435b5-205">No (default: 10000)</span></span> |
| <span data-ttu-id="435b5-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="435b5-206">writeBatchTimeout</span></span> |<span data-ttu-id="435b5-207">WriteBatchSize 또는 writeBatchTimeout에 도달하면 Azure 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="435b5-208">timespan</span><span class="sxs-lookup"><span data-stu-id="435b5-208">timespan</span></span><br/><br/><span data-ttu-id="435b5-209">예: "00:20:00"(20분)</span><span class="sxs-lookup"><span data-stu-id="435b5-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="435b5-210">No (기본적으로 저장소 클라이언트 기본 시간 제한 값인 90초로 설정)</span><span class="sxs-lookup"><span data-stu-id="435b5-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="435b5-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="435b5-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="435b5-212">대상 열을 azureTablePartitionKeyName으로 사용할 수 있기 전에 JSON 속성 변환기를 사용하여 원본 열을 대상 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="435b5-213">다음 예제에서 원본 열 DivisionID은 대상 열 DivisionID에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="435b5-214">DivisionID는 파티션 키로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="435b5-215">JSON 예</span><span class="sxs-lookup"><span data-stu-id="435b5-215">JSON examples</span></span>
<span data-ttu-id="435b5-216">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="435b5-217">Azure 테이블 저장소 및 Azure Blob 데이터베이스 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="435b5-218">그러나 임의의 원본에서 지원되는 싱크로 **직접** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="435b5-219">자세한 내용은 [복사 작업을 사용하여 데이터 이동](data-factory-data-movement-activities.md)에서 "지원되는 데이터 저장소 및 형식" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="435b5-220">예제: Azure 테이블에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="435b5-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="435b5-221">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-221">The following sample shows:</span></span>

1. <span data-ttu-id="435b5-222">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)</span><span class="sxs-lookup"><span data-stu-id="435b5-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="435b5-223">[AzureTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="435b5-224">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="435b5-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="435b5-225">[AzureTableSource](#activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="435b5-226">샘플은 매시간 Azure 테이블의 기본 파티션에 속하는 데이터를 blob로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="435b5-227">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="435b5-228">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="435b5-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="435b5-229">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="435b5-230">첫 번째 것의 경우 계정 키를 포함하는 연결 문자열을 지정하고 이후 것의 경우 SAS(공유 액세스 서명) Uri를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="435b5-231">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="435b5-232">**Azure 테이블 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="435b5-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="435b5-233">샘플은 Azure 테이블에 "MyTable" 테이블을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="435b5-234">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="435b5-235">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="435b5-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="435b5-236">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="435b5-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="435b5-237">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="435b5-238">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="435b5-239">**AzureTableSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="435b5-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="435b5-240">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="435b5-241">파이프라인 JSON 정의에서 **source** 형식은 **AzureTableSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="435b5-242">**AzureTableSourceQuery** 속성으로 지정된 SQL 쿼리는 매시간 기본 파티션에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="435b5-243">예제: Azure Blob에서 Azure 테이블로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="435b5-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="435b5-244">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-244">The following sample shows:</span></span>

1. <span data-ttu-id="435b5-245">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)</span><span class="sxs-lookup"><span data-stu-id="435b5-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="435b5-246">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="435b5-247">[AzureTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="435b5-248">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureTableSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="435b5-249">샘플은 Azure Blob에서 Azure 테이블로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="435b5-250">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="435b5-251">**Azure 저장소 연결된 서비스(Azure 테이블 및 Blob용):**</span><span class="sxs-lookup"><span data-stu-id="435b5-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="435b5-252">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="435b5-253">첫 번째 것의 경우 계정 키를 포함하는 연결 문자열을 지정하고 이후 것의 경우 SAS(공유 액세스 서명) Uri를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="435b5-254">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="435b5-255">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="435b5-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="435b5-256">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="435b5-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="435b5-257">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="435b5-258">폴더 경로에는 시작 시간의 년/월/일 부분이 사용되고 파일 이름에는 시작 시간의 시간 부분이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="435b5-259">"external": "true" 설정을 사용하는 경우 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="435b5-260">**Azure 테이블 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="435b5-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="435b5-261">샘플은 Azure 테이블의 "MyTable"이라는 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="435b5-262">Blob CSV 파일을 포함하려 하면 같은 수의 열을 사용하여 Azure 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="435b5-263">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-263">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="435b5-264">**BlobSource 및 AzureTableSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="435b5-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="435b5-265">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="435b5-266">파이프라인 JSON 정의에서 **source** 형식은 **BlobSource**로 설정되고 **sink** 형식은 **AzureTableSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="435b5-267">Azure 테이블에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="435b5-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="435b5-268">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="435b5-269">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="435b5-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="435b5-270">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="435b5-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="435b5-271">Azure 테이블에서 데이터를 이동하는 경우 다음 [Azure 테이블 서비스에서 정의된 매핑](https://msdn.microsoft.com/library/azure/dd179338.aspx)은 Azure 테이블 OData 형식에서 .NET 유형에 또는 그 반대로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="435b5-272">OData 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="435b5-272">OData Data Type</span></span> | <span data-ttu-id="435b5-273">.NET 형식</span><span class="sxs-lookup"><span data-stu-id="435b5-273">.NET Type</span></span> | <span data-ttu-id="435b5-274">세부 정보</span><span class="sxs-lookup"><span data-stu-id="435b5-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="435b5-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="435b5-275">Edm.Binary</span></span> |<span data-ttu-id="435b5-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="435b5-276">byte[]</span></span> |<span data-ttu-id="435b5-277">바이트 배열은 최대 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="435b5-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="435b5-278">Edm.Boolean</span></span> |<span data-ttu-id="435b5-279">bool</span><span class="sxs-lookup"><span data-stu-id="435b5-279">bool</span></span> |<span data-ttu-id="435b5-280">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-280">A Boolean value.</span></span> |
| <span data-ttu-id="435b5-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="435b5-281">Edm.DateTime</span></span> |<span data-ttu-id="435b5-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="435b5-282">DateTime</span></span> |<span data-ttu-id="435b5-283">UTC(협정 세계시)로 표현되는 64비트 값입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="435b5-284">지원되는 DateTime 범위는 서기 1601년 1월 1일 자정 12시부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="435b5-285">(서기), UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-285">(C.E.), UTC.</span></span> <span data-ttu-id="435b5-286">범위는 9999년 12월 31일에 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="435b5-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="435b5-287">Edm.Double</span></span> |<span data-ttu-id="435b5-288">double</span><span class="sxs-lookup"><span data-stu-id="435b5-288">double</span></span> |<span data-ttu-id="435b5-289">64비트 부동 소수점 값입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="435b5-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="435b5-290">Edm.Guid</span></span> |<span data-ttu-id="435b5-291">Guid</span><span class="sxs-lookup"><span data-stu-id="435b5-291">Guid</span></span> |<span data-ttu-id="435b5-292">전역적으로 고유한 128 비트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="435b5-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="435b5-293">Edm.Int32</span></span> |<span data-ttu-id="435b5-294">Int32</span><span class="sxs-lookup"><span data-stu-id="435b5-294">Int32</span></span> |<span data-ttu-id="435b5-295">32비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="435b5-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="435b5-296">Edm.Int64</span></span> |<span data-ttu-id="435b5-297">Int64</span><span class="sxs-lookup"><span data-stu-id="435b5-297">Int64</span></span> |<span data-ttu-id="435b5-298">64비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="435b5-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="435b5-299">Edm.String</span></span> |<span data-ttu-id="435b5-300">문자열</span><span class="sxs-lookup"><span data-stu-id="435b5-300">String</span></span> |<span data-ttu-id="435b5-301">UTF-16으로 인코딩된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="435b5-302">문자열 값은 최대 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="435b5-303">형식 변환 샘플</span><span class="sxs-lookup"><span data-stu-id="435b5-303">Type Conversion Sample</span></span>
<span data-ttu-id="435b5-304">다음 샘플은 Azure Blob에서 형식 변환이 있는 Azure 테이블에 데이터를 복사하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="435b5-305">Blob 데이터 집합이 CSV 형식이며 3개의 열을 포함하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="435b5-306">그 중 하나는 요일에 축약된 프랑스 이름을 사용하여 사용자 지정 datetime 형식을 사용하는 datetime 열입니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="435b5-307">열에 대한 형식 정의가 다음과 같으면 Blob 원본 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="435b5-308">Azure 테이블 OData 형식에서 .NET 형식에 형식 매핑을 지정하면 다음 스키마로 Azure 테이블에서 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="435b5-309">**Azure 테이블 스키마:**</span><span class="sxs-lookup"><span data-stu-id="435b5-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="435b5-310">열 이름</span><span class="sxs-lookup"><span data-stu-id="435b5-310">Column name</span></span> | <span data-ttu-id="435b5-311">형식</span><span class="sxs-lookup"><span data-stu-id="435b5-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="435b5-312">userid</span><span class="sxs-lookup"><span data-stu-id="435b5-312">userid</span></span> |<span data-ttu-id="435b5-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="435b5-313">Edm.Int64</span></span> |
| <span data-ttu-id="435b5-314">name</span><span class="sxs-lookup"><span data-stu-id="435b5-314">name</span></span> |<span data-ttu-id="435b5-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="435b5-315">Edm.String</span></span> |
| <span data-ttu-id="435b5-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="435b5-316">lastlogindate</span></span> |<span data-ttu-id="435b5-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="435b5-317">Edm.DateTime</span></span> |

<span data-ttu-id="435b5-318">다음으로, Azure 테이블 데이터 집합을 다음과 같이 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="435b5-319">형식 정보가 기본 데이터 저장소에 이미 지정되어 있으므로 형식 정보로 "structure" 섹션을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="435b5-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="435b5-320">이 경우 .Blob에서 Azure 테이블에 데이터를 이동하면 Data Factory는fr-fr 문화권을 사용하여 사용자 지정 datetime 서식으로 Datetime 필드를 포함하는 형식 변환을 자동으로 수행합니다</span><span class="sxs-lookup"><span data-stu-id="435b5-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="435b5-321">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="435b5-322">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="435b5-322">Performance and Tuning</span></span>
<span data-ttu-id="435b5-323">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435b5-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
