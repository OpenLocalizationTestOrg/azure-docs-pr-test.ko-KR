---
title: "aaaCopy 데이터/Azure SQL 데이터 웨어하우스 로부터 | Microsoft Docs"
description: "자세한 내용은 방법 toocopy 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스"
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
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="7b42e-103">Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 복사</span><span class="sxs-lookup"><span data-stu-id="7b42e-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="7b42e-104">이 문서에서는 toouse Azure SQL 데이터 웨어하우스 로부터 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="7b42e-106">tooachieve 최고의 성능을, Azure SQL 데이터 웨어하우스로 PolyBase tooload 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-107">hello [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 섹션 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="7b42e-108">사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="7b42e-109">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="7b42e-109">Supported scenarios</span></span>
<span data-ttu-id="7b42e-110">데이터를 복사할 수 **Azure SQL 데이터 웨어하우스에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="7b42e-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="7b42e-111">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure SQL 데이터 웨어하우스**:</span><span class="sxs-lookup"><span data-stu-id="7b42e-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="7b42e-112">SQL Server 또는 Azure SQL 데이터베이스 tooAzure에서 데이터를 복사 하는 경우 SQL 데이터 웨어하우스, hello 대상 저장소, Data Factory에에서 hello 테이블이 존재 하지 않는 경우 자동으로 hello 테이블을에서 만들 수 SQL 데이터 웨어하우스 hello 원본의 hello 테이블의 스키마 hello를 사용 하 여 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="7b42e-113">자세한 내용은 [자동 테이블 만들기](#auto-table-creation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="7b42e-114">지원되는 인증 유형</span><span class="sxs-lookup"><span data-stu-id="7b42e-114">Supported authentication type</span></span>
<span data-ttu-id="7b42e-115">Azure SQL Data Warehouse 커넥터는 기본 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7b42e-116">시작</span><span class="sxs-lookup"><span data-stu-id="7b42e-116">Getting started</span></span>
<span data-ttu-id="7b42e-117">다른 도구/API를 사용하여 Azure SQL Data Warehouse 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="7b42e-118">hello 가장 쉬운 방법은 toocreate Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 파이프라인 toouse hello 복사 데이터 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="7b42e-119">참조 [자습서: 데이터를 Data Factory와 SQL 데이터 웨어하우스 로드](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="7b42e-120">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7b42e-121">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="7b42e-122">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="7b42e-123">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-123">Create a **data factory**.</span></span> <span data-ttu-id="7b42e-124">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="7b42e-125">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="7b42e-126">예를 들어 Azure blob 저장소 tooan Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터 웨어하우스 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="7b42e-127">특정 tooAzure SQL 데이터 웨어하우스에 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="7b42e-128">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="7b42e-129">Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="7b42e-130">고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터 웨어하우스에 다른 데이터 집합 toospecify hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="7b42e-131">특정 tooAzure SQL 데이터 웨어하우스는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="7b42e-132">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="7b42e-133">앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlDWSink 싱크도 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="7b42e-134">마찬가지로, Azure SQL 데이터 웨어하우스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlDWSource 및 사용 BlobSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="7b42e-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="7b42e-135">복사 활동 속성을 특정 tooAzure SQL 데이터 웨어하우스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="7b42e-136">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="7b42e-137">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="7b42e-138">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="7b42e-139">샘플 은/Azure SQL 데이터 웨어하우스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="7b42e-140">다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooAzure SQL 데이터 웨어하우스는 JSON 속성에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7b42e-141">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-141">Linked service properties</span></span>
<span data-ttu-id="7b42e-142">다음 표에서 hello JSON 요소 특정 tooAzure SQL 데이터 웨어하우스 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="7b42e-143">속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-143">Property</span></span> | <span data-ttu-id="7b42e-144">설명</span><span class="sxs-lookup"><span data-stu-id="7b42e-144">Description</span></span> | <span data-ttu-id="7b42e-145">필수</span><span class="sxs-lookup"><span data-stu-id="7b42e-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b42e-146">type</span><span class="sxs-lookup"><span data-stu-id="7b42e-146">type</span></span> |<span data-ttu-id="7b42e-147">hello type 속성 설정 해야 합니다: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="7b42e-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="7b42e-148">예</span><span class="sxs-lookup"><span data-stu-id="7b42e-148">Yes</span></span> |
| <span data-ttu-id="7b42e-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="7b42e-149">connectionString</span></span> |<span data-ttu-id="7b42e-150">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="7b42e-151">기본 인증만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="7b42e-152">예</span><span class="sxs-lookup"><span data-stu-id="7b42e-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7b42e-153">구성 [Azure SQL 데이터베이스 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 데이터베이스 서버를 너무 hello 및[Azure 서비스 tooaccess hello 서버](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="7b42e-154">또한 외부 Azure 비롯 하 여 데이터 팩터리 게이트웨이와 온-프레미스 데이터 원본에서 데이터 tooAzure SQL 데이터 웨어하우스를 복사 하는 경우 데이터 tooAzure SQL 데이터 웨어하우스를 전송 하는 hello 컴퓨터에 대 한 적절 한 IP 주소 범위를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="7b42e-155">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-155">Dataset properties</span></span>
<span data-ttu-id="7b42e-156">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="7b42e-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7b42e-157">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="7b42e-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7b42e-158">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="7b42e-159">hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureSqlDWTable** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="7b42e-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="7b42e-160">속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-160">Property</span></span> | <span data-ttu-id="7b42e-161">설명</span><span class="sxs-lookup"><span data-stu-id="7b42e-161">Description</span></span> | <span data-ttu-id="7b42e-162">필수</span><span class="sxs-lookup"><span data-stu-id="7b42e-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b42e-163">tableName</span><span class="sxs-lookup"><span data-stu-id="7b42e-163">tableName</span></span> |<span data-ttu-id="7b42e-164">Hello 테이블 또는 뷰의 연결 된 서비스 hello hello Azure SQL 데이터 웨어하우스 데이터베이스의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="7b42e-165">예</span><span class="sxs-lookup"><span data-stu-id="7b42e-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="7b42e-166">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-166">Copy activity properties</span></span>
<span data-ttu-id="7b42e-167">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="7b42e-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7b42e-168">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="7b42e-169">복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="7b42e-170">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="7b42e-171">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="7b42e-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="7b42e-172">SqlDWSource</span></span>
<span data-ttu-id="7b42e-173">원본 유형의 경우 **SqlDWSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="7b42e-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="7b42e-174">속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-174">Property</span></span> | <span data-ttu-id="7b42e-175">설명</span><span class="sxs-lookup"><span data-stu-id="7b42e-175">Description</span></span> | <span data-ttu-id="7b42e-176">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="7b42e-176">Allowed values</span></span> | <span data-ttu-id="7b42e-177">필수</span><span class="sxs-lookup"><span data-stu-id="7b42e-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7b42e-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="7b42e-178">sqlReaderQuery</span></span> |<span data-ttu-id="7b42e-179">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="7b42e-180">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="7b42e-180">SQL query string.</span></span> <span data-ttu-id="7b42e-181">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="7b42e-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="7b42e-182">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-182">No</span></span> |
| <span data-ttu-id="7b42e-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="7b42e-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="7b42e-184">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="7b42e-185">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-185">Name of hello stored procedure.</span></span> <span data-ttu-id="7b42e-186">hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="7b42e-187">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-187">No</span></span> |
| <span data-ttu-id="7b42e-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="7b42e-188">storedProcedureParameters</span></span> |<span data-ttu-id="7b42e-189">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="7b42e-190">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-190">Name/value pairs.</span></span> <span data-ttu-id="7b42e-191">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="7b42e-192">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-192">No</span></span> |

<span data-ttu-id="7b42e-193">경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlDWSource, hello 복사 활동 hello Azure SQL 데이터 웨어하우스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="7b42e-194">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="7b42e-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="7b42e-195">Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello Azure SQL 데이터 웨어하우스 로부터 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-196">예: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="7b42e-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="7b42e-197">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="7b42e-198">SqlDWSource 예제</span><span class="sxs-lookup"><span data-stu-id="7b42e-198">SqlDWSource example</span></span>

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
<span data-ttu-id="7b42e-199">**hello는 프로시저 정의 저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42e-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="7b42e-200">파이프라인</span><span class="sxs-lookup"><span data-stu-id="7b42e-200">SqlDWSink</span></span>
<span data-ttu-id="7b42e-201">**SqlDWSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="7b42e-202">속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-202">Property</span></span> | <span data-ttu-id="7b42e-203">설명</span><span class="sxs-lookup"><span data-stu-id="7b42e-203">Description</span></span> | <span data-ttu-id="7b42e-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="7b42e-204">Allowed values</span></span> | <span data-ttu-id="7b42e-205">필수</span><span class="sxs-lookup"><span data-stu-id="7b42e-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7b42e-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="7b42e-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="7b42e-207">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="7b42e-208">자세한 내용은 [반복성 섹션](#repeatability-during-copy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="7b42e-209">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-209">A query statement.</span></span> |<span data-ttu-id="7b42e-210">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-210">No</span></span> |
| <span data-ttu-id="7b42e-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="7b42e-211">allowPolyBase</span></span> |<span data-ttu-id="7b42e-212">나타냅니다 여부 BULKINSERT 메커니즘 대신 toouse PolyBase (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="7b42e-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="7b42e-213">**PolyBase를 사용 하는 권장 방법은 tooload 데이터를 SQL 데이터 웨어하우스에 하는 hello입니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42e-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="7b42e-214">참조 [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](#use-polybase-to-load-data-into-azure-sql-data-warehouse) 제약 조건 및 세부 정보에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="7b42e-215">True</span><span class="sxs-lookup"><span data-stu-id="7b42e-215">True</span></span> <br/><span data-ttu-id="7b42e-216">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="7b42e-216">False (default)</span></span> |<span data-ttu-id="7b42e-217">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-217">No</span></span> |
| <span data-ttu-id="7b42e-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="7b42e-218">polyBaseSettings</span></span> |<span data-ttu-id="7b42e-219">속성 때 hello 지정할 수 있는 그룹을 **allowPolybase** 너무 속성이**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="7b42e-220">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-220">No</span></span> |
| <span data-ttu-id="7b42e-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="7b42e-221">rejectValue</span></span> |<span data-ttu-id="7b42e-222">Hello 쿼리가 실패 하기 전에 거부 될 수 있는 행의 hello 개수 또는 비율을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="7b42e-223">Hello에 대 한 옵션을 거부 hello PolyBase에 대해 자세히 알아보려면 **인수** 섹션 [CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="7b42e-224">0(기본값), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="7b42e-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="7b42e-225">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-225">No</span></span> |
| <span data-ttu-id="7b42e-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="7b42e-226">rejectType</span></span> |<span data-ttu-id="7b42e-227">리터럴 값 또는 백분율 hello rejectValue 옵션이 지정 되었는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="7b42e-228">값(기본값), 백분율</span><span class="sxs-lookup"><span data-stu-id="7b42e-228">Value (default), Percentage</span></span> |<span data-ttu-id="7b42e-229">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-229">No</span></span> |
| <span data-ttu-id="7b42e-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="7b42e-230">rejectSampleValue</span></span> |<span data-ttu-id="7b42e-231">PolyBase hello 다시 거부 된 행의 hello 비율을 계산 하기 전에 행 tooretrieve hello 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="7b42e-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="7b42e-232">1, 2, …</span></span> |<span data-ttu-id="7b42e-233">예. **rejectType**이 **백분율**인 경우</span><span class="sxs-lookup"><span data-stu-id="7b42e-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="7b42e-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="7b42e-234">useTypeDefault</span></span> |<span data-ttu-id="7b42e-235">PolyBase hello 텍스트 파일에서 데이터를 검색 하는 경우 toohandle 누락 값의 텍스트 파일을 구분 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="7b42e-236">hello 인수 섹션에서이 속성에 대 한 자세한 [CREATE EXTERNAL FILE FORMAT (Transact SQL)](https://msdn.microsoft.com/library/dn935026.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="7b42e-237">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="7b42e-237">True, False (default)</span></span> |<span data-ttu-id="7b42e-238">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-238">No</span></span> |
| <span data-ttu-id="7b42e-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="7b42e-239">writeBatchSize</span></span> |<span data-ttu-id="7b42e-240">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="7b42e-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="7b42e-241">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="7b42e-241">Integer (number of rows)</span></span> |<span data-ttu-id="7b42e-242">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-242">No (default: 10000)</span></span> |
| <span data-ttu-id="7b42e-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="7b42e-243">writeBatchTimeout</span></span> |<span data-ttu-id="7b42e-244">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="7b42e-245">timespan</span><span class="sxs-lookup"><span data-stu-id="7b42e-245">timespan</span></span><br/><br/> <span data-ttu-id="7b42e-246">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="7b42e-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="7b42e-247">아니요</span><span class="sxs-lookup"><span data-stu-id="7b42e-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="7b42e-248">SqlDWSink 예제</span><span class="sxs-lookup"><span data-stu-id="7b42e-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="7b42e-249">PolyBase tooload 데이터를 사용 하 여 Azure SQL 데이터 웨어하우스로</span><span class="sxs-lookup"><span data-stu-id="7b42e-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7b42e-250">**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**를 사용하는 것은 처리량이 높은 많은 양의 데이터를 Azure SQL Data Warehouse에 로드하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="7b42e-251">Hello 처리량이 많은 향상 된 hello 기본 BULKINSERT 메커니즘 대신 PolyBase를 사용 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="7b42e-252">자세히 비교하려면 [복사 성능 참조 번호](data-factory-copy-activity-performance.md#performance-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="7b42e-253">사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="7b42e-254">원본 데이터에 있으면 **Azure Blob 또는 Azure 데이터 레이크 저장소**, 및 hello 형식은 PolyBase와 호환, PolyBase를 사용 하 여 SQL 데이터 웨어하우스 tooAzure 직접 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="7b42e-255">자세한 내용은 **[PolyBase를 사용하여 직접 복사](#direct-copy-using-polybase)**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="7b42e-256">원본 데이터 저장소와 형식이 지원 되지 않는 원래 PolyBase에서 사용 하 여 hello  **[PolyBase를 사용 하 여 준비 된 복사본](#staged-copy-using-polybase)**  대신 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="7b42e-257">또한 제공 하면 처리량이 더 자동으로 hello 데이터 PolyBase 호환 가능한 형식으로 변환 하 고 hello 데이터를 Azure Blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="7b42e-258">그런 다음 SQL Data Warehouse에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="7b42e-259">집합 hello `allowPolyBase` 속성 너무**true** hello Azure SQL 데이터 웨어하우스로 다음 Azure Data Factory toouse PolyBase toocopy 데이터에 대 한 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-260">AllowPolyBase tootrue 설정 하는 경우에 hello를 사용 하 여 PolyBase 특정 속성을 지정할 수 있습니다 `polyBaseSettings` 속성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="7b42e-261">hello 참조 [SqlDWSink](#SqlDWSink) polyBaseSettings 함께 사용할 수 있는 속성에 대 한 세부 정보에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42e-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="7b42e-262">PolyBase를 사용하여 직접 복사</span><span class="sxs-lookup"><span data-stu-id="7b42e-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="7b42e-263">SQL Data Warehouse PolyBase는 Azure Blob 및 Azure Data Lake Store(서비스 주체 사용)를 원본으로 직접 지원하며 특정 파일 형식 요구 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="7b42e-264">원본 데이터에이 섹션에 설명 된 hello 조건에 부합 하는 경우에 원본 데이터 저장소 tooAzure PolyBase를 사용 하 여 SQL 데이터 웨어하우스에서 직접 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="7b42e-265">그렇지 않을 경우, [PolyBase를 사용하여 준비한 복사본](#staged-copy-using-polybase)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="7b42e-266">데이터 레이크 저장소 tooSQL 데이터 웨어하우스에서에서 toocopy 데이터를 효율적으로 자세한 정보에서 [Azure 데이터 팩터리를 사용 하면 더 쉽고 편리 하 게 toouncover 데이터 로부터 이해를 포함 하 여 SQL 데이터 웨어하우스에 데이터 레이크 저장소를 사용 하는 경우](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="7b42e-267">Hello 요구 사항이 충족 되지 않는 Azure Data Factory hello 설정을 확인 하 고 hello 데이터 이동 위한 toohello BULKINSERT 메커니즘 자동으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="7b42e-268">**원본에 연결된 서비스**의 형식은 **AzureStorage** 또는 **서비스 주체 인증이 적용된 AzureDataLakeStore**입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="7b42e-269">hello **입력된 데이터 집합** 유형의: **AzureBlob** 또는 **AzureDataLakeStore**에서 형식을 hello 및 `type` 속성은 **OrcFormat** , 또는 **TextFormat** 하는 구성을 따르고 hello로:</span><span class="sxs-lookup"><span data-stu-id="7b42e-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="7b42e-270">`rowDelimiter`는 **\n**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="7b42e-271">`nullValue`너무 설정**빈 문자열** (""), 또는 `treatEmptyAsNull` 너무 설정**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="7b42e-272">`encodingName`너무 설정**u t f-8**, 즉 **기본** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="7b42e-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` 및 `skipLineCount`는 지정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="7b42e-274">`compression`은 **no compression**, **GZip** 또는 **Deflate**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="7b42e-275">없는 `skipHeaderLineCount` 설정을 **BlobSource** 또는 **AzureDataLakeStore** hello hello 파이프라인에서 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="7b42e-276">없는 `sliceIdentifierColumnName` 설정을 **SqlDWSink** hello hello 파이프라인에서 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="7b42e-277">(PolyBase는 한 번의 실행으로 모든 데이터를 업데이트하거나 아무 것도 업데이트하지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="7b42e-278">tooachieve **반복성**를 사용할 수 있습니다 `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="7b42e-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="7b42e-279">없는 `columnMapping` 복사 작업에 연결 된 hello에서 사용 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="7b42e-280">PolyBase를 사용하여 준비한 복사본</span><span class="sxs-lookup"><span data-stu-id="7b42e-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="7b42e-281">원본 데이터 hello 이전 섹션에 도입 된 hello 조건 충족 하지 않는 경우 중간 준비 Azure Blob 저장소 (프리미엄 저장소 수 없음)를 통해 데이터 복사를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="7b42e-282">이 경우 Azure 데이터 팩터리 자동으로 hello 데이터 toomeet 데이터 형식 요구 사항을 PolyBase를 사용 하 여 PolyBase tooload 데이터의 SQL 데이터 웨어하우스로 변환을 수행 및 최초의 정리 hello Blob 저장소에서 임시 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="7b42e-283">스테이징 Azure Blob을 통해 데이터를 복사하는 방법에 대한 자세한 내용은 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="7b42e-284">PolyBase를 사용 하 여 Azure SQL 데이터 웨어하우스에 저장 합니다. 온-프레미스 데이터에서 데이터를 복사 하 고 준비를 사용 중인 데이터 관리 게이트웨이 버전 2.4 미만인 경우 JRE (Java Runtime Environment) 게이트웨이에 필요한 컴퓨터를 사용 하는 tootransform 원본 데이터는 적절 한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="7b42e-285">이와 같은 종속성 게이트웨이 toohello 최신 tooavoid를 업그레이드 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="7b42e-286">toouse이 기능을 만듭니다는 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) toohello hello 중간 blob 저장소에 있는 Azure 저장소 계정을 참조 하는, 다음 hello 지정 `enableStaging` 및 `stagingSettings` hello 복사 작업에 대 한 속성 와 같이 코드 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="7b42e-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="7b42e-287">PolyBase를 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="7b42e-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="7b42e-288">hello 다음 섹션에서는 추가 모범 사례 toohello에서 설명 하는 스토리 [Azure SQL 데이터 웨어하우스에 대 한 모범 사례](../sql-data-warehouse/sql-data-warehouse-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="7b42e-289">필수 데이터베이스 권한</span><span class="sxs-lookup"><span data-stu-id="7b42e-289">Required database permission</span></span>
<span data-ttu-id="7b42e-290">PolyBase toouse 필요 hello 사용자 되 고 사용 되는 tooload 데이터를 SQL 데이터 웨어하우스에 hello ["권한"](https://msdn.microsoft.com/library/ms191291.aspx) hello 대상 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="7b42e-291">Tooadd는 한 가지 방법은 tooachieve "db_owner" 역할의 멤버인 사용자에 게 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="7b42e-292">자세한 내용은 방법 toodo 따르면 [이 섹션](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="7b42e-293">행 크기 및 데이터 형식 제한 사항</span><span class="sxs-lookup"><span data-stu-id="7b42e-293">Row size and data type limitation</span></span>
<span data-ttu-id="7b42e-294">Polybase 부하는 제한 된 tooloading 행 모두 보다 작은 **1MB** tooVARCHR(MAX)를 로드할 수 없습니다 및 nvarchar (max) 또는 varbinary (max).</span><span class="sxs-lookup"><span data-stu-id="7b42e-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="7b42e-295">너무 참조[여기](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="7b42e-296">크기가 1MB 보다 큰 행을 사용 하 여 원본 데이터를 설정한 경우 toosplit hello 원본 테이블 세로로를 각각의 최대 행 크기 hello hello 제한을 초과 하지 않는 여러 개의 작은 시나리오로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="7b42e-297">Azure SQL 데이터 웨어하우스에 함께 병합 하 고 PolyBase를 사용 하 여 hello 작은 테이블로 다음 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="7b42e-298">SQL Data Warehouse 리소스 클래스</span><span class="sxs-lookup"><span data-stu-id="7b42e-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="7b42e-299">최상의 가능한 처리량 tooachieve tooassign 큰 리소스 클래스 toohello 사용자 되 고 하는 것이 좋습니다. PolyBase 통해 SQL 데이터 웨어하우스로 tooload 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="7b42e-300">자세한 방법을 toodo를 따르면 [사용자 리소스 클래스 예제 변경](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="7b42e-301">Azure SQL 데이터 웨어하우스의 tableName</span><span class="sxs-lookup"><span data-stu-id="7b42e-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7b42e-302">hello 다음 표에서 예제에 대해 방법 toospecify hello **tableName** JSON 스키마와 테이블 이름의 다양 한 조합에 대 한 데이터 집합의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="7b42e-303">DB 스키마</span><span class="sxs-lookup"><span data-stu-id="7b42e-303">DB Schema</span></span> | <span data-ttu-id="7b42e-304">테이블 이름</span><span class="sxs-lookup"><span data-stu-id="7b42e-304">Table name</span></span> | <span data-ttu-id="7b42e-305">tableName JSON 속성</span><span class="sxs-lookup"><span data-stu-id="7b42e-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b42e-306">dbo</span><span class="sxs-lookup"><span data-stu-id="7b42e-306">dbo</span></span> |<span data-ttu-id="7b42e-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="7b42e-307">MyTable</span></span> |<span data-ttu-id="7b42e-308">MyTable 또는 dbo.MyTable 또는 [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="7b42e-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="7b42e-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="7b42e-309">dbo1</span></span> |<span data-ttu-id="7b42e-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="7b42e-310">MyTable</span></span> |<span data-ttu-id="7b42e-311">dbo1.MyTable 또는 [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="7b42e-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="7b42e-312">dbo</span><span class="sxs-lookup"><span data-stu-id="7b42e-312">dbo</span></span> |<span data-ttu-id="7b42e-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="7b42e-313">My.Table</span></span> |<span data-ttu-id="7b42e-314">[My.Table] 또는 [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="7b42e-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="7b42e-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="7b42e-315">dbo1</span></span> |<span data-ttu-id="7b42e-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="7b42e-316">My.Table</span></span> |<span data-ttu-id="7b42e-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="7b42e-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="7b42e-318">Hello 다음 오류가 표시 되 면 hello tableName 속성에 대 한 지정 된 값이 hello 문제일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="7b42e-319">Hello hello tableName JSON 속성에 대 한 hello 올바른 방법은 toospecify 값 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b42e-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="7b42e-320">기본값이 있는 열</span><span class="sxs-lookup"><span data-stu-id="7b42e-320">Columns with default values</span></span>
<span data-ttu-id="7b42e-321">현재, PolyBase 기능 Data Factory에만 허용 hello hello 대상 테이블에 나와 있듯이 열 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="7b42e-322">가령 네 개의 열이 있고 그 중 한 열이 기본 값으로 정의된 테이블이 있다고 합시다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="7b42e-323">hello 입력된 데이터는 4 개의 열을 포함 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="7b42e-324">3 열 입력된 데이터 집합을 제공 하는 오류와 비슷한 toohello 메시지의 뒤에 생성:</span><span class="sxs-lookup"><span data-stu-id="7b42e-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="7b42e-325">NULL 값은 특별한 형태의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="7b42e-326">Hello 입력된 데이터 (blob) 해당 열에 대 한 hello 열에서 null을 허용 하는 경우 비어 있을 수 있습니다 (hello 입력된 데이터 집합에서 누락 될 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="7b42e-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="7b42e-327">PolyBase hello Azure SQL 데이터 웨어하우스 NULL을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="7b42e-328">자동 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="7b42e-328">Auto table creation</span></span>
<span data-ttu-id="7b42e-329">SQL Server에서 toocopy 데이터 복사 마법사를 사용 하는 경우, Azure SQL 데이터베이스 tooAzure SQL 데이터 웨어하우스 및 hello 테이블 toohello 원본 테이블의 해당 hello 대상 저장소에 없습니다. Data Factory 자동으로 hello 테이블을에서 만들 수 hello hello 원본 테이블 스키마를 사용 하 여 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="7b42e-330">데이터 팩터리 hello 대상 저장소에 hello 표를 만들고 hello 동일한 hello 원본 데이터 저장소에는 이름 테이블로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="7b42e-331">hello 데이터 형식 열에 대 한 형식 매핑을 수행 하는 hello에 따라 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="7b42e-332">필요한 경우 형식 변환 toofix 소스 및 대상 저장소 간의 비 호환성 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="7b42e-333">라운드 로빈 테이블 배포를 사용하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="7b42e-334">원본 SQL Database 열 형식</span><span class="sxs-lookup"><span data-stu-id="7b42e-334">Source SQL Database column type</span></span> | <span data-ttu-id="7b42e-335">대상 SQL DW 열 유형(크기 제한)</span><span class="sxs-lookup"><span data-stu-id="7b42e-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="7b42e-336">int</span><span class="sxs-lookup"><span data-stu-id="7b42e-336">Int</span></span> | <span data-ttu-id="7b42e-337">int</span><span class="sxs-lookup"><span data-stu-id="7b42e-337">Int</span></span> |
| <span data-ttu-id="7b42e-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-338">BigInt</span></span> | <span data-ttu-id="7b42e-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-339">BigInt</span></span> |
| <span data-ttu-id="7b42e-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-340">SmallInt</span></span> | <span data-ttu-id="7b42e-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-341">SmallInt</span></span> |
| <span data-ttu-id="7b42e-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-342">TinyInt</span></span> | <span data-ttu-id="7b42e-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="7b42e-343">TinyInt</span></span> |
| <span data-ttu-id="7b42e-344">Bit</span><span class="sxs-lookup"><span data-stu-id="7b42e-344">Bit</span></span> | <span data-ttu-id="7b42e-345">Bit</span><span class="sxs-lookup"><span data-stu-id="7b42e-345">Bit</span></span> |
| <span data-ttu-id="7b42e-346">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-346">Decimal</span></span> | <span data-ttu-id="7b42e-347">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-347">Decimal</span></span> |
| <span data-ttu-id="7b42e-348">숫자</span><span class="sxs-lookup"><span data-stu-id="7b42e-348">Numeric</span></span> | <span data-ttu-id="7b42e-349">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-349">Decimal</span></span> |
| <span data-ttu-id="7b42e-350">Float</span><span class="sxs-lookup"><span data-stu-id="7b42e-350">Float</span></span> | <span data-ttu-id="7b42e-351">Float</span><span class="sxs-lookup"><span data-stu-id="7b42e-351">Float</span></span> |
| <span data-ttu-id="7b42e-352">Money</span><span class="sxs-lookup"><span data-stu-id="7b42e-352">Money</span></span> | <span data-ttu-id="7b42e-353">Money</span><span class="sxs-lookup"><span data-stu-id="7b42e-353">Money</span></span> |
| <span data-ttu-id="7b42e-354">Real</span><span class="sxs-lookup"><span data-stu-id="7b42e-354">Real</span></span> | <span data-ttu-id="7b42e-355">Real</span><span class="sxs-lookup"><span data-stu-id="7b42e-355">Real</span></span> |
| <span data-ttu-id="7b42e-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="7b42e-356">SmallMoney</span></span> | <span data-ttu-id="7b42e-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="7b42e-357">SmallMoney</span></span> |
| <span data-ttu-id="7b42e-358">이진</span><span class="sxs-lookup"><span data-stu-id="7b42e-358">Binary</span></span> | <span data-ttu-id="7b42e-359">이진</span><span class="sxs-lookup"><span data-stu-id="7b42e-359">Binary</span></span> |
| <span data-ttu-id="7b42e-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="7b42e-360">Varbinary</span></span> | <span data-ttu-id="7b42e-361">Varbinary (위쪽 too8000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="7b42e-362">Date</span><span class="sxs-lookup"><span data-stu-id="7b42e-362">Date</span></span> | <span data-ttu-id="7b42e-363">Date</span><span class="sxs-lookup"><span data-stu-id="7b42e-363">Date</span></span> |
| <span data-ttu-id="7b42e-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-364">DateTime</span></span> | <span data-ttu-id="7b42e-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-365">DateTime</span></span> |
| <span data-ttu-id="7b42e-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="7b42e-366">DateTime2</span></span> | <span data-ttu-id="7b42e-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="7b42e-367">DateTime2</span></span> |
| <span data-ttu-id="7b42e-368">Time</span><span class="sxs-lookup"><span data-stu-id="7b42e-368">Time</span></span> | <span data-ttu-id="7b42e-369">Time</span><span class="sxs-lookup"><span data-stu-id="7b42e-369">Time</span></span> |
| <span data-ttu-id="7b42e-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="7b42e-370">DateTimeOffset</span></span> | <span data-ttu-id="7b42e-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="7b42e-371">DateTimeOffset</span></span> |
| <span data-ttu-id="7b42e-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-372">SmallDateTime</span></span> | <span data-ttu-id="7b42e-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-373">SmallDateTime</span></span> |
| <span data-ttu-id="7b42e-374">텍스트</span><span class="sxs-lookup"><span data-stu-id="7b42e-374">Text</span></span> | <span data-ttu-id="7b42e-375">Varchar (위쪽 too8000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="7b42e-376">NText</span><span class="sxs-lookup"><span data-stu-id="7b42e-376">NText</span></span> | <span data-ttu-id="7b42e-377">NVarChar (위쪽 too4000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="7b42e-378">이미지</span><span class="sxs-lookup"><span data-stu-id="7b42e-378">Image</span></span> | <span data-ttu-id="7b42e-379">VarBinary (위쪽 too8000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="7b42e-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="7b42e-380">UniqueIdentifier</span></span> | <span data-ttu-id="7b42e-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="7b42e-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="7b42e-382">Char</span><span class="sxs-lookup"><span data-stu-id="7b42e-382">Char</span></span> | <span data-ttu-id="7b42e-383">Char</span><span class="sxs-lookup"><span data-stu-id="7b42e-383">Char</span></span> |
| <span data-ttu-id="7b42e-384">NChar</span><span class="sxs-lookup"><span data-stu-id="7b42e-384">NChar</span></span> | <span data-ttu-id="7b42e-385">NChar</span><span class="sxs-lookup"><span data-stu-id="7b42e-385">NChar</span></span> |
| <span data-ttu-id="7b42e-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="7b42e-386">VarChar</span></span> | <span data-ttu-id="7b42e-387">VarChar (위쪽 too8000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="7b42e-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="7b42e-388">NVarChar</span></span> | <span data-ttu-id="7b42e-389">NVarChar (위쪽 too4000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="7b42e-390">xml</span><span class="sxs-lookup"><span data-stu-id="7b42e-390">Xml</span></span> | <span data-ttu-id="7b42e-391">Varchar (위쪽 too8000)</span><span class="sxs-lookup"><span data-stu-id="7b42e-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="7b42e-392">Azure SQL 데이터 웨어하우스에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="7b42e-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7b42e-393">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 단계 2 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="7b42e-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="7b42e-394">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="7b42e-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="7b42e-395">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="7b42e-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="7b42e-396">를 너무 및 Azure SQL 데이터 웨어하우스 로부터 데이터를 이동할 때는 hello 다음 매핑은 사용 하는 SQL 유형 too.NET 형식에서 그 반대의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="7b42e-397">hello 매핑 hello와 같습니다. [ADO.NET에 대 한 SQL Server 데이터 형식 매핑](https://msdn.microsoft.com/library/cc716729.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="7b42e-398">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="7b42e-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="7b42e-399">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="7b42e-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="7b42e-400">bigint</span><span class="sxs-lookup"><span data-stu-id="7b42e-400">bigint</span></span> |<span data-ttu-id="7b42e-401">Int64</span><span class="sxs-lookup"><span data-stu-id="7b42e-401">Int64</span></span> |
| <span data-ttu-id="7b42e-402">binary</span><span class="sxs-lookup"><span data-stu-id="7b42e-402">binary</span></span> |<span data-ttu-id="7b42e-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-403">Byte[]</span></span> |
| <span data-ttu-id="7b42e-404">bit</span><span class="sxs-lookup"><span data-stu-id="7b42e-404">bit</span></span> |<span data-ttu-id="7b42e-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="7b42e-405">Boolean</span></span> |
| <span data-ttu-id="7b42e-406">char</span><span class="sxs-lookup"><span data-stu-id="7b42e-406">char</span></span> |<span data-ttu-id="7b42e-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-407">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-408">date</span><span class="sxs-lookup"><span data-stu-id="7b42e-408">date</span></span> |<span data-ttu-id="7b42e-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-409">DateTime</span></span> |
| <span data-ttu-id="7b42e-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-410">Datetime</span></span> |<span data-ttu-id="7b42e-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-411">DateTime</span></span> |
| <span data-ttu-id="7b42e-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="7b42e-412">datetime2</span></span> |<span data-ttu-id="7b42e-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-413">DateTime</span></span> |
| <span data-ttu-id="7b42e-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="7b42e-414">Datetimeoffset</span></span> |<span data-ttu-id="7b42e-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="7b42e-415">DateTimeOffset</span></span> |
| <span data-ttu-id="7b42e-416">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-416">Decimal</span></span> |<span data-ttu-id="7b42e-417">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-417">Decimal</span></span> |
| <span data-ttu-id="7b42e-418">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="7b42e-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="7b42e-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-419">Byte[]</span></span> |
| <span data-ttu-id="7b42e-420">Float</span><span class="sxs-lookup"><span data-stu-id="7b42e-420">Float</span></span> |<span data-ttu-id="7b42e-421">Double</span><span class="sxs-lookup"><span data-stu-id="7b42e-421">Double</span></span> |
| <span data-ttu-id="7b42e-422">이미지</span><span class="sxs-lookup"><span data-stu-id="7b42e-422">image</span></span> |<span data-ttu-id="7b42e-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-423">Byte[]</span></span> |
| <span data-ttu-id="7b42e-424">int</span><span class="sxs-lookup"><span data-stu-id="7b42e-424">int</span></span> |<span data-ttu-id="7b42e-425">Int32</span><span class="sxs-lookup"><span data-stu-id="7b42e-425">Int32</span></span> |
| <span data-ttu-id="7b42e-426">money</span><span class="sxs-lookup"><span data-stu-id="7b42e-426">money</span></span> |<span data-ttu-id="7b42e-427">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-427">Decimal</span></span> |
| <span data-ttu-id="7b42e-428">nchar</span><span class="sxs-lookup"><span data-stu-id="7b42e-428">nchar</span></span> |<span data-ttu-id="7b42e-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-429">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-430">ntext</span><span class="sxs-lookup"><span data-stu-id="7b42e-430">ntext</span></span> |<span data-ttu-id="7b42e-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-431">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-432">numeric</span><span class="sxs-lookup"><span data-stu-id="7b42e-432">numeric</span></span> |<span data-ttu-id="7b42e-433">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-433">Decimal</span></span> |
| <span data-ttu-id="7b42e-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="7b42e-434">nvarchar</span></span> |<span data-ttu-id="7b42e-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-435">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-436">real</span><span class="sxs-lookup"><span data-stu-id="7b42e-436">real</span></span> |<span data-ttu-id="7b42e-437">단일</span><span class="sxs-lookup"><span data-stu-id="7b42e-437">Single</span></span> |
| <span data-ttu-id="7b42e-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="7b42e-438">rowversion</span></span> |<span data-ttu-id="7b42e-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-439">Byte[]</span></span> |
| <span data-ttu-id="7b42e-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="7b42e-440">smalldatetime</span></span> |<span data-ttu-id="7b42e-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="7b42e-441">DateTime</span></span> |
| <span data-ttu-id="7b42e-442">smallint</span><span class="sxs-lookup"><span data-stu-id="7b42e-442">smallint</span></span> |<span data-ttu-id="7b42e-443">Int16</span><span class="sxs-lookup"><span data-stu-id="7b42e-443">Int16</span></span> |
| <span data-ttu-id="7b42e-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="7b42e-444">smallmoney</span></span> |<span data-ttu-id="7b42e-445">10진수</span><span class="sxs-lookup"><span data-stu-id="7b42e-445">Decimal</span></span> |
| <span data-ttu-id="7b42e-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="7b42e-446">sql_variant</span></span> |<span data-ttu-id="7b42e-447">개체 *</span><span class="sxs-lookup"><span data-stu-id="7b42e-447">Object *</span></span> |
| <span data-ttu-id="7b42e-448">텍스트</span><span class="sxs-lookup"><span data-stu-id="7b42e-448">text</span></span> |<span data-ttu-id="7b42e-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-449">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-450">실시간</span><span class="sxs-lookup"><span data-stu-id="7b42e-450">time</span></span> |<span data-ttu-id="7b42e-451">timespan</span><span class="sxs-lookup"><span data-stu-id="7b42e-451">TimeSpan</span></span> |
| <span data-ttu-id="7b42e-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="7b42e-452">timestamp</span></span> |<span data-ttu-id="7b42e-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-453">Byte[]</span></span> |
| <span data-ttu-id="7b42e-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="7b42e-454">tinyint</span></span> |<span data-ttu-id="7b42e-455">Byte</span><span class="sxs-lookup"><span data-stu-id="7b42e-455">Byte</span></span> |
| <span data-ttu-id="7b42e-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="7b42e-456">uniqueidentifier</span></span> |<span data-ttu-id="7b42e-457">Guid</span><span class="sxs-lookup"><span data-stu-id="7b42e-457">Guid</span></span> |
| <span data-ttu-id="7b42e-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="7b42e-458">varbinary</span></span> |<span data-ttu-id="7b42e-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-459">Byte[]</span></span> |
| <span data-ttu-id="7b42e-460">varchar</span><span class="sxs-lookup"><span data-stu-id="7b42e-460">varchar</span></span> |<span data-ttu-id="7b42e-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="7b42e-461">String, Char[]</span></span> |
| <span data-ttu-id="7b42e-462">xml</span><span class="sxs-lookup"><span data-stu-id="7b42e-462">xml</span></span> |<span data-ttu-id="7b42e-463">xml</span><span class="sxs-lookup"><span data-stu-id="7b42e-463">Xml</span></span> |

<span data-ttu-id="7b42e-464">원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="7b42e-465">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b42e-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="7b42e-466">SQL 데이터 웨어하우스에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="7b42e-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="7b42e-467">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7b42e-468">표시 방법을 Azure SQL 데이터 웨어하우스 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="7b42e-469">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="7b42e-470">예: Azure SQL 데이터 웨어하우스 tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="7b42e-471">hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="7b42e-472">[AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="7b42e-473">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7b42e-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7b42e-474">[AzureSqlDWTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="7b42e-475">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="7b42e-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7b42e-476">[SqlDWSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7b42e-477">hello 샘플 시계열 (시간별, 일별, 등) 데이터 복사 Azure SQL 데이터 웨어하우스 데이터베이스 tooa blob의 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="7b42e-478">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="7b42e-479">**Azure SQL 데이터 웨어하우스 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="7b42e-480">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="7b42e-481">**Azure SQL 데이터 웨어하우스 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="7b42e-482">hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 데이터 웨어하우스 및 포함 된 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="7b42e-483">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="7b42e-484">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="7b42e-485">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="7b42e-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7b42e-486">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="7b42e-487">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="7b42e-488">**SqlDWSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="7b42e-489">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="7b42e-490">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlDWSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="7b42e-491">hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="7b42e-492">Hello 예에서 **sqlReaderQuery** SqlDWSource hello에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="7b42e-493">복사 활동 hello hello Azure SQL 데이터 웨어하우스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="7b42e-494">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="7b42e-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="7b42e-495">Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열은 사용 되는 toobuild 쿼리 (select column1, column2 mytable에서) sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 Azure SQL 데이터 웨어하우스 hello에 대 한 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-496">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="7b42e-497">예: Azure Blob tooAzure SQL 데이터 웨어하우스에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="7b42e-498">hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="7b42e-499">[AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="7b42e-500">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7b42e-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7b42e-501">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="7b42e-502">[AzureSqlDWTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="7b42e-503">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlDWSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="7b42e-504">hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터 웨어하우스 데이터베이스의 Azure blob tooa 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="7b42e-505">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="7b42e-506">**Azure SQL 데이터 웨어하우스 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="7b42e-507">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="7b42e-508">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="7b42e-509">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7b42e-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7b42e-510">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="7b42e-511">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="7b42e-512">"external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="7b42e-513">**Azure SQL 데이터 웨어하우스 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="7b42e-514">hello 샘플 Azure SQL 데이터 웨어하우스에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b42e-515">와 Azure SQL 데이터 웨어하우스에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="7b42e-516">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-516">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="7b42e-517">**BlobSource 및 SqlDWSink를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="7b42e-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="7b42e-518">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="7b42e-519">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlDWSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

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
<span data-ttu-id="7b42e-520">연습을 참조 하는 hello를 참조 하세요. [15 분 미만 Azure 데이터 팩터리에 Azure SQL 데이터 웨어하우스를 1TB를 로드](data-factory-load-sql-data-warehouse.md) 및 [Azure 데이터 팩터리를 사용 하 여 데이터 로드](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL 데이터 웨어하우스의에서 문서 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7b42e-521">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="7b42e-521">Performance and Tuning</span></span>
<span data-ttu-id="7b42e-522">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42e-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
