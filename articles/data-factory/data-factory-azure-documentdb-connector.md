---
title: "aaaMove 데이터/Azure Cosmos DB에서 | Microsoft Docs"
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="9582a-103">Azure 데이터 팩터리를 사용 하 여 Azure Cosmos DB에서 tooand 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="9582a-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="9582a-104">이 문서에서는 toouse Azure Cosmos DB (DocumentDB API)에서 Azure Data Factory toomove 데이터 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="9582a-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="9582a-106">데이터 tooAzure Cosmos DB 저장 하거나 Azure Cosmos DB 지원 tooany 싱크 데이터에서 저장할 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="9582a-107">목록이 hello 복사 작업에서 원본 또는 싱크도 지 원하는 데이터 저장소에 대 한 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9582a-108">Azure Cosmos DB 커넥터만 DocumentDB API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="9582a-109">toocopy 데이터도-는 를/다른 Cosmos DB 컬렉션 또는 JSON 파일에서 참조 [가져오기/내보내기 JSON 문서](#importexport-json-documents)합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="9582a-110">시작</span><span class="sxs-lookup"><span data-stu-id="9582a-110">Getting started</span></span>
<span data-ttu-id="9582a-111">다른 도구/API를 사용하여 Azure Cosmos DB 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="9582a-112">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="9582a-113">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="9582a-114">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9582a-115">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9582a-116">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="9582a-117">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="9582a-118">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="9582a-119">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9582a-120">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="9582a-121">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="9582a-122">샘플 은/Cosmos DB에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="9582a-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="9582a-123">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooCosmos DB에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="9582a-124">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="9582a-124">Linked service properties</span></span>
<span data-ttu-id="9582a-125">다음 표에서 hello JSON 요소 특정 tooAzure Cosmos DB 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="9582a-126">**속성**</span><span class="sxs-lookup"><span data-stu-id="9582a-126">**Property**</span></span> | <span data-ttu-id="9582a-127">**설명**</span><span class="sxs-lookup"><span data-stu-id="9582a-127">**Description**</span></span> | <span data-ttu-id="9582a-128">**필수**</span><span class="sxs-lookup"><span data-stu-id="9582a-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9582a-129">type</span><span class="sxs-lookup"><span data-stu-id="9582a-129">type</span></span> |<span data-ttu-id="9582a-130">hello type 속성 설정 해야 합니다: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="9582a-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="9582a-131">예</span><span class="sxs-lookup"><span data-stu-id="9582a-131">Yes</span></span> |
| <span data-ttu-id="9582a-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="9582a-132">connectionString</span></span> |<span data-ttu-id="9582a-133">Tooconnect tooAzure Cosmos DB 데이터베이스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="9582a-134">예</span><span class="sxs-lookup"><span data-stu-id="9582a-134">Yes</span></span> |

