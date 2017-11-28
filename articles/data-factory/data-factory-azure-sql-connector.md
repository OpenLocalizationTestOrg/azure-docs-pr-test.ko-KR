---
title: "Azure SQL 데이터베이스에서 데이터를 aaaCopy | Microsoft Docs"
description: "자세한 방법을 toocopy 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터베이스입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="bd9cf-103">Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터베이스에서 데이터 tooand 복사</span><span class="sxs-lookup"><span data-stu-id="bd9cf-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="bd9cf-104">이 문서에서는 toouse 복사 작업에서 Azure SQL 데이터베이스에서 Azure Data Factory toomove 데이터 tooand hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="bd9cf-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="bd9cf-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="bd9cf-106">Supported scenarios</span></span>
<span data-ttu-id="bd9cf-107">데이터를 복사할 수 **Azure SQL 데이터베이스에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="bd9cf-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="bd9cf-108">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure SQL 데이터베이스**:</span><span class="sxs-lookup"><span data-stu-id="bd9cf-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="bd9cf-109">지원되는 인증 유형</span><span class="sxs-lookup"><span data-stu-id="bd9cf-109">Supported authentication type</span></span>
<span data-ttu-id="bd9cf-110">Azure SQL Database 커넥터는 기본 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd9cf-111">시작</span><span class="sxs-lookup"><span data-stu-id="bd9cf-111">Getting started</span></span>
<span data-ttu-id="bd9cf-112">다른 도구/API를 사용하여 Azure SQL Database 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="bd9cf-113">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="bd9cf-114">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="bd9cf-115">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bd9cf-116">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="bd9cf-117">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="bd9cf-118">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-118">Create a **data factory**.</span></span> <span data-ttu-id="bd9cf-119">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="bd9cf-120">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="bd9cf-121">예를 들어 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="bd9cf-122">연결 된 서비스 속성 특정 tooAzure SQL 데이터베이스에 대해 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="bd9cf-123">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="bd9cf-124">Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="bd9cf-125">고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터베이스에서 다른 데이터 집합 toospecify hello SQL 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="bd9cf-126">특정 tooAzure 데이터 레이크 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="bd9cf-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="bd9cf-128">앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlSink 싱크도 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="bd9cf-129">마찬가지로, Azure SQL 데이터베이스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlSource 및 사용 BlobSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="bd9cf-130">복사 활동 속성을 특정 tooAzure SQL 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="bd9cf-131">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="bd9cf-132">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="bd9cf-133">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="bd9cf-134">샘플 은/Azure SQL 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-sql-database) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="bd9cf-135">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure SQL 데이터베이스에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="bd9cf-136">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-136">Linked service properties</span></span>
<span data-ttu-id="bd9cf-137">Azure SQL 한 Azure SQL 데이터베이스 tooyour 데이터 팩터리 서비스 링크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="bd9cf-138">다음 표에서 hello JSON 요소 특정 tooAzure SQL에 대 한 연결 된 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="bd9cf-139">속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-139">Property</span></span> | <span data-ttu-id="bd9cf-140">설명</span><span class="sxs-lookup"><span data-stu-id="bd9cf-140">Description</span></span> | <span data-ttu-id="bd9cf-141">필수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd9cf-142">type</span><span class="sxs-lookup"><span data-stu-id="bd9cf-142">type</span></span> |<span data-ttu-id="bd9cf-143">hello type 속성 설정 해야 합니다: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="bd9cf-144">예</span><span class="sxs-lookup"><span data-stu-id="bd9cf-144">Yes</span></span> |
| <span data-ttu-id="bd9cf-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="bd9cf-145">connectionString</span></span> |<span data-ttu-id="bd9cf-146">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="bd9cf-147">기본 인증만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="bd9cf-148">예</span><span class="sxs-lookup"><span data-stu-id="bd9cf-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bd9cf-149">구성 [Azure SQL 데이터베이스 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 데이터베이스 서버를 너무 hello[Azure 서비스 tooaccess hello 서버](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="bd9cf-150">또한 외부 Azure 비롯 하 여 데이터 팩터리 게이트웨이와 온-프레미스 데이터 원본에서 데이터 tooAzure SQL 데이터베이스를 복사 하는 경우 데이터 tooAzure SQL 데이터베이스를 전송 하는 hello 컴퓨터에 대 한 적절 한 IP 주소 범위를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="bd9cf-151">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-151">Dataset properties</span></span>
<span data-ttu-id="bd9cf-152">데이터 집합 toorepresent toospecify hello 데이터 집합의 hello 형식 속성을 설정 Azure SQL 데이터베이스에 입력 또는 출력 데이터: **AzureSqlTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="bd9cf-153">집합 hello **linkedServiceName** hello SQL Azure의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="bd9cf-154">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bd9cf-155">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bd9cf-156">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="bd9cf-157">hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureSqlTable** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="bd9cf-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="bd9cf-158">속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-158">Property</span></span> | <span data-ttu-id="bd9cf-159">설명</span><span class="sxs-lookup"><span data-stu-id="bd9cf-159">Description</span></span> | <span data-ttu-id="bd9cf-160">필수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd9cf-161">tableName</span><span class="sxs-lookup"><span data-stu-id="bd9cf-161">tableName</span></span> |<span data-ttu-id="bd9cf-162">Hello 테이블 또는 뷰의 연결 된 서비스는 hello Azure SQL 데이터베이스 인스턴스의 이름이 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="bd9cf-163">예</span><span class="sxs-lookup"><span data-stu-id="bd9cf-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bd9cf-164">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-164">Copy activity properties</span></span>
<span data-ttu-id="bd9cf-165">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bd9cf-166">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="bd9cf-167">복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="bd9cf-168">반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="bd9cf-169">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="bd9cf-170">Azure SQL 데이터베이스에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**SqlSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="bd9cf-171">마찬가지로, 데이터 tooan Azure SQL 데이터베이스를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="bd9cf-172">이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="bd9cf-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="bd9cf-173">SqlSource</span></span>
<span data-ttu-id="bd9cf-174">Hello 원본 유형인 경우 복사 활동에서 **SqlSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="bd9cf-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="bd9cf-175">속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-175">Property</span></span> | <span data-ttu-id="bd9cf-176">설명</span><span class="sxs-lookup"><span data-stu-id="bd9cf-176">Description</span></span> | <span data-ttu-id="bd9cf-177">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="bd9cf-177">Allowed values</span></span> | <span data-ttu-id="bd9cf-178">필수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd9cf-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="bd9cf-179">sqlReaderQuery</span></span> |<span data-ttu-id="bd9cf-180">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="bd9cf-181">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-181">SQL query string.</span></span> <span data-ttu-id="bd9cf-182">예: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="bd9cf-183">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-183">No</span></span> |
| <span data-ttu-id="bd9cf-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="bd9cf-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="bd9cf-185">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="bd9cf-186">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-186">Name of hello stored procedure.</span></span> <span data-ttu-id="bd9cf-187">hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="bd9cf-188">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-188">No</span></span> |
| <span data-ttu-id="bd9cf-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="bd9cf-189">storedProcedureParameters</span></span> |<span data-ttu-id="bd9cf-190">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="bd9cf-191">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-191">Name/value pairs.</span></span> <span data-ttu-id="bd9cf-192">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="bd9cf-193">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-193">No</span></span> |

