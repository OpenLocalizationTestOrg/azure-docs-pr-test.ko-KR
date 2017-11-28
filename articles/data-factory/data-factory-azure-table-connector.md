---
title: "Azure 테이블에서 데이터를 aaaMove | Microsoft Docs"
description: "자세한 내용은 방법 toomove 한 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure 테이블 저장소에서."
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
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="6d093-103">Azure 데이터 팩터리를 사용 하 여 Azure 테이블에서 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="6d093-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="6d093-104">이 문서에서는 toouse Azure 테이블 저장소에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="6d093-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="6d093-106">데이터 테이블 저장소 tooAzure 저장 하거나 Azure 테이블 저장소 지원 tooany 싱크 데이터에서 저장할 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="6d093-107">목록이 hello 복사 작업에서 원본 또는 싱크도 지 원하는 데이터 저장소에 대 한 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6d093-108">시작</span><span class="sxs-lookup"><span data-stu-id="6d093-108">Getting started</span></span>
<span data-ttu-id="6d093-109">다른 도구/API를 사용하여 Azure Table Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="6d093-110">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6d093-111">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6d093-112">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6d093-113">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6d093-114">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="6d093-115">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="6d093-116">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="6d093-117">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6d093-118">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6d093-119">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6d093-120">샘플 은/Azure 테이블 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="6d093-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="6d093-121">사용 되는 toodefine Data Factory 엔터티에 특정 tooAzure 테이블 저장소는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="6d093-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6d093-122">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="6d093-122">Linked service properties</span></span>
<span data-ttu-id="6d093-123">두 가지가 toolink Azure blob 저장소 tooan Azure 데이터 팩터리에 연결 된 서비스의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="6d093-124">**AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="6d093-125">Azure 저장소 연결 서비스 hello 전역 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="6d093-126">반면 hello Azure 저장소 SAS (공유 액세스 서명) 연결 된 서비스 시간 제한/범위 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="6d093-127">이 두 연결된 서비스에는 다른 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="6d093-128">필요에 맞는 hello 연결 된 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="6d093-129">hello 다음 섹션에서는 더욱 자세히 설명에 두 개의 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="6d093-130">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="6d093-130">Dataset properties</span></span>
<span data-ttu-id="6d093-131">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6d093-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6d093-132">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="6d093-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6d093-133">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6d093-134">hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureTable** hello 다음과 같은 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="6d093-135">속성</span><span class="sxs-lookup"><span data-stu-id="6d093-135">Property</span></span> | <span data-ttu-id="6d093-136">설명</span><span class="sxs-lookup"><span data-stu-id="6d093-136">Description</span></span> | <span data-ttu-id="6d093-137">필수</span><span class="sxs-lookup"><span data-stu-id="6d093-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d093-138">tableName</span><span class="sxs-lookup"><span data-stu-id="6d093-138">tableName</span></span> |<span data-ttu-id="6d093-139">연결 된 서비스는 hello Azure 테이블 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="6d093-140">예.</span><span class="sxs-lookup"><span data-stu-id="6d093-140">Yes.</span></span> <span data-ttu-id="6d093-141">를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="6d093-142">Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="6d093-143">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="6d093-143">Schema by Data Factory</span></span>
<span data-ttu-id="6d093-144">Azure 테이블과 같은 스키마가 없는 데이터 저장소에 대 한 hello 데이터 팩터리 서비스 hello 같은 방법으로 다음 중 하나에 hello 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="6d093-145">Hello를 사용 하 여 데이터의 hello 구조를 지정 하는 경우 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 스키마와이 구조를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="6d093-146">이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="6d093-147">Hello를 사용 하 여 hello 데이터 구조를 지정 하지 않으면 **구조** hello 데이터 집합 정의 데이터 팩터리의 속성 hello 데이터의 첫 번째 행 hello를 사용 하 여 hello 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="6d093-148">이 경우 첫 번째 행 hello hello 전체 스키마를 포함 하지 않으면 일부 열 복사 작업의 hello 결과에서 누락 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="6d093-149">따라서 스키마 없는 데이터 원본에 대 한 hello 것이 가장 좋습니다 hello를 사용 하 여 데이터의 toospecify hello 구조 **구조** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6d093-150">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="6d093-150">Copy activity properties</span></span>
<span data-ttu-id="6d093-151">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6d093-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6d093-152">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6d093-153">속성 hello에 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 각 활동 유형에 다른 손 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="6d093-154">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="6d093-155">**AzureTableSource** hello 다음과 같은 섹션 typeProperties의에서 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="6d093-156">속성</span><span class="sxs-lookup"><span data-stu-id="6d093-156">Property</span></span> | <span data-ttu-id="6d093-157">설명</span><span class="sxs-lookup"><span data-stu-id="6d093-157">Description</span></span> | <span data-ttu-id="6d093-158">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="6d093-158">Allowed values</span></span> | <span data-ttu-id="6d093-159">필수</span><span class="sxs-lookup"><span data-stu-id="6d093-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6d093-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="6d093-160">azureTableSourceQuery</span></span> |<span data-ttu-id="6d093-161">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6d093-162">Azure 테이블 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="6d093-162">Azure table query string.</span></span> <span data-ttu-id="6d093-163">Hello 다음 섹션의 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d093-163">See examples in hello next section.</span></span> |<span data-ttu-id="6d093-164">아니요.</span><span class="sxs-lookup"><span data-stu-id="6d093-164">No.</span></span> <span data-ttu-id="6d093-165">를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="6d093-166">Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="6d093-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="6d093-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="6d093-168">테이블의 hello 예외를 무시할지 존재 하지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="6d093-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="6d093-169">TRUE</span></span><br/><span data-ttu-id="6d093-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="6d093-170">FALSE</span></span> |<span data-ttu-id="6d093-171">아니요</span><span class="sxs-lookup"><span data-stu-id="6d093-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="6d093-172">azureTableSourceQuery 예제</span><span class="sxs-lookup"><span data-stu-id="6d093-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="6d093-173">Azure 테이블 열이 문자열 형식인 경우:</span><span class="sxs-lookup"><span data-stu-id="6d093-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="6d093-174">Azure 테이블 열이 날짜/시간 형식인 경우:</span><span class="sxs-lookup"><span data-stu-id="6d093-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="6d093-175">**AzureTableSink** hello 다음과 같은 섹션 typeProperties의에서 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="6d093-176">속성</span><span class="sxs-lookup"><span data-stu-id="6d093-176">Property</span></span> | <span data-ttu-id="6d093-177">설명</span><span class="sxs-lookup"><span data-stu-id="6d093-177">Description</span></span> | <span data-ttu-id="6d093-178">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="6d093-178">Allowed values</span></span> | <span data-ttu-id="6d093-179">필수</span><span class="sxs-lookup"><span data-stu-id="6d093-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6d093-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="6d093-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="6d093-181">기본 파티션 키 값 hello 싱크에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="6d093-182">문자열 값</span><span class="sxs-lookup"><span data-stu-id="6d093-182">A string value.</span></span> |<span data-ttu-id="6d093-183">아니요</span><span class="sxs-lookup"><span data-stu-id="6d093-183">No</span></span> |
| <span data-ttu-id="6d093-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="6d093-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="6d093-185">해당 값은 파티션 키로 사용 하는 hello 열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="6d093-186">지정 하지 않으면 AzureTableDefaultPartitionKeyValue hello 파티션 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="6d093-187">열 이름</span><span class="sxs-lookup"><span data-stu-id="6d093-187">A column name.</span></span> |<span data-ttu-id="6d093-188">아니요</span><span class="sxs-lookup"><span data-stu-id="6d093-188">No</span></span> |
| <span data-ttu-id="6d093-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="6d093-189">azureTableRowKeyName</span></span> |<span data-ttu-id="6d093-190">해당 열 값은 행 키로 사용 되는 hello 열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="6d093-191">지정하지 않으면 각 행에 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="6d093-192">열 이름</span><span class="sxs-lookup"><span data-stu-id="6d093-192">A column name.</span></span> |<span data-ttu-id="6d093-193">아니요</span><span class="sxs-lookup"><span data-stu-id="6d093-193">No</span></span> |
| <span data-ttu-id="6d093-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="6d093-194">azureTableInsertType</span></span> |<span data-ttu-id="6d093-195">Azure 테이블에 hello 모드 tooinsert 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="6d093-196">이 속성은 파티션 및 행 키 일치 하는 hello 출력 테이블의 기존 행에는 값을 바꾸거나 병합 있는지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="6d093-197">이러한 설정을 (병합 및 대체) 작동 방법에 대해 toolearn 참조 [삽입 또는 병합 엔터티](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [삽입 또는 교체 엔터티](https://msdn.microsoft.com/library/azure/hh452242.aspx) 항목.</span><span class="sxs-lookup"><span data-stu-id="6d093-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="6d093-198">두 옵션 모두 hello 입력에 존재 하지 않는 hello 출력 테이블에 행을 삭제 및 hello 테이블 수준이 아닌 hello 행 수준에서이 설정을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="6d093-199">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="6d093-199">merge (default)</span></span><br/><span data-ttu-id="6d093-200">바꾸기</span><span class="sxs-lookup"><span data-stu-id="6d093-200">replace</span></span> |<span data-ttu-id="6d093-201">아니요</span><span class="sxs-lookup"><span data-stu-id="6d093-201">No</span></span> |
| <span data-ttu-id="6d093-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6d093-202">writeBatchSize</span></span> |<span data-ttu-id="6d093-203">Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우에 hello Azure 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="6d093-204">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="6d093-204">Integer (number of rows)</span></span> |<span data-ttu-id="6d093-205">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="6d093-205">No (default: 10000)</span></span> |
| <span data-ttu-id="6d093-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6d093-206">writeBatchTimeout</span></span> |<span data-ttu-id="6d093-207">Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우 hello Azure 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="6d093-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="6d093-208">timespan</span><span class="sxs-lookup"><span data-stu-id="6d093-208">timespan</span></span><br/><br/><span data-ttu-id="6d093-209">예: "00:20:00"(20분)</span><span class="sxs-lookup"><span data-stu-id="6d093-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="6d093-210">더 (기본 toostorage 클라이언트 기본 제한 시간 값인 90 초)</span><span class="sxs-lookup"><span data-stu-id="6d093-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="6d093-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="6d093-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="6d093-212">AzureTablePartitionKeyName hello으로 hello 대상 열을 사용 하기 전에 hello 변환기 JSON 속성을 사용 하 여 원본 열 tooa 대상 열을 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d093-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="6d093-213">다음 예제는 hello, 원본 열 DivisionID 매핑된 toohello 대상 열입니다.: DivisionID 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="6d093-214">hello DivisionID hello 파티션 키로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="6d093-215">JSON 예</span><span class="sxs-lookup"><span data-stu-id="6d093-215">JSON examples</span></span>
<span data-ttu-id="6d093-216">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6d093-217">보여 줍니다 어떻게 toocopy 데이터 tooand Azure 테이블 저장소 및 Azure Blob 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="6d093-218">그러나 데이터를 복사할 수 있습니다 **직접** 지원 hello 싱크 hello 소스 tooany 중 어디에서 든 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="6d093-219">자세한 내용은의 "지원 되는 데이터 저장소와 형식" hello 섹션 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="6d093-220">예: Azure 테이블 tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="6d093-221">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="6d093-221">hello following sample shows:</span></span>