<span data-ttu-id="9582a-135">예제:</span><span class="sxs-lookup"><span data-stu-id="9582a-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="9582a-136">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="9582a-136">Dataset properties</span></span>
<span data-ttu-id="9582a-137">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록은 toohello를 참조 하십시오 [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="9582a-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9582a-138">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="9582a-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9582a-139">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="9582a-140">hello typeProperties 형식의 hello 데이터 집합에 대 한 섹션 **DocumentDbCollection** hello 다음과 같은 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="9582a-141">**속성**</span><span class="sxs-lookup"><span data-stu-id="9582a-141">**Property**</span></span> | <span data-ttu-id="9582a-142">**설명**</span><span class="sxs-lookup"><span data-stu-id="9582a-142">**Description**</span></span> | <span data-ttu-id="9582a-143">**필수**</span><span class="sxs-lookup"><span data-stu-id="9582a-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9582a-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="9582a-144">collectionName</span></span> |<span data-ttu-id="9582a-145">Hello Cosmos DB 문서 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="9582a-146">예</span><span class="sxs-lookup"><span data-stu-id="9582a-146">Yes</span></span> |

<span data-ttu-id="9582a-147">예제:</span><span class="sxs-lookup"><span data-stu-id="9582a-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="9582a-148">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="9582a-148">Schema by Data Factory</span></span>
<span data-ttu-id="9582a-149">Azure Cosmos DB와 같은 스키마가 없는 데이터 저장소에 대 한 hello 데이터 팩터리 서비스 hello 같은 방법으로 다음 중 하나에 hello 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="9582a-150">Hello를 사용 하 여 데이터의 hello 구조를 지정 하는 경우 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 스키마와이 구조를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="9582a-151">이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="9582a-152">Hello를 사용 하 여 데이터의 hello 구조를 지정 하지 않으면 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 데이터의 첫 번째 행 hello를 사용 하 여 hello 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="9582a-153">이 경우 hello 첫 번째 행에 hello 전체 스키마가 포함 되어 있지 않으면, 일부 열은 복사 작업의 hello 결과에서 누락 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="9582a-154">따라서 스키마 없는 데이터 원본에 대 한 hello 것이 가장 좋습니다 hello를 사용 하 여 데이터의 toospecify hello 구조 **구조** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9582a-155">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="9582a-155">Copy activity properties</span></span>
<span data-ttu-id="9582a-156">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록은 toohello를 참조 하십시오 [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="9582a-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9582a-157">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="9582a-158">복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="9582a-159">속성 hello에 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 반면 다 각 활동 유형 및 복사 작업의 원본 및 싱크 hello 형식에 따라 발생 한 경우.</span><span class="sxs-lookup"><span data-stu-id="9582a-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="9582a-160">원본 유형인 경우 복사 작업의 경우 **DocumentDbCollectionSource** hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="9582a-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="9582a-161">**속성**</span><span class="sxs-lookup"><span data-stu-id="9582a-161">**Property**</span></span> | <span data-ttu-id="9582a-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="9582a-162">**Description**</span></span> | <span data-ttu-id="9582a-163">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="9582a-163">**Allowed values**</span></span> | <span data-ttu-id="9582a-164">**필수**</span><span class="sxs-lookup"><span data-stu-id="9582a-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9582a-165">쿼리</span><span class="sxs-lookup"><span data-stu-id="9582a-165">query</span></span> |<span data-ttu-id="9582a-166">Hello tooread 데이터 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="9582a-167">Azure Cosmos DB에서 지원하는 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="9582a-168">예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="9582a-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="9582a-169">아니요</span><span class="sxs-lookup"><span data-stu-id="9582a-169">No</span></span> <br/><br/><span data-ttu-id="9582a-170">지정 하지 않으면 실행 되는 SQL 문을 hello:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="9582a-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="9582a-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="9582a-171">nestingSeparator</span></span> |<span data-ttu-id="9582a-172">문서 hello 특수 문자 tooindicate 중첩</span><span class="sxs-lookup"><span data-stu-id="9582a-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="9582a-173">모든 character입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-173">Any character.</span></span> <br/><br/><span data-ttu-id="9582a-174">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="9582a-175">Azure 데이터 팩터리는 nestingSeparator 통해 사용자 toodenote 계층 구조를 사용 하면 "."</span><span class="sxs-lookup"><span data-stu-id="9582a-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="9582a-176">위의 예제 안녕하세요에.</span><span class="sxs-lookup"><span data-stu-id="9582a-176">in hello above examples.</span></span> <span data-ttu-id="9582a-177">Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="9582a-178">아니요</span><span class="sxs-lookup"><span data-stu-id="9582a-178">No</span></span> |

<span data-ttu-id="9582a-179">**DocumentDbCollectionSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="9582a-180">**속성**</span><span class="sxs-lookup"><span data-stu-id="9582a-180">**Property**</span></span> | <span data-ttu-id="9582a-181">**설명**</span><span class="sxs-lookup"><span data-stu-id="9582a-181">**Description**</span></span> | <span data-ttu-id="9582a-182">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="9582a-182">**Allowed values**</span></span> | <span data-ttu-id="9582a-183">**필수**</span><span class="sxs-lookup"><span data-stu-id="9582a-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9582a-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="9582a-184">nestingSeparator</span></span> |<span data-ttu-id="9582a-185">Hello 원본 열 이름 tooindicate 중첩 문서에에서 특수 문자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="9582a-186">예를 들어 위의: `Name.First` hello 출력 테이블 생성 하는 hello Cosmos DB 문서의 JSON 구조를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="9582a-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="9582a-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="9582a-187">"Name": {</span></span><br/>    <span data-ttu-id="9582a-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="9582a-188">"First": "John"</span></span><br/><span data-ttu-id="9582a-189">},</span><span class="sxs-lookup"><span data-stu-id="9582a-189">},</span></span> |<span data-ttu-id="9582a-190">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="9582a-191">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="9582a-192">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="9582a-193">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="9582a-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="9582a-194">writeBatchSize</span></span> |<span data-ttu-id="9582a-195">TooAzure Cosmos DB 서비스 toocreate 문서를 요청 하는 병렬의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="9582a-196">이 속성을 사용 하 여 Cosmos DB에서 데이터를 복사할 때 hello 성능을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="9582a-197">더 많은 병렬 요청 tooCosmos DB 보내지므로 writeBatchSize를 늘리면 성능이 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="9582a-198">그러나 조정을 tooavoid 해야 hello 오류 메시지가 발생할 수 있습니다: "요청 빈도가 높습니다."입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="9582a-199">제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 작업을 사용할 수 있습니다 더 나은 컬렉션 (예: S3) toohave hello 사용 가능한 대부분 처리량 (2,500 단위 수/초를 요청 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="9582a-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="9582a-200">Integer</span><span class="sxs-lookup"><span data-stu-id="9582a-200">Integer</span></span> |<span data-ttu-id="9582a-201">아니요(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="9582a-201">No (default: 5)</span></span> |
| <span data-ttu-id="9582a-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="9582a-202">writeBatchTimeout</span></span> |<span data-ttu-id="9582a-203">대기 시간이 초과 되기 전에 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="9582a-204">timespan</span><span class="sxs-lookup"><span data-stu-id="9582a-204">timespan</span></span><br/><br/> <span data-ttu-id="9582a-205">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="9582a-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="9582a-206">아니요</span><span class="sxs-lookup"><span data-stu-id="9582a-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="9582a-207">JSON 문서 가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="9582a-207">Import/Export JSON documents</span></span>
<span data-ttu-id="9582a-208">이 Cosmos DB 커넥터를 사용하여 다음을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="9582a-209">Azure Blob, Azure Data Lake, 온-프레미스 파일 시스템 또는 기타 Azure Data Factory에서 지원하는 파일 기반 저장소 등 다양한 원본에서 Cosmos DB로 JSON 문서를 가져오기</span><span class="sxs-lookup"><span data-stu-id="9582a-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="9582a-210">Cosmos DB 컬렉션에서 다양한 파일 기반 저장소로 JSON 문서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9582a-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="9582a-211">두 Cosmos DB 컬렉션 간에 데이터를 있는 그대로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9582a-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="9582a-212">tooachieve 이러한 스키마를 알 수 없는 복사</span><span class="sxs-lookup"><span data-stu-id="9582a-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="9582a-213">복사 마법사를 사용 하는 경우 확인 hello **"으로 내보내기-tooJSON 파일 또는 Cosmos DB 컬렉션"** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="9582a-214">때 JSON 편집을 사용 하 여 지정 하지 않으면 hello "구조" 섹션 Cosmos DB 데이터 집합에도 복사 작업에서 소스/싱크 Cosmos DB "nestingSeparator" 속성.</span><span class="sxs-lookup"><span data-stu-id="9582a-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="9582a-215">tooimport / 내보내기 tooJSON 파일, hello 파일 저장소 데이터 집합의 형식 유형을 "filePattern" config "JsonFormat"로 지정 하 고 hello rest 형식 설정 건너뛰기, 참조 [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format) 세부 정보 섹션.</span><span class="sxs-lookup"><span data-stu-id="9582a-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="9582a-216">JSON 예</span><span class="sxs-lookup"><span data-stu-id="9582a-216">JSON examples</span></span>
<span data-ttu-id="9582a-217">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9582a-218">표시 방법을 toocopy 데이터 tooand Azure Cosmos DB 및 Azure Blob 저장소에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="9582a-219">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 hello 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="9582a-220">예: Azure Cosmos DB tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="9582a-221">아래 hello 샘플을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-221">hello sample below shows:</span></span>

1. <span data-ttu-id="9582a-222">[DocumentDb](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="9582a-223">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="9582a-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9582a-224">[DocumentDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="9582a-225">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="9582a-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9582a-226">[DocumentDbCollectionSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9582a-227">hello 샘플 Azure Cosmos DB tooAzure Blob 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="9582a-228">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="9582a-229">**Azure Cosmos DB 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9582a-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="9582a-230">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9582a-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="9582a-231">**Azure 문서 DB 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9582a-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="9582a-232">라는 컬렉션 있다고 가정 하 고 hello 샘플 **사람** Azure Cosmos DB 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="9582a-233">설정 "외부": "true" 및 externalData 지정 hello Azure 데이터 팩터리 서비스는 hello 테이블 정책 정보는 외부 toohello 데이터 팩터리 및 hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="9582a-234">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9582a-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9582a-235">데이터는 새 blob 복사 tooa 시간 단위가 hello 특정 날짜/시간을 반영 하는 hello blob에 대 한 hello 경로로 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="9582a-236">Hello Cosmos DB 데이터베이스의 사용자 컬렉션에에서 대 한 샘플 JSON 문서:</span><span class="sxs-lookup"><span data-stu-id="9582a-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="9582a-237">Cosmos DB는 계층적 JSON 문서에 대한 구문과 같이 SQL을 사용하여 쿼리 문서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="9582a-238">예제:</span><span class="sxs-lookup"><span data-stu-id="9582a-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="9582a-239">hello 다음 파이프라인 hello hello Azure Cosmos DB 데이터베이스 tooan Azure blob의에서 사용자 컬렉션에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="9582a-240">Hello 복사 활동 hello의 일환으로 입력 및 출력 데이터 집합 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="9582a-241">예: Azure Blob tooAzure Cosmos DB에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="9582a-242">아래 hello 샘플을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-242">hello sample below shows:</span></span>

1. <span data-ttu-id="9582a-243">[DocumentDb](#azure-documentdb-linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="9582a-244">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="9582a-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9582a-245">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="9582a-246">[DocumentDbCollection](#azure-documentdb-dataset-type-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="9582a-247">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="9582a-248">hello 예제는 Azure blob tooAzure Cosmos DB에서에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="9582a-249">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="9582a-250">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9582a-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="9582a-251">**Azure Cosmos DB 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9582a-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="9582a-252">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9582a-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="9582a-253">**Azure Cosmos DB 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9582a-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="9582a-254">hello 샘플 "Person" 이라는 데이터 tooa 컬렉션을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="9582a-255">hello 다음 Azure Blob toohello hello Cosmos DB에서에서 사용자 컬렉션의에서 데이터 복사 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="9582a-256">Hello 복사 활동 hello의 일환으로 입력 및 출력 데이터 집합 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="9582a-257">Hello 샘플 blob 입력 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9582a-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="9582a-258">다음으로 hello Cosmos DB의 JSON 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="9582a-259">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="9582a-260">Azure 데이터 팩터리를 통해 사용자 toodenote 계층 구조를 사용 하면 **nestingSeparator**, 즉 "."</span><span class="sxs-lookup"><span data-stu-id="9582a-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="9582a-261">표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-261">in this example.</span></span> <span data-ttu-id="9582a-262">Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="9582a-263">부록</span><span class="sxs-lookup"><span data-stu-id="9582a-263">Appendix</span></span>
1. <span data-ttu-id="9582a-264">**질문:** 기존 레코드의 복사 작업 지원 업데이트 hello가?</span><span class="sxs-lookup"><span data-stu-id="9582a-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="9582a-265">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="9582a-265">**Answer:** No.</span></span>
2. <span data-ttu-id="9582a-266">**질문:** 레코드 복사와 복사 tooAzure Cosmos DB 거래의 다시 시도 하면 이미 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="9582a-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="9582a-267">**답변:** 레코드는 "ID" 필드를 포함 하 고 hello 복사 작업 tooinsert hello로 레코드 동일한 ID를 hello 복사 작업에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="9582a-268">**질문:** Data Factory는 [범위 또는 해시 기반 데이터 분할](../documentdb/documentdb-partition-data.md)을 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="9582a-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="9582a-269">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="9582a-269">**Answer:** No.</span></span>
4. <span data-ttu-id="9582a-270">**질문:** 하나의 테이블에 대해 하나 이상의 Azure Cosmos DB 컬렉션을 지정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="9582a-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="9582a-271">**대답:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="9582a-271">**Answer:** No.</span></span> <span data-ttu-id="9582a-272">이 경우 하나의 컬렉션만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9582a-273">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="9582a-273">Performance and Tuning</span></span>
<span data-ttu-id="9582a-274">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9582a-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