<span data-ttu-id="bd9cf-194">경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello Azure SQL 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="bd9cf-195">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="bd9cf-196">Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열은 사용 되는 toobuild 쿼리 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 (`select column1, column2 from mytable`) toorun hello Azure SQL 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="bd9cf-197">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="bd9cf-198">사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="bd9cf-199">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="bd9cf-200">SqlSource 예제</span><span class="sxs-lookup"><span data-stu-id="bd9cf-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="bd9cf-201">**hello는 프로시저 정의 저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="bd9cf-202">파이프라인</span><span class="sxs-lookup"><span data-stu-id="bd9cf-202">SqlSink</span></span>
<span data-ttu-id="bd9cf-203">**SqlSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="bd9cf-204">속성</span><span class="sxs-lookup"><span data-stu-id="bd9cf-204">Property</span></span> | <span data-ttu-id="bd9cf-205">설명</span><span class="sxs-lookup"><span data-stu-id="bd9cf-205">Description</span></span> | <span data-ttu-id="bd9cf-206">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="bd9cf-206">Allowed values</span></span> | <span data-ttu-id="bd9cf-207">필수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd9cf-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="bd9cf-208">writeBatchTimeout</span></span> |<span data-ttu-id="bd9cf-209">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="bd9cf-210">timespan</span><span class="sxs-lookup"><span data-stu-id="bd9cf-210">timespan</span></span><br/><br/> <span data-ttu-id="bd9cf-211">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="bd9cf-212">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-212">No</span></span> |
| <span data-ttu-id="bd9cf-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="bd9cf-213">writeBatchSize</span></span> |<span data-ttu-id="bd9cf-214">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="bd9cf-215">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="bd9cf-215">Integer (number of rows)</span></span> |<span data-ttu-id="bd9cf-216">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="bd9cf-216">No (default: 10000)</span></span> |
| <span data-ttu-id="bd9cf-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="bd9cf-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="bd9cf-218">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="bd9cf-219">자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="bd9cf-220">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-220">A query statement.</span></span> |<span data-ttu-id="bd9cf-221">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-221">No</span></span> |
| <span data-ttu-id="bd9cf-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="bd9cf-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="bd9cf-223">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="bd9cf-224">자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="bd9cf-225">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="bd9cf-226">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-226">No</span></span> |
| <span data-ttu-id="bd9cf-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="bd9cf-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="bd9cf-228">Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="bd9cf-229">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="bd9cf-230">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-230">No</span></span> |
| <span data-ttu-id="bd9cf-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="bd9cf-231">storedProcedureParameters</span></span> |<span data-ttu-id="bd9cf-232">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="bd9cf-233">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-233">Name/value pairs.</span></span> <span data-ttu-id="bd9cf-234">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="bd9cf-235">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-235">No</span></span> |
| <span data-ttu-id="bd9cf-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="bd9cf-236">sqlWriterTableType</span></span> |<span data-ttu-id="bd9cf-237">Hello 저장 프로시저에 사용 하는 테이블 형식 이름 toobe를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="bd9cf-238">복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="bd9cf-239">저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="bd9cf-240">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="bd9cf-240">A table type name.</span></span> |<span data-ttu-id="bd9cf-241">아니요</span><span class="sxs-lookup"><span data-stu-id="bd9cf-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="bd9cf-242">SqlSink 예제</span><span class="sxs-lookup"><span data-stu-id="bd9cf-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="bd9cf-243">SQL 데이터베이스에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="bd9cf-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="bd9cf-244">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bd9cf-245">표시 방법을 Azure SQL 데이터베이스 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="bd9cf-246">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="bd9cf-247">예: Azure SQL 데이터베이스 tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="bd9cf-248">hello 동일 정의 Data Factory 엔터티에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="bd9cf-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="bd9cf-249">[AzureSqlDatabase](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd9cf-250">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="bd9cf-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd9cf-251">[AzureSqlTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="bd9cf-252">[Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="bd9cf-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bd9cf-253">[SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bd9cf-254">hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터베이스 tooa blob의 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="bd9cf-255">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="bd9cf-256">**Azure SQL Database 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-256">**Azure SQL Database linked service:**</span></span>

```JSON
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
<span data-ttu-id="bd9cf-257">Hello 참조 [Azure SQL 연결 서비스](#linked-service) hello 목록에 대 한이 연결 된 서비스에서 지 원하는 속성의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="bd9cf-258">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bd9cf-259">Hello 참조 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 이 연결 된 서비스에서 지 원하는 속성의 hello 목록에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="bd9cf-260">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="bd9cf-261">hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="bd9cf-262">설정 "외부": "true" 알리고 hello Azure 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
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

<span data-ttu-id="bd9cf-263">Hello 참조 [Azure SQL 데이터 집합 형식 속성](#dataset) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="bd9cf-264">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bd9cf-265">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd9cf-266">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="bd9cf-267">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
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
<span data-ttu-id="bd9cf-268">Hello 참조 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="bd9cf-269">**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="bd9cf-270">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="bd9cf-271">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="bd9cf-272">hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
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
<span data-ttu-id="bd9cf-273">Hello 예에서 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="bd9cf-274">복사 활동 hello hello Azure SQL 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="bd9cf-275">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="bd9cf-276">Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello Azure SQL 데이터베이스에 대 한 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="bd9cf-277">예: `select column1, column2 from mytable`</span><span class="sxs-lookup"><span data-stu-id="bd9cf-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="bd9cf-278">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="bd9cf-279">Hello 참조 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello SqlSource에서 BlobSink로 지원 되는 속성 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="bd9cf-280">예: Azure Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="bd9cf-281">hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="bd9cf-282">[AzureSqlDatabase](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd9cf-283">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="bd9cf-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd9cf-284">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="bd9cf-285">[AzureSqlTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="bd9cf-286">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="bd9cf-287">hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터베이스에서 Azure blob tooa 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="bd9cf-288">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bd9cf-289">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-289">**Azure SQL linked service:**</span></span>

```JSON
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
<span data-ttu-id="bd9cf-290">Hello 참조 [Azure SQL 연결 서비스](#linked-service) hello 목록에 대 한이 연결 된 서비스에서 지 원하는 속성의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="bd9cf-291">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bd9cf-292">Hello 참조 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 이 연결 된 서비스에서 지 원하는 속성의 hello 목록에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="bd9cf-293">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="bd9cf-294">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd9cf-295">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="bd9cf-296">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="bd9cf-297">"external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="bd9cf-298">Hello 참조 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="bd9cf-299">**Azure SQL Database 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="bd9cf-300">hello 샘플 라는 이름의 "MyTable" Azure sql에서 데이터 tooa 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="bd9cf-301">Azure SQL로에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="bd9cf-302">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-302">New rows are added toohello table every hour.</span></span>

```JSON
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
<span data-ttu-id="bd9cf-303">Hello 참조 [Azure SQL 데이터 집합 형식 속성](#dataset) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="bd9cf-304">**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="bd9cf-305">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="bd9cf-306">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
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
            "type": "BlobSource",
            "blobColumnSeparators": ","
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
<span data-ttu-id="bd9cf-307">Hello 참조 [Sql 싱크](#sqlsink) 섹션 및 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello 목록이 SqlSink 및 BlobSource에서 지 원하는 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="bd9cf-308">Hello 대상 데이터베이스의 id 열</span><span class="sxs-lookup"><span data-stu-id="bd9cf-308">Identity columns in hello target database</span></span>
<span data-ttu-id="bd9cf-309">이 섹션에서는 id 열이 있는 id 열 tooa 대상 테이블 없이 원본 테이블에서 데이터를 복사 하기 위한 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="bd9cf-310">**원본 테이블:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="bd9cf-311">**대상 테이블:**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="bd9cf-312">해당 hello 대상 테이블에 id 열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="bd9cf-313">**원본 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="bd9cf-314">**대상 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="bd9cf-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="bd9cf-315">원본 테이블과 대상 테이블의 스키마가 서로 다릅니다(대상에 ID가 포함된 추가 열이 있음).</span><span class="sxs-lookup"><span data-stu-id="bd9cf-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="bd9cf-316">이 시나리오에서는 toospecify 필요 **구조** hello id 열이 포함 되지 않으면 hello 대상 데이터 집합 정의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="bd9cf-317">SQL 싱크에서 저장된 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="bd9cf-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="bd9cf-318">파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [복사 작업에서 SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="bd9cf-319">Azure SQL Database에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="bd9cf-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="bd9cf-320">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="bd9cf-321">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="bd9cf-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="bd9cf-322">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="bd9cf-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="bd9cf-323">Azure SQL 데이터베이스에서 데이터 tooand를 이동할 때는 hello 다음 매핑은 사용 하는 SQL 유형 too.NET 형식에서 그 반대의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="bd9cf-324">hello 매핑 hello ADO.NET에 대 한 SQL Server 데이터 형식 매핑과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="bd9cf-325">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="bd9cf-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="bd9cf-326">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="bd9cf-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="bd9cf-327">bigint</span><span class="sxs-lookup"><span data-stu-id="bd9cf-327">bigint</span></span> |<span data-ttu-id="bd9cf-328">Int64</span><span class="sxs-lookup"><span data-stu-id="bd9cf-328">Int64</span></span> |
| <span data-ttu-id="bd9cf-329">binary</span><span class="sxs-lookup"><span data-stu-id="bd9cf-329">binary</span></span> |<span data-ttu-id="bd9cf-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-330">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-331">bit</span><span class="sxs-lookup"><span data-stu-id="bd9cf-331">bit</span></span> |<span data-ttu-id="bd9cf-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="bd9cf-332">Boolean</span></span> |
| <span data-ttu-id="bd9cf-333">char</span><span class="sxs-lookup"><span data-stu-id="bd9cf-333">char</span></span> |<span data-ttu-id="bd9cf-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-334">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-335">date</span><span class="sxs-lookup"><span data-stu-id="bd9cf-335">date</span></span> |<span data-ttu-id="bd9cf-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-336">DateTime</span></span> |
| <span data-ttu-id="bd9cf-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-337">Datetime</span></span> |<span data-ttu-id="bd9cf-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-338">DateTime</span></span> |
| <span data-ttu-id="bd9cf-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="bd9cf-339">datetime2</span></span> |<span data-ttu-id="bd9cf-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-340">DateTime</span></span> |
| <span data-ttu-id="bd9cf-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bd9cf-341">Datetimeoffset</span></span> |<span data-ttu-id="bd9cf-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bd9cf-342">DateTimeOffset</span></span> |
| <span data-ttu-id="bd9cf-343">10진수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-343">Decimal</span></span> |<span data-ttu-id="bd9cf-344">10진수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-344">Decimal</span></span> |
| <span data-ttu-id="bd9cf-345">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="bd9cf-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="bd9cf-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-346">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-347">Float</span><span class="sxs-lookup"><span data-stu-id="bd9cf-347">Float</span></span> |<span data-ttu-id="bd9cf-348">Double</span><span class="sxs-lookup"><span data-stu-id="bd9cf-348">Double</span></span> |
| <span data-ttu-id="bd9cf-349">이미지</span><span class="sxs-lookup"><span data-stu-id="bd9cf-349">image</span></span> |<span data-ttu-id="bd9cf-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-350">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-351">int</span><span class="sxs-lookup"><span data-stu-id="bd9cf-351">int</span></span> |<span data-ttu-id="bd9cf-352">Int32</span><span class="sxs-lookup"><span data-stu-id="bd9cf-352">Int32</span></span> |
| <span data-ttu-id="bd9cf-353">money</span><span class="sxs-lookup"><span data-stu-id="bd9cf-353">money</span></span> |<span data-ttu-id="bd9cf-354">10진수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-354">Decimal</span></span> |
| <span data-ttu-id="bd9cf-355">nchar</span><span class="sxs-lookup"><span data-stu-id="bd9cf-355">nchar</span></span> |<span data-ttu-id="bd9cf-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-356">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-357">ntext</span><span class="sxs-lookup"><span data-stu-id="bd9cf-357">ntext</span></span> |<span data-ttu-id="bd9cf-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-358">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-359">numeric</span><span class="sxs-lookup"><span data-stu-id="bd9cf-359">numeric</span></span> |<span data-ttu-id="bd9cf-360">10진수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-360">Decimal</span></span> |
| <span data-ttu-id="bd9cf-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="bd9cf-361">nvarchar</span></span> |<span data-ttu-id="bd9cf-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-362">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-363">real</span><span class="sxs-lookup"><span data-stu-id="bd9cf-363">real</span></span> |<span data-ttu-id="bd9cf-364">단일</span><span class="sxs-lookup"><span data-stu-id="bd9cf-364">Single</span></span> |
| <span data-ttu-id="bd9cf-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="bd9cf-365">rowversion</span></span> |<span data-ttu-id="bd9cf-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-366">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-367">smalldatetime</span></span> |<span data-ttu-id="bd9cf-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd9cf-368">DateTime</span></span> |
| <span data-ttu-id="bd9cf-369">smallint</span><span class="sxs-lookup"><span data-stu-id="bd9cf-369">smallint</span></span> |<span data-ttu-id="bd9cf-370">Int16</span><span class="sxs-lookup"><span data-stu-id="bd9cf-370">Int16</span></span> |
| <span data-ttu-id="bd9cf-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="bd9cf-371">smallmoney</span></span> |<span data-ttu-id="bd9cf-372">10진수</span><span class="sxs-lookup"><span data-stu-id="bd9cf-372">Decimal</span></span> |
| <span data-ttu-id="bd9cf-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="bd9cf-373">sql_variant</span></span> |<span data-ttu-id="bd9cf-374">개체 *</span><span class="sxs-lookup"><span data-stu-id="bd9cf-374">Object *</span></span> |
| <span data-ttu-id="bd9cf-375">텍스트</span><span class="sxs-lookup"><span data-stu-id="bd9cf-375">text</span></span> |<span data-ttu-id="bd9cf-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-376">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-377">실시간</span><span class="sxs-lookup"><span data-stu-id="bd9cf-377">time</span></span> |<span data-ttu-id="bd9cf-378">timespan</span><span class="sxs-lookup"><span data-stu-id="bd9cf-378">TimeSpan</span></span> |
| <span data-ttu-id="bd9cf-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="bd9cf-379">timestamp</span></span> |<span data-ttu-id="bd9cf-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-380">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="bd9cf-381">tinyint</span></span> |<span data-ttu-id="bd9cf-382">Byte</span><span class="sxs-lookup"><span data-stu-id="bd9cf-382">Byte</span></span> |
| <span data-ttu-id="bd9cf-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="bd9cf-383">uniqueidentifier</span></span> |<span data-ttu-id="bd9cf-384">Guid</span><span class="sxs-lookup"><span data-stu-id="bd9cf-384">Guid</span></span> |
| <span data-ttu-id="bd9cf-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="bd9cf-385">varbinary</span></span> |<span data-ttu-id="bd9cf-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-386">Byte[]</span></span> |
| <span data-ttu-id="bd9cf-387">varchar</span><span class="sxs-lookup"><span data-stu-id="bd9cf-387">varchar</span></span> |<span data-ttu-id="bd9cf-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="bd9cf-388">String, Char[]</span></span> |
| <span data-ttu-id="bd9cf-389">xml</span><span class="sxs-lookup"><span data-stu-id="bd9cf-389">xml</span></span> |<span data-ttu-id="bd9cf-390">xml</span><span class="sxs-lookup"><span data-stu-id="bd9cf-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="bd9cf-391">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="bd9cf-391">Map source toosink columns</span></span>
<span data-ttu-id="bd9cf-392">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="bd9cf-393">반복 가능한 복사</span><span class="sxs-lookup"><span data-stu-id="bd9cf-393">Repeatable copy</span></span>
<span data-ttu-id="bd9cf-394">데이터 tooSQL 서버 데이터베이스를 복사할 때 hello 복사 활동 기본적으로 데이터 toohello 싱크 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="bd9cf-395">UPSERT tooperform 대신 참조 [반복 쓰기 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="bd9cf-396">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="bd9cf-397">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="bd9cf-398">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="bd9cf-399">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="bd9cf-400">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bd9cf-401">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="bd9cf-401">Performance and Tuning</span></span>
<span data-ttu-id="bd9cf-402">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd9cf-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