1. <span data-ttu-id="6d093-222">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)</span><span class="sxs-lookup"><span data-stu-id="6d093-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="6d093-223">[AzureTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="6d093-224">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="6d093-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6d093-225">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [AzureTableSource](#activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6d093-226">hello 예제 1 시간 마다 Azure 테이블 tooa blob에 toohello 기본 파티션에 속한 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="6d093-227">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6d093-228">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="6d093-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="6d093-229">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6d093-230">에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6d093-231">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d093-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6d093-232">**Azure 테이블 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6d093-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="6d093-233">hello 샘플 Azure 테이블에 포함 된 "MyTable" 테이블을 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="6d093-234">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="6d093-235">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6d093-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6d093-236">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="6d093-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6d093-237">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6d093-238">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="6d093-239">**AzureTableSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="6d093-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="6d093-240">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6d093-241">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**AzureTableSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6d093-242">지정 된 hello SQL 쿼리 **AzureTableSourceQuery** 속성 hello에서에서 데이터를 선택 hello 기본 파티션에 모든 시간 toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="6d093-243">예: Azure Blob tooAzure 테이블에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="6d093-244">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="6d093-244">hello following sample shows:</span></span>

1. <span data-ttu-id="6d093-245">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)</span><span class="sxs-lookup"><span data-stu-id="6d093-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="6d093-246">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="6d093-247">[AzureTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6d093-248">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureTableSink](#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6d093-249">hello 샘플에 1 시간 마다 Azure blob tooan Azure 테이블에서에서 시계열 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="6d093-250">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6d093-251">**Azure 저장소 연결된 서비스(Azure 테이블 및 Blob용):**</span><span class="sxs-lookup"><span data-stu-id="6d093-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="6d093-252">Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6d093-253">에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6d093-254">자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d093-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="6d093-255">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6d093-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="6d093-256">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6d093-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6d093-257">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6d093-258">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6d093-259">"external": "true" 설정을 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="6d093-260">**Azure 테이블 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6d093-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="6d093-261">hello 샘플 Azure 테이블에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="6d093-262">와 Azure 테이블 만들기 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6d093-263">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-263">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="6d093-264">**BlobSource 및 AzureTableSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="6d093-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="6d093-265">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6d093-266">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**AzureTableSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="6d093-267">Azure 테이블에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="6d093-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="6d093-268">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="6d093-269">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="6d093-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6d093-270">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="6d093-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6d093-271">를 너무 & Azure 테이블에서 데이터를 이동할 때 다음 hello [Azure 테이블 서비스에 의해 정의 된 매핑을](https://msdn.microsoft.com/library/azure/dd179338.aspx) 그 반대의 Azure 테이블 OData 형식 too.NET 형식에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="6d093-272">OData 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="6d093-272">OData Data Type</span></span> | <span data-ttu-id="6d093-273">.NET 형식</span><span class="sxs-lookup"><span data-stu-id="6d093-273">.NET Type</span></span> | <span data-ttu-id="6d093-274">세부 정보</span><span class="sxs-lookup"><span data-stu-id="6d093-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d093-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="6d093-275">Edm.Binary</span></span> |<span data-ttu-id="6d093-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="6d093-276">byte[]</span></span> |<span data-ttu-id="6d093-277">Too64 KB 바이트 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="6d093-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="6d093-278">Edm.Boolean</span></span> |<span data-ttu-id="6d093-279">bool</span><span class="sxs-lookup"><span data-stu-id="6d093-279">bool</span></span> |<span data-ttu-id="6d093-280">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-280">A Boolean value.</span></span> |
| <span data-ttu-id="6d093-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="6d093-281">Edm.DateTime</span></span> |<span data-ttu-id="6d093-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="6d093-282">DateTime</span></span> |<span data-ttu-id="6d093-283">UTC(협정 세계시)로 표현되는 64비트 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="6d093-284">hello는 범위가 서 기 1601 년 1 월 1 일 자정 12 시에서에서 시작 하는 날짜/시간 지원</span><span class="sxs-lookup"><span data-stu-id="6d093-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="6d093-285">(서기), UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-285">(C.E.), UTC.</span></span> <span data-ttu-id="6d093-286">hello 범위 9999 년 12 월 31 일에 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="6d093-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="6d093-287">Edm.Double</span></span> |<span data-ttu-id="6d093-288">double</span><span class="sxs-lookup"><span data-stu-id="6d093-288">double</span></span> |<span data-ttu-id="6d093-289">64비트 부동 소수점 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="6d093-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="6d093-290">Edm.Guid</span></span> |<span data-ttu-id="6d093-291">Guid</span><span class="sxs-lookup"><span data-stu-id="6d093-291">Guid</span></span> |<span data-ttu-id="6d093-292">전역적으로 고유한 128 비트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="6d093-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="6d093-293">Edm.Int32</span></span> |<span data-ttu-id="6d093-294">Int32</span><span class="sxs-lookup"><span data-stu-id="6d093-294">Int32</span></span> |<span data-ttu-id="6d093-295">32비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="6d093-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="6d093-296">Edm.Int64</span></span> |<span data-ttu-id="6d093-297">Int64</span><span class="sxs-lookup"><span data-stu-id="6d093-297">Int64</span></span> |<span data-ttu-id="6d093-298">64비트 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="6d093-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="6d093-299">Edm.String</span></span> |<span data-ttu-id="6d093-300">문자열</span><span class="sxs-lookup"><span data-stu-id="6d093-300">String</span></span> |<span data-ttu-id="6d093-301">UTF-16으로 인코딩된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="6d093-302">문자열 값 too64 KB up 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="6d093-303">형식 변환 샘플</span><span class="sxs-lookup"><span data-stu-id="6d093-303">Type Conversion Sample</span></span>
<span data-ttu-id="6d093-304">다음 예제는 hello 형식 변환이 있는 Azure Blob tooAzure 테이블에서에서 데이터를 복사 하기 위해 사용 되며</span><span class="sxs-lookup"><span data-stu-id="6d093-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="6d093-305">Hello Blob 데이터 집합 CSV 형태로 표시 하 고 3 개의 열이 포함 되어 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="6d093-306">그 중 하나가 hello 요일에 대 한 약어 프랑스어 이름을 사용 하 여 사용자 지정 날짜/시간 형식의 datetime 열입니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="6d093-307">Hello 열에 대 한 형식 정의 함께 다음과 같이 hello Blob 원본 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

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
<span data-ttu-id="6d093-308">Azure 테이블 OData 형식 too.NET 형식에서 hello 형식 매핑이 들어 hello 테이블 Azure 테이블의 스키마를 따르는 hello로 정의할는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="6d093-309">**Azure 테이블 스키마:**</span><span class="sxs-lookup"><span data-stu-id="6d093-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="6d093-310">열 이름</span><span class="sxs-lookup"><span data-stu-id="6d093-310">Column name</span></span> | <span data-ttu-id="6d093-311">형식</span><span class="sxs-lookup"><span data-stu-id="6d093-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="6d093-312">userid</span><span class="sxs-lookup"><span data-stu-id="6d093-312">userid</span></span> |<span data-ttu-id="6d093-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="6d093-313">Edm.Int64</span></span> |
| <span data-ttu-id="6d093-314">name</span><span class="sxs-lookup"><span data-stu-id="6d093-314">name</span></span> |<span data-ttu-id="6d093-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="6d093-315">Edm.String</span></span> |
| <span data-ttu-id="6d093-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="6d093-316">lastlogindate</span></span> |<span data-ttu-id="6d093-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="6d093-317">Edm.DateTime</span></span> |

<span data-ttu-id="6d093-318">다음으로 hello Azure 테이블의 데이터 집합을 다음과 같이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="6d093-319">Hello 형식 정보가 데이터 저장소를 기본 hello에 이미 지정 되어 있으므로 hello 유형 정보와 함께 toospecify "구조" 섹션을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

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

<span data-ttu-id="6d093-320">이 경우 데이터 팩터리의 자동으로 유형 수행 hello 날짜/시간 필드를 포함 하 여 Blob tooAzure 테이블에서에서 데이터를 이동 하는 경우 "fr-fr" hello culture를 사용 하 여 hello 사용자 지정 날짜/시간 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="6d093-321">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6d093-322">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="6d093-322">Performance and Tuning</span></span>
<span data-ttu-id="6d093-323">키에 대 한 toolearn Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 요소를 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d093-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
