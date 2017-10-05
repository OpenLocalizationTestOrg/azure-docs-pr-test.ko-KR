---
title: "Azure SQL Database 간 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Azure SQL Database 간에 데이터를 복사하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="47134-103">Azure Data Factory를 사용하여 Azure SQL Database 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="47134-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="47134-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure SQL Database 간에 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="47134-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="47134-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="47134-106">Supported scenarios</span></span>
<span data-ttu-id="47134-107">**Azure SQL Database**에서 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="47134-108">다음 데이터 저장소에서 **Azure SQL Database**로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="47134-109">지원되는 인증 유형</span><span class="sxs-lookup"><span data-stu-id="47134-109">Supported authentication type</span></span>
<span data-ttu-id="47134-110">Azure SQL Database 커넥터는 기본 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="47134-111">시작</span><span class="sxs-lookup"><span data-stu-id="47134-111">Getting started</span></span>
<span data-ttu-id="47134-112">다른 도구/API를 사용하여 Azure SQL Database 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="47134-113">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="47134-114">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="47134-115">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="47134-116">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="47134-117">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="47134-118">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-118">Create a **data factory**.</span></span> <span data-ttu-id="47134-119">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="47134-120">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="47134-121">예를 들어 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 경우 Azure Storage 계정 및 Azure SQL Database를 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="47134-122">Azure SQL Database와 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="47134-123">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="47134-124">마지막 단계에서 설명한 예제에서는 입력 데이터가 포함된 BLOB 컨테이너 및 폴더를 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="47134-125">그리고 Blob Storage에서 복사한 데이터를 포함하는 Azure SQL Database의 SQL 테이블을 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="47134-126">Azure Data Lake Store와 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="47134-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="47134-128">앞에서 언급한 예에서는 BlobSource를 원본으로, SqlSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="47134-129">마찬가지로, Azure SQL Database에서 Azure Blob Storage로 복사하는 경우 복사 작업에 SqlSource 및 BlobSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="47134-130">Azure SQL Database와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="47134-131">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="47134-132">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="47134-133">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="47134-134">다른 곳에서 Azure SQL Database로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-sql-database) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="47134-135">다음 섹션에서는 Azure SQL Database에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="47134-136">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="47134-136">Linked service properties</span></span>
<span data-ttu-id="47134-137">Azure SQL Database를 데이터 팩터리에 연결하는 Azure SQL 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="47134-138">다음 테이블은 Azure SQL 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="47134-139">속성</span><span class="sxs-lookup"><span data-stu-id="47134-139">Property</span></span> | <span data-ttu-id="47134-140">설명</span><span class="sxs-lookup"><span data-stu-id="47134-140">Description</span></span> | <span data-ttu-id="47134-141">필수</span><span class="sxs-lookup"><span data-stu-id="47134-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47134-142">type</span><span class="sxs-lookup"><span data-stu-id="47134-142">type</span></span> |<span data-ttu-id="47134-143">형식 속성은 **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="47134-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="47134-144">예</span><span class="sxs-lookup"><span data-stu-id="47134-144">Yes</span></span> |
| <span data-ttu-id="47134-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="47134-145">connectionString</span></span> |<span data-ttu-id="47134-146">connectionString 속성에 대한 Azure SQL 데이터베이스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="47134-147">기본 인증만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="47134-148">예</span><span class="sxs-lookup"><span data-stu-id="47134-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="47134-149">데이터베이스 서버인 [Azure SQL Database 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)을 구성하여 [Azure 서비스가 서버에 액세스할 수 있도록](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="47134-150">또한 데이터 팩터리 게이트웨이를 사용하여 온-프레미스 데이터 원본을 포함한 Azure 외부에서 Azure SQL 데이터베이스로 데이터를 복사하는 경우 데이터를 Azure SQL Database로 보내는 컴퓨터에 대한 적절한 IP 주소 범위를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="47134-151">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="47134-151">Dataset properties</span></span>
<span data-ttu-id="47134-152">Azure SQL Database에서 입력 또는 출력 데이터를 표시할 데이터 집합을 지정하려면 데이터 집합의 형식 속성을 **AzureSqlTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="47134-153">데이터 집합의 **linkedServiceName** 속성을 Azure SQL 연결된 서비스의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="47134-154">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="47134-155">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="47134-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="47134-156">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="47134-157">**AzureSqlTable** 데이터 집합 형식의 데이터 집합에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="47134-158">속성</span><span class="sxs-lookup"><span data-stu-id="47134-158">Property</span></span> | <span data-ttu-id="47134-159">설명</span><span class="sxs-lookup"><span data-stu-id="47134-159">Description</span></span> | <span data-ttu-id="47134-160">필수</span><span class="sxs-lookup"><span data-stu-id="47134-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47134-161">tableName</span><span class="sxs-lookup"><span data-stu-id="47134-161">tableName</span></span> |<span data-ttu-id="47134-162">연결된 서비스가 참조하는 Azure SQL 데이터베이스 인스턴스에서 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="47134-163">예</span><span class="sxs-lookup"><span data-stu-id="47134-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="47134-164">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="47134-164">Copy activity properties</span></span>
<span data-ttu-id="47134-165">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="47134-166">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="47134-167">복사 작업은 하나의 입력을 가지고 하나의 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="47134-168">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="47134-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="47134-169">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="47134-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="47134-170">Azure SQL Database에서 데이터를 이동하는 경우 복사 작업의 원본 유형을 **SqlSource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="47134-171">마찬가지로 Azure SQL Database로 데이터를 이동하는 경우 복사 작업의 싱크 유형을 **SqlSink**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="47134-172">이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="47134-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="47134-173">SqlSource</span></span>
<span data-ttu-id="47134-174">원본이 **SqlSource** 형식인 복사 작업의 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="47134-175">속성</span><span class="sxs-lookup"><span data-stu-id="47134-175">Property</span></span> | <span data-ttu-id="47134-176">설명</span><span class="sxs-lookup"><span data-stu-id="47134-176">Description</span></span> | <span data-ttu-id="47134-177">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="47134-177">Allowed values</span></span> | <span data-ttu-id="47134-178">필수</span><span class="sxs-lookup"><span data-stu-id="47134-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47134-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="47134-179">sqlReaderQuery</span></span> |<span data-ttu-id="47134-180">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-180">Use the custom query to read data.</span></span> |<span data-ttu-id="47134-181">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="47134-181">SQL query string.</span></span> <span data-ttu-id="47134-182">예: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="47134-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="47134-183">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-183">No</span></span> |
| <span data-ttu-id="47134-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="47134-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="47134-185">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="47134-186">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-186">Name of the stored procedure.</span></span> <span data-ttu-id="47134-187">마지막 SQL 문은 저장 프로시저의 SELECT 문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="47134-188">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-188">No</span></span> |
| <span data-ttu-id="47134-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="47134-189">storedProcedureParameters</span></span> |<span data-ttu-id="47134-190">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="47134-191">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-191">Name/value pairs.</span></span> <span data-ttu-id="47134-192">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="47134-193">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-193">No</span></span> |

<span data-ttu-id="47134-194">**sqlReaderQuery** 이 SqlSource에 지정되면 복사 작업은 데이터를 가져오는 Azure SQL 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="47134-195">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="47134-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="47134-196">sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정하지 않으면 JSON 데이터 집합의 구조 섹션에 정의된 열은 (`select column1, column2 from mytable`) 쿼리를 작성하는 데 사용되어 Azure SQL Database에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="47134-197">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="47134-198">**sqlReaderStoredProcedureName**을 사용하는 경우에도 데이터 집합 JSON에서 **tableName** 속성 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="47134-199">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="47134-200">SqlSource 예제</span><span class="sxs-lookup"><span data-stu-id="47134-200">SqlSource example</span></span>

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

<span data-ttu-id="47134-201">**저장 프로시저 정의:**</span><span class="sxs-lookup"><span data-stu-id="47134-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="47134-202">파이프라인</span><span class="sxs-lookup"><span data-stu-id="47134-202">SqlSink</span></span>
<span data-ttu-id="47134-203">**SqlSink** 는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="47134-204">속성</span><span class="sxs-lookup"><span data-stu-id="47134-204">Property</span></span> | <span data-ttu-id="47134-205">설명</span><span class="sxs-lookup"><span data-stu-id="47134-205">Description</span></span> | <span data-ttu-id="47134-206">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="47134-206">Allowed values</span></span> | <span data-ttu-id="47134-207">필수</span><span class="sxs-lookup"><span data-stu-id="47134-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47134-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="47134-208">writeBatchTimeout</span></span> |<span data-ttu-id="47134-209">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="47134-210">timespan</span><span class="sxs-lookup"><span data-stu-id="47134-210">timespan</span></span><br/><br/> <span data-ttu-id="47134-211">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="47134-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="47134-212">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-212">No</span></span> |
| <span data-ttu-id="47134-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="47134-213">writeBatchSize</span></span> |<span data-ttu-id="47134-214">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="47134-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="47134-215">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="47134-215">Integer (number of rows)</span></span> |<span data-ttu-id="47134-216">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="47134-216">No (default: 10000)</span></span> |
| <span data-ttu-id="47134-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="47134-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="47134-218">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="47134-219">자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="47134-220">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-220">A query statement.</span></span> |<span data-ttu-id="47134-221">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-221">No</span></span> |
| <span data-ttu-id="47134-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="47134-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="47134-223">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="47134-224">자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="47134-225">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="47134-226">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-226">No</span></span> |
| <span data-ttu-id="47134-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="47134-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="47134-228">대상 테이블에 대한 데이터 Upsert(업데이트/삽입)를 수행하는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="47134-229">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-229">Name of the stored procedure.</span></span> |<span data-ttu-id="47134-230">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-230">No</span></span> |
| <span data-ttu-id="47134-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="47134-231">storedProcedureParameters</span></span> |<span data-ttu-id="47134-232">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="47134-233">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-233">Name/value pairs.</span></span> <span data-ttu-id="47134-234">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="47134-235">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-235">No</span></span> |
| <span data-ttu-id="47134-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="47134-236">sqlWriterTableType</span></span> |<span data-ttu-id="47134-237">저장 프로시저에 사용할 테이블 형식 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="47134-238">복사 작업을 사용하면 이 테이블 형식으로 임시 테이블에서 사용할 수 있는 데이터를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="47134-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="47134-239">그러면 저장 프로시저 코드가 복사되는 데이터를 기존 데이터와 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="47134-240">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="47134-240">A table type name.</span></span> |<span data-ttu-id="47134-241">아니요</span><span class="sxs-lookup"><span data-stu-id="47134-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="47134-242">SqlSink 예제</span><span class="sxs-lookup"><span data-stu-id="47134-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="47134-243">SQL Database로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="47134-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="47134-244">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="47134-245">Azure Blob 저장소 및 Azure SQL 데이터베이스 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47134-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="47134-246">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="47134-247">예제: Azure SQL Database에서 Azure Blob에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="47134-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="47134-248">샘플이 다음 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="47134-249">[AzureSqlDatabase](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="47134-250">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="47134-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="47134-251">[AzureSqlTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="47134-252">[Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="47134-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="47134-253">[SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="47134-254">샘플은 Azure SQL database의 테이블에서 Blob으로 (매시간, 매일 등) 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="47134-255">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="47134-256">**Azure SQL Database 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="47134-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="47134-257">연결된 서비스에서 지원하는 속성의 목록은 [Azure SQL 연결된 서비스](#linked-service) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="47134-258">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="47134-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="47134-259">연결된 서비스에서 지원하는 속성의 목록은 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="47134-260">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="47134-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="47134-261">샘플은 Azure SQL에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn" 라는 열이 포함되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="47134-262">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Azure Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="47134-263">데이터 집합 형식에서 지원하는 속성의 목록은 [Azure SQL 데이터 집합 형식 속성](#dataset) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="47134-264">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="47134-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="47134-265">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="47134-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="47134-266">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="47134-267">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="47134-268">데이터 집합 형식에서 지원하는 속성의 목록은 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="47134-269">**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="47134-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="47134-270">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="47134-271">파이프라인 JSON 정의에서 **source** 형식은 **SqlSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="47134-272">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="47134-273">위의 예에서는 SqlSource에 대해 **sqlReaderQuery** 가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="47134-274">복사 작업은 데이터를 가져오는 Azure SQL 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="47134-275">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="47134-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="47134-276">sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정하지 않으면 JSON 데이터 집합의 구조 섹션에 정의된 열은 쿼리를 작성하는 데 사용되어 Azure SQL Database에 대해 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="47134-277">예: `select column1, column2 from mytable`</span><span class="sxs-lookup"><span data-stu-id="47134-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="47134-278">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="47134-279">SqlSource 및 BlobSink에서 지원하는 속성 목록은 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="47134-280">예제: Azure Blob에서 Azure SQL Database로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="47134-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="47134-281">샘플이 다음 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="47134-282">[AzureSqlDatabase](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="47134-283">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="47134-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="47134-284">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="47134-285">[AzureSqlTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="47134-286">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="47134-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="47134-287">샘플은 Azure blob에서 Azure SQL database의 테이블로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="47134-288">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="47134-289">**Azure SQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="47134-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="47134-290">연결된 서비스에서 지원하는 속성의 목록은 [Azure SQL 연결된 서비스](#linked-service) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="47134-291">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="47134-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="47134-292">연결된 서비스에서 지원하는 속성의 목록은 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="47134-293">**Azure Blob 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="47134-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="47134-294">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="47134-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="47134-295">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="47134-296">폴더 경로는 연도, 월 및 일 일부 시작 시간을 사용하고 파일 이름은 시작 시간의 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="47134-297">"external": "true" 설정은 데이터 팩터리 서비스에 이 테이블이 데이터 팩터리의 외부에 있으며 데이터 팩터리의 작업에 의해 생성되지 않는다는 점을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="47134-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="47134-298">데이터 집합 형식에서 지원하는 속성의 목록은 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="47134-299">**Azure SQL Database 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="47134-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="47134-300">샘플은 Azure SQL의 "MyTable"이라는 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="47134-301">Blob CSV 파일을 포함하려 하면 같은 수의 열을 사용하여 Azure SQL의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47134-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="47134-302">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-302">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="47134-303">데이터 집합 형식에서 지원하는 속성의 목록은 [Azure SQL 데이터 집합 형식 속성](#dataset) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="47134-304">**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="47134-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="47134-305">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="47134-306">파이프라인 JSON 정의에서 **원본** 형식은 **BlobSource**로 설정되고 **싱크** 형식은 **SqlSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="47134-307">SqlSink 및 BlobSource에서 지원하는 속성 목록은 [Sql 싱크](#sqlsink) 섹션 및 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="47134-308">대상 데이터베이스의 ID 열</span><span class="sxs-lookup"><span data-stu-id="47134-308">Identity columns in the target database</span></span>
<span data-ttu-id="47134-309">이 섹션에서는 ID 열이 없는 원본 테이블에서 ID 열이 있는 대상 테이블로 데이터를 복사하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="47134-310">**원본 테이블:**</span><span class="sxs-lookup"><span data-stu-id="47134-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="47134-311">**대상 테이블:**</span><span class="sxs-lookup"><span data-stu-id="47134-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="47134-312">대상 테이블에 ID 열이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="47134-313">**원본 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="47134-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="47134-314">**대상 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="47134-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="47134-315">원본 테이블과 대상 테이블의 스키마가 서로 다릅니다(대상에 ID가 포함된 추가 열이 있음).</span><span class="sxs-lookup"><span data-stu-id="47134-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="47134-316">이 시나리오에서는 ID 열을 포함하지 않는 대상 데이터 집합 정의에서 **structure** 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="47134-317">SQL 싱크에서 저장된 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="47134-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="47134-318">파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [복사 작업에서 SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="47134-319">Azure SQL Database에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="47134-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="47134-320">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="47134-321">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="47134-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="47134-322">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="47134-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="47134-323">Azure SQL Database 간에 데이터를 이동할 때는 다음과 같은 매핑이 SQL 형식에서 .NET 형식으로 또는 그 반대로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47134-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="47134-324">매핑은 ADO.NET에 대한 SQL Server 데이터 형식 매핑과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="47134-325">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="47134-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="47134-326">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="47134-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="47134-327">bigint</span><span class="sxs-lookup"><span data-stu-id="47134-327">bigint</span></span> |<span data-ttu-id="47134-328">Int64</span><span class="sxs-lookup"><span data-stu-id="47134-328">Int64</span></span> |
| <span data-ttu-id="47134-329">binary</span><span class="sxs-lookup"><span data-stu-id="47134-329">binary</span></span> |<span data-ttu-id="47134-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-330">Byte[]</span></span> |
| <span data-ttu-id="47134-331">bit</span><span class="sxs-lookup"><span data-stu-id="47134-331">bit</span></span> |<span data-ttu-id="47134-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="47134-332">Boolean</span></span> |
| <span data-ttu-id="47134-333">char</span><span class="sxs-lookup"><span data-stu-id="47134-333">char</span></span> |<span data-ttu-id="47134-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-334">String, Char[]</span></span> |
| <span data-ttu-id="47134-335">date</span><span class="sxs-lookup"><span data-stu-id="47134-335">date</span></span> |<span data-ttu-id="47134-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="47134-336">DateTime</span></span> |
| <span data-ttu-id="47134-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="47134-337">Datetime</span></span> |<span data-ttu-id="47134-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="47134-338">DateTime</span></span> |
| <span data-ttu-id="47134-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="47134-339">datetime2</span></span> |<span data-ttu-id="47134-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="47134-340">DateTime</span></span> |
| <span data-ttu-id="47134-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47134-341">Datetimeoffset</span></span> |<span data-ttu-id="47134-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47134-342">DateTimeOffset</span></span> |
| <span data-ttu-id="47134-343">10진수</span><span class="sxs-lookup"><span data-stu-id="47134-343">Decimal</span></span> |<span data-ttu-id="47134-344">10진수</span><span class="sxs-lookup"><span data-stu-id="47134-344">Decimal</span></span> |
| <span data-ttu-id="47134-345">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="47134-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="47134-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-346">Byte[]</span></span> |
| <span data-ttu-id="47134-347">Float</span><span class="sxs-lookup"><span data-stu-id="47134-347">Float</span></span> |<span data-ttu-id="47134-348">Double</span><span class="sxs-lookup"><span data-stu-id="47134-348">Double</span></span> |
| <span data-ttu-id="47134-349">이미지</span><span class="sxs-lookup"><span data-stu-id="47134-349">image</span></span> |<span data-ttu-id="47134-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-350">Byte[]</span></span> |
| <span data-ttu-id="47134-351">int</span><span class="sxs-lookup"><span data-stu-id="47134-351">int</span></span> |<span data-ttu-id="47134-352">Int32</span><span class="sxs-lookup"><span data-stu-id="47134-352">Int32</span></span> |
| <span data-ttu-id="47134-353">money</span><span class="sxs-lookup"><span data-stu-id="47134-353">money</span></span> |<span data-ttu-id="47134-354">10진수</span><span class="sxs-lookup"><span data-stu-id="47134-354">Decimal</span></span> |
| <span data-ttu-id="47134-355">nchar</span><span class="sxs-lookup"><span data-stu-id="47134-355">nchar</span></span> |<span data-ttu-id="47134-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-356">String, Char[]</span></span> |
| <span data-ttu-id="47134-357">ntext</span><span class="sxs-lookup"><span data-stu-id="47134-357">ntext</span></span> |<span data-ttu-id="47134-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-358">String, Char[]</span></span> |
| <span data-ttu-id="47134-359">numeric</span><span class="sxs-lookup"><span data-stu-id="47134-359">numeric</span></span> |<span data-ttu-id="47134-360">10진수</span><span class="sxs-lookup"><span data-stu-id="47134-360">Decimal</span></span> |
| <span data-ttu-id="47134-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="47134-361">nvarchar</span></span> |<span data-ttu-id="47134-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-362">String, Char[]</span></span> |
| <span data-ttu-id="47134-363">real</span><span class="sxs-lookup"><span data-stu-id="47134-363">real</span></span> |<span data-ttu-id="47134-364">단일</span><span class="sxs-lookup"><span data-stu-id="47134-364">Single</span></span> |
| <span data-ttu-id="47134-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="47134-365">rowversion</span></span> |<span data-ttu-id="47134-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-366">Byte[]</span></span> |
| <span data-ttu-id="47134-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="47134-367">smalldatetime</span></span> |<span data-ttu-id="47134-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="47134-368">DateTime</span></span> |
| <span data-ttu-id="47134-369">smallint</span><span class="sxs-lookup"><span data-stu-id="47134-369">smallint</span></span> |<span data-ttu-id="47134-370">Int16</span><span class="sxs-lookup"><span data-stu-id="47134-370">Int16</span></span> |
| <span data-ttu-id="47134-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="47134-371">smallmoney</span></span> |<span data-ttu-id="47134-372">10진수</span><span class="sxs-lookup"><span data-stu-id="47134-372">Decimal</span></span> |
| <span data-ttu-id="47134-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="47134-373">sql_variant</span></span> |<span data-ttu-id="47134-374">개체 *</span><span class="sxs-lookup"><span data-stu-id="47134-374">Object *</span></span> |
| <span data-ttu-id="47134-375">텍스트</span><span class="sxs-lookup"><span data-stu-id="47134-375">text</span></span> |<span data-ttu-id="47134-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-376">String, Char[]</span></span> |
| <span data-ttu-id="47134-377">실시간</span><span class="sxs-lookup"><span data-stu-id="47134-377">time</span></span> |<span data-ttu-id="47134-378">timespan</span><span class="sxs-lookup"><span data-stu-id="47134-378">TimeSpan</span></span> |
| <span data-ttu-id="47134-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="47134-379">timestamp</span></span> |<span data-ttu-id="47134-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-380">Byte[]</span></span> |
| <span data-ttu-id="47134-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="47134-381">tinyint</span></span> |<span data-ttu-id="47134-382">Byte</span><span class="sxs-lookup"><span data-stu-id="47134-382">Byte</span></span> |
| <span data-ttu-id="47134-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="47134-383">uniqueidentifier</span></span> |<span data-ttu-id="47134-384">Guid</span><span class="sxs-lookup"><span data-stu-id="47134-384">Guid</span></span> |
| <span data-ttu-id="47134-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="47134-385">varbinary</span></span> |<span data-ttu-id="47134-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47134-386">Byte[]</span></span> |
| <span data-ttu-id="47134-387">varchar</span><span class="sxs-lookup"><span data-stu-id="47134-387">varchar</span></span> |<span data-ttu-id="47134-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47134-388">String, Char[]</span></span> |
| <span data-ttu-id="47134-389">xml</span><span class="sxs-lookup"><span data-stu-id="47134-389">xml</span></span> |<span data-ttu-id="47134-390">xml</span><span class="sxs-lookup"><span data-stu-id="47134-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="47134-391">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="47134-391">Map source to sink columns</span></span>
<span data-ttu-id="47134-392">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="47134-393">반복 가능한 복사</span><span class="sxs-lookup"><span data-stu-id="47134-393">Repeatable copy</span></span>
<span data-ttu-id="47134-394">SQL Server 데이터베이스로 데이터를 복사할 때 복사 작업은 기본적으로 싱크 테이블에 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="47134-395">그 대신 UPSERT를 수행하려면 [SqlSink에 반복 가능한 쓰기](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="47134-396">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="47134-397">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="47134-398">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47134-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="47134-399">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47134-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="47134-400">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="47134-401">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="47134-401">Performance and Tuning</span></span>
<span data-ttu-id="47134-402">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47134-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
