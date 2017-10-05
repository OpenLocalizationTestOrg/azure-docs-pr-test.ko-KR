---
title: "Azure Cosmos DB 간 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Azure Cosmos DB 컬렉션 간 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="191fb-103">Azure Data Factory를 사용하여 Azure Cosmos DB 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="191fb-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="191fb-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure Cosmos DB(DocumentDB API) 간에 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="191fb-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="191fb-106">모든 지원되는 원본 데이터 저장소에서 Azure Cosmos DB로 또는 Azure Cosmos DB에서 모든 지원되는 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="191fb-107">복사 작업의 원본 또는 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="191fb-108">Azure Cosmos DB 커넥터만 DocumentDB API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="191fb-109">JSON 파일 또는 다른 Cosmos DB 컬렉션으로/에서 있는 그대로 데이터를 복사하려면 [JSON 문서 Import/Export](#importexport-json-documents)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="191fb-110">시작</span><span class="sxs-lookup"><span data-stu-id="191fb-110">Getting started</span></span>
<span data-ttu-id="191fb-111">다른 도구/API를 사용하여 Azure Cosmos DB 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="191fb-112">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="191fb-113">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="191fb-114">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="191fb-115">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="191fb-116">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="191fb-117">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="191fb-118">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="191fb-119">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="191fb-120">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="191fb-121">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="191fb-122">다른 곳에서 Cosmos DB로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예제](#json-examples) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="191fb-123">다음 섹션에서는 Cosmos DB에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="191fb-124">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="191fb-124">Linked service properties</span></span>
<span data-ttu-id="191fb-125">다음 테이블은 Azure Cosmos DB 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="191fb-126">**속성**</span><span class="sxs-lookup"><span data-stu-id="191fb-126">**Property**</span></span> | <span data-ttu-id="191fb-127">**설명**</span><span class="sxs-lookup"><span data-stu-id="191fb-127">**Description**</span></span> | <span data-ttu-id="191fb-128">**필수**</span><span class="sxs-lookup"><span data-stu-id="191fb-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="191fb-129">type</span><span class="sxs-lookup"><span data-stu-id="191fb-129">type</span></span> |<span data-ttu-id="191fb-130">형식 속성은 **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="191fb-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="191fb-131">예</span><span class="sxs-lookup"><span data-stu-id="191fb-131">Yes</span></span> |
| <span data-ttu-id="191fb-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="191fb-132">connectionString</span></span> |<span data-ttu-id="191fb-133">Azure Cosmos DB 데이터베이스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="191fb-134">예</span><span class="sxs-lookup"><span data-stu-id="191fb-134">Yes</span></span> |

<span data-ttu-id="191fb-135">예제:</span><span class="sxs-lookup"><span data-stu-id="191fb-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="191fb-136">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="191fb-136">Dataset properties</span></span>
<span data-ttu-id="191fb-137">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="191fb-138">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="191fb-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="191fb-139">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="191fb-140">**DocumentDbCollection** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="191fb-141">**속성**</span><span class="sxs-lookup"><span data-stu-id="191fb-141">**Property**</span></span> | <span data-ttu-id="191fb-142">**설명**</span><span class="sxs-lookup"><span data-stu-id="191fb-142">**Description**</span></span> | <span data-ttu-id="191fb-143">**필수**</span><span class="sxs-lookup"><span data-stu-id="191fb-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="191fb-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="191fb-144">collectionName</span></span> |<span data-ttu-id="191fb-145">Cosmos DB 문서 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="191fb-146">예</span><span class="sxs-lookup"><span data-stu-id="191fb-146">Yes</span></span> |

<span data-ttu-id="191fb-147">예제:</span><span class="sxs-lookup"><span data-stu-id="191fb-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="191fb-148">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="191fb-148">Schema by Data Factory</span></span>
<span data-ttu-id="191fb-149">Azure Cosmos DB와 같은 스키마 없는 데이터 저장소의 경우 Data Factory 서비스는 다음 방법 중 하나로 스키마를 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="191fb-150">데이터 집합 정의에서 **구조** 속성을 사용하여 데이터의 구조를 지정하는 경우 Data Factory 서비스는 이 구조를 스키마로 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="191fb-151">이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="191fb-152">데이터 집합 정의에서 **구조** 속성을 사용하여 데이터의 구조를 지정하지 않는 경우 Data Factory 서비스는 데이터의 첫 번째 행을 사용하여 스키마를 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="191fb-153">이 경우 첫 번째 행에 전체 스키마가 포함되어 있지 않으면 일부 열이 복사 작업의 결과에서 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="191fb-154">따라서 스키마 없는 데이터 원본에 대한 모범 사례는 **구조** 속성을 사용하여 데이터의 구조를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="191fb-155">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="191fb-155">Copy activity properties</span></span>
<span data-ttu-id="191fb-156">작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="191fb-157">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="191fb-158">복사 작업은 하나의 입력을 가지고 하나의 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="191fb-159">반면 작업의 typeProperties 섹션에서 사용할 수 있는 속성은 각 작업 형식에 따라 다르며 복사 작업의 경우 속성은 원본 및 싱크의 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="191fb-160">원본이 **DocumentDbCollectionSource** 형식인 복사 작업의 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="191fb-161">**속성**</span><span class="sxs-lookup"><span data-stu-id="191fb-161">**Property**</span></span> | <span data-ttu-id="191fb-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="191fb-162">**Description**</span></span> | <span data-ttu-id="191fb-163">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="191fb-163">**Allowed values**</span></span> | <span data-ttu-id="191fb-164">**필수**</span><span class="sxs-lookup"><span data-stu-id="191fb-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="191fb-165">쿼리</span><span class="sxs-lookup"><span data-stu-id="191fb-165">query</span></span> |<span data-ttu-id="191fb-166">데이터를 읽는 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-166">Specify the query to read data.</span></span> |<span data-ttu-id="191fb-167">Azure Cosmos DB에서 지원하는 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="191fb-168">예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="191fb-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="191fb-169">아니요</span><span class="sxs-lookup"><span data-stu-id="191fb-169">No</span></span> <br/><br/><span data-ttu-id="191fb-170">지정하지 않는 경우 실행되는 SQL 문: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="191fb-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="191fb-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="191fb-171">nestingSeparator</span></span> |<span data-ttu-id="191fb-172">문서가 중첩됨을 나타내는 특수 문자</span><span class="sxs-lookup"><span data-stu-id="191fb-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="191fb-173">모든 character입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-173">Any character.</span></span> <br/><br/><span data-ttu-id="191fb-174">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="191fb-175">Azure 데이터 팩터리를 사용하면 nestingSeparator, 즉 위 예에서 "."를 통해 계층 구조를</span><span class="sxs-lookup"><span data-stu-id="191fb-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="191fb-176">표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-176">in the above examples.</span></span> <span data-ttu-id="191fb-177">테이블 정의에서 "Name.First", "Name.Middle" 및 "Name.Last"에 따르면 구분 기호를 사용하여 복사 작업이 3개의 자식 요소(처음, 중간 및 마지막)가 있는 "Name" 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="191fb-178">아니요</span><span class="sxs-lookup"><span data-stu-id="191fb-178">No</span></span> |

<span data-ttu-id="191fb-179">**DocumentDbCollectionSink**는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="191fb-180">**속성**</span><span class="sxs-lookup"><span data-stu-id="191fb-180">**Property**</span></span> | <span data-ttu-id="191fb-181">**설명**</span><span class="sxs-lookup"><span data-stu-id="191fb-181">**Description**</span></span> | <span data-ttu-id="191fb-182">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="191fb-182">**Allowed values**</span></span> | <span data-ttu-id="191fb-183">**필수**</span><span class="sxs-lookup"><span data-stu-id="191fb-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="191fb-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="191fb-184">nestingSeparator</span></span> |<span data-ttu-id="191fb-185">중첩된 해당 문서를 나타내는 원본 열 이름에 특수 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="191fb-186">위의 예에서 출력 테이블의 `Name.First`는 Cosmos DB 문서에서 다음 JSON 구조를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="191fb-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="191fb-187">"Name": {</span></span><br/>    <span data-ttu-id="191fb-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="191fb-188">"First": "John"</span></span><br/><span data-ttu-id="191fb-189">},</span><span class="sxs-lookup"><span data-stu-id="191fb-189">},</span></span> |<span data-ttu-id="191fb-190">중첩 수준을 구분하는데 사용되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="191fb-191">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="191fb-192">중첩 수준을 구분하는데 사용되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="191fb-193">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="191fb-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="191fb-194">writeBatchSize</span></span> |<span data-ttu-id="191fb-195">문서를 작성하는 Azure Cosmos DB 서비스에 대한 병렬 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="191fb-196">이 속성을 사용하여 Cosmos DB 간 데이터를 복사하는 경우 성능을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="191fb-197">Cosmos DB에 더 많은 병렬 요청이 전송되기 때문에 writeBatchSize 증가하는 경우 더 나은 성능을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="191fb-198">하지만 오류 메시지: “요청 빈도가 높습니다."를 발생 시킬 수 있는 제한을 방지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="191fb-199">제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 작업의 경우 더 나은 컬렉션(예: S3)을 사용하여 사용할 수 있는 처리량(2,500개의 요청 단위/초)을 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="191fb-200">Integer</span><span class="sxs-lookup"><span data-stu-id="191fb-200">Integer</span></span> |<span data-ttu-id="191fb-201">아니요(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="191fb-201">No (default: 5)</span></span> |
| <span data-ttu-id="191fb-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="191fb-202">writeBatchTimeout</span></span> |<span data-ttu-id="191fb-203">시간이 초과 되기 전에 완료하려는 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="191fb-204">timespan</span><span class="sxs-lookup"><span data-stu-id="191fb-204">timespan</span></span><br/><br/> <span data-ttu-id="191fb-205">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="191fb-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="191fb-206">아니요</span><span class="sxs-lookup"><span data-stu-id="191fb-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="191fb-207">JSON 문서 가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="191fb-207">Import/Export JSON documents</span></span>
<span data-ttu-id="191fb-208">이 Cosmos DB 커넥터를 사용하여 다음을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="191fb-209">Azure Blob, Azure Data Lake, 온-프레미스 파일 시스템 또는 기타 Azure Data Factory에서 지원하는 파일 기반 저장소 등 다양한 원본에서 Cosmos DB로 JSON 문서를 가져오기</span><span class="sxs-lookup"><span data-stu-id="191fb-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="191fb-210">Cosmos DB 컬렉션에서 다양한 파일 기반 저장소로 JSON 문서 내보내기</span><span class="sxs-lookup"><span data-stu-id="191fb-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="191fb-211">두 Cosmos DB 컬렉션 간에 데이터를 있는 그대로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="191fb-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="191fb-212">이러한 스키마 독립적 복사를 수행하려면</span><span class="sxs-lookup"><span data-stu-id="191fb-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="191fb-213">복사 마법사를 사용할 경우 **"JSON 파일 또는 Cosmos DB 컬렉션으로 있는 그대로 내보내기"** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="191fb-214">JSON 편집을 사용할 때 복사 작업에서 Cosmos DB 데이터 집합에서 "structure" 섹션을 지정하지 않고 Cosmos DB 원본/싱크에 대한 "nestingSeparator" 속성도 지정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="191fb-215">JSON 파일에서 가져오거나 이 파일로 내보내려면 파일 저장소 데이터 집합에서 형식을 "JsonFormat"으로, 구성을 "filePattern"으로 지정한 후 나머지 형식 설정을 건너뜁니다. 자세한 내용은 [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="191fb-216">JSON 예</span><span class="sxs-lookup"><span data-stu-id="191fb-216">JSON examples</span></span>
<span data-ttu-id="191fb-217">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="191fb-218">Azure Cosmos DB 및 Azure Blob Storage 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="191fb-219">그러나 Azure Data Factory의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="191fb-220">예제: Azure Cosmos DB에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="191fb-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="191fb-221">아래 샘플은 다음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-221">The sample below shows:</span></span>

1. <span data-ttu-id="191fb-222">[DocumentDb](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="191fb-223">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="191fb-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="191fb-224">[DocumentDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="191fb-225">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="191fb-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="191fb-226">[DocumentDbCollectionSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="191fb-227">이 샘플에서는 Azure Cosmos DB에서 Azure Blob으로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="191fb-228">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="191fb-229">**Azure Cosmos DB 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="191fb-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="191fb-230">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="191fb-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="191fb-231">**Azure 문서 DB 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="191fb-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="191fb-232">예제는 Azure Cosmos DB 데이터베이스에 **사람**이라는 컬렉션이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="191fb-233">"외부":"true" 설정 및 externalData 정책 지정은 Azure 데이터 팩터리 서비스가 테이블이 데이터 팩터리의 외부에 있으며 데이터 공장의 활동에 의해 생성되지 않는다는 점을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="191fb-234">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="191fb-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="191fb-235">데이터는 시간 세분성으로 특정 날짜와 시간을 반영하는 blob에 대한 경로가 있는 새 blob로 매시간 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="191fb-236">Cosmos DB 데이터베이스의 사용자 컬렉션에서 샘플 JSON 문서:</span><span class="sxs-lookup"><span data-stu-id="191fb-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="191fb-237">Cosmos DB는 계층적 JSON 문서에 대한 구문과 같이 SQL을 사용하여 쿼리 문서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="191fb-238">예제:</span><span class="sxs-lookup"><span data-stu-id="191fb-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="191fb-239">다음 파이프라인은 Azure Cosmos DB 데이터베이스의 Person 컬렉션에서 Azure blob에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="191fb-240">복사 작업의 부분인 입력 및 출력 데이터 집합이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="191fb-241">예제: Azure Blob에서 Azure Cosmos DB로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="191fb-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="191fb-242">아래 샘플은 다음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-242">The sample below shows:</span></span>

1. <span data-ttu-id="191fb-243">[DocumentDb](#azure-documentdb-linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="191fb-244">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="191fb-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="191fb-245">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="191fb-246">[DocumentDbCollection](#azure-documentdb-dataset-type-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="191fb-247">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="191fb-248">이 샘플은 Azure Blob에서 Azure Cosmos DB로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="191fb-249">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="191fb-250">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="191fb-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="191fb-251">**Azure Cosmos DB 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="191fb-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="191fb-252">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="191fb-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="191fb-253">**Azure Cosmos DB 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="191fb-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="191fb-254">샘플은 "Person"이라는 컬렉션에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="191fb-255">다음 파이프라인은 Azure Blob에서 Cosmos DB의 사용자 컬렉션에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="191fb-256">복사 작업의 부분인 입력 및 출력 데이터 집합이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="191fb-257">샘플 blob 입력이 인 경우</span><span class="sxs-lookup"><span data-stu-id="191fb-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="191fb-258">Cosmos DB에서 출력 JSON은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="191fb-259">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="191fb-260">Azure 데이터 팩터리를 사용하면 **nestingSeparator** 즉, 이 예에서 "."를 통해 계층 구조를</span><span class="sxs-lookup"><span data-stu-id="191fb-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="191fb-261">표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-261">in this example.</span></span> <span data-ttu-id="191fb-262">테이블 정의에서 "Name.First", "Name.Middle" 및 "Name.Last"에 따르면 구분 기호를 사용하여 복사 작업이 3개의 자식 요소(처음, 중간 및 마지막)가 있는 "Name" 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="191fb-263">부록</span><span class="sxs-lookup"><span data-stu-id="191fb-263">Appendix</span></span>
1. <span data-ttu-id="191fb-264">**질문:** 복사 작업은 기존 레코드의 업데이트를 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="191fb-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="191fb-265">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="191fb-265">**Answer:** No.</span></span>
2. <span data-ttu-id="191fb-266">**질문:** 레코드 복사 이미 처리 하도록 Azure Cosmos DB에 복사본을 다시 시도 하면 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="191fb-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="191fb-267">**대답:** 레코드에 "ID" 필드가 있고 복사 작업이 동일한 ID를 가진 레코드를 삽입하려고 시도하는 경우 복사 작업에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="191fb-268">**질문:** 는 Data Factory 지원 [범위 또는 해시를 기반으로 데이터 분할](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="191fb-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="191fb-269">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="191fb-269">**Answer:** No.</span></span>
4. <span data-ttu-id="191fb-270">**질문:** 테이블에 대 한 하나 이상의 Azure Cosmos DB 컬렉션 지정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="191fb-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="191fb-271">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="191fb-271">**Answer:** No.</span></span> <span data-ttu-id="191fb-272">이 경우 하나의 컬렉션만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191fb-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="191fb-273">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="191fb-273">Performance and Tuning</span></span>
<span data-ttu-id="191fb-274">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191fb-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
