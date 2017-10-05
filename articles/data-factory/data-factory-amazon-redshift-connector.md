---
title: "Data Factory를 사용하여 Amazon Redshift에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 Amazon Redshift에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="31892-103">Azure 데이터 팩터리를 사용하여 Amazon Redshift에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="31892-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="31892-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Amazon Redshift에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="31892-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="31892-106">Amazon Redshift에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="31892-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="31892-108">현재 데이터 팩터리는 Amazon Redshift에서 다른 데이터 저장소로의 데이터 이동을 지원하지만, 다른 데이터 저장소에서 Amazon Redshift로 데이터 이동은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31892-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31892-109">Prerequisites</span></span>
* <span data-ttu-id="31892-110">온-프레미스 데이터 저장소로 데이터를 이동하는 경우 온-프레미스 컴퓨터에 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="31892-111">그런 다음 데이터 관리 게이트웨이(컴퓨터의 IP 주소 사용)에 Amazon Redshift 클러스터에 대한 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="31892-112">자세한 내용은 [클러스터에 대한 액세스 권한 부여](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="31892-113">Azure 데이터 저장소에 데이터를 이동하는 경우, Azure 데이터 센터에서 사용하는 IP 주소 및 SQL 범위를 계산하기 위해 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="31892-114">시작</span><span class="sxs-lookup"><span data-stu-id="31892-114">Getting started</span></span>
<span data-ttu-id="31892-115">다른 도구/API를 사용하여 Amazon Redshift 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="31892-116">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="31892-117">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="31892-118">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="31892-119">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="31892-120">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="31892-121">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31892-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="31892-122">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31892-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="31892-123">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31892-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="31892-124">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="31892-125">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="31892-126">Amazon Redshift 데이터 저장소의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: Amazon Redshift에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-amazon-redshift-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="31892-127">다음 섹션에서는 Amazon Redshift에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="31892-128">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="31892-128">Linked service properties</span></span>
<span data-ttu-id="31892-129">다음 테이블은 Amazon Redshift 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="31892-130">속성</span><span class="sxs-lookup"><span data-stu-id="31892-130">Property</span></span> | <span data-ttu-id="31892-131">설명</span><span class="sxs-lookup"><span data-stu-id="31892-131">Description</span></span> | <span data-ttu-id="31892-132">필수</span><span class="sxs-lookup"><span data-stu-id="31892-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31892-133">type</span><span class="sxs-lookup"><span data-stu-id="31892-133">type</span></span> |<span data-ttu-id="31892-134">형식 속성은 **AmazonRedshift**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="31892-135">예</span><span class="sxs-lookup"><span data-stu-id="31892-135">Yes</span></span> |
| <span data-ttu-id="31892-136">server</span><span class="sxs-lookup"><span data-stu-id="31892-136">server</span></span> |<span data-ttu-id="31892-137">Amazon Redshift 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="31892-138">예</span><span class="sxs-lookup"><span data-stu-id="31892-138">Yes</span></span> |
| <span data-ttu-id="31892-139">포트</span><span class="sxs-lookup"><span data-stu-id="31892-139">port</span></span> |<span data-ttu-id="31892-140">Amazon Redshift 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="31892-141">기본값이 없음: 5439</span><span class="sxs-lookup"><span data-stu-id="31892-141">No, default value: 5439</span></span> |
| <span data-ttu-id="31892-142">database</span><span class="sxs-lookup"><span data-stu-id="31892-142">database</span></span> |<span data-ttu-id="31892-143">Amazon Redshift 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="31892-144">예</span><span class="sxs-lookup"><span data-stu-id="31892-144">Yes</span></span> |
| <span data-ttu-id="31892-145">username</span><span class="sxs-lookup"><span data-stu-id="31892-145">username</span></span> |<span data-ttu-id="31892-146">데이터베이스에 대한 액세스 권한이 있는 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="31892-147">예</span><span class="sxs-lookup"><span data-stu-id="31892-147">Yes</span></span> |
| <span data-ttu-id="31892-148">password</span><span class="sxs-lookup"><span data-stu-id="31892-148">password</span></span> |<span data-ttu-id="31892-149">사용자 계정의 password입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-149">Password for the user account.</span></span> |<span data-ttu-id="31892-150">예</span><span class="sxs-lookup"><span data-stu-id="31892-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="31892-151">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="31892-151">Dataset properties</span></span>
<span data-ttu-id="31892-152">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="31892-153">구조, 가용성 및 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="31892-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="31892-154">**typeProperties** 섹션은 데이터 집합의 각 형식마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="31892-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="31892-155">데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="31892-156">**RelationalTable** 형식(Amazon Redshift 데이터 집합을 포함)의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="31892-157">속성</span><span class="sxs-lookup"><span data-stu-id="31892-157">Property</span></span> | <span data-ttu-id="31892-158">설명</span><span class="sxs-lookup"><span data-stu-id="31892-158">Description</span></span> | <span data-ttu-id="31892-159">필수</span><span class="sxs-lookup"><span data-stu-id="31892-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31892-160">tableName</span><span class="sxs-lookup"><span data-stu-id="31892-160">tableName</span></span> |<span data-ttu-id="31892-161">연결된 서비스가 참조하는 Amazon Redshift 데이터베이스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="31892-162">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="31892-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="31892-163">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="31892-163">Copy activity properties</span></span>
<span data-ttu-id="31892-164">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="31892-165">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="31892-166">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="31892-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="31892-167">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="31892-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="31892-168">복사 작업의 원본이 **RelationalSource** 형식인 경우(Amazon Redshift 포함) typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="31892-169">속성</span><span class="sxs-lookup"><span data-stu-id="31892-169">Property</span></span> | <span data-ttu-id="31892-170">설명</span><span class="sxs-lookup"><span data-stu-id="31892-170">Description</span></span> | <span data-ttu-id="31892-171">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="31892-171">Allowed values</span></span> | <span data-ttu-id="31892-172">필수</span><span class="sxs-lookup"><span data-stu-id="31892-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31892-173">쿼리</span><span class="sxs-lookup"><span data-stu-id="31892-173">query</span></span> |<span data-ttu-id="31892-174">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-174">Use the custom query to read data.</span></span> |<span data-ttu-id="31892-175">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="31892-175">SQL query string.</span></span> <span data-ttu-id="31892-176">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="31892-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="31892-177">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="31892-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="31892-178">JSON 예제: Amazon Redshift에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="31892-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="31892-179">이 샘플은 Amazon Redshift 데이터베이스에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="31892-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="31892-180">그러나 Azure Data Factory의 복사 작업을 사용하여 **여기** 에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="31892-181">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="31892-182">[AmazonRedshift](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="31892-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="31892-183">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="31892-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="31892-184">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="31892-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="31892-185">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="31892-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="31892-186">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="31892-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="31892-187">샘플은 Amazon Redshift의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="31892-188">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="31892-189">**Amazon Redshift 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="31892-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="31892-190">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="31892-190">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="31892-191">**Amazon Redshift 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="31892-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="31892-192">`"external": true` 설정을 사용하는 경우 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="31892-193">파이프라인에서의 작업에 의해 생성되지 않은 입력 데이터 집합에서 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="31892-194">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="31892-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="31892-195">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="31892-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="31892-196">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="31892-197">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="31892-198">**Azure Redshift 원본(RelationalSource) 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="31892-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="31892-199">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="31892-200">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="31892-201">**query** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="31892-202">Amazon Redshift에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="31892-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="31892-203">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="31892-204">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="31892-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="31892-205">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="31892-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="31892-206">Amazon Redshift에 데이터를 이동하는 경우 Amazon Redshift 형식에서 .NET 형식으로 이동에 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="31892-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="31892-207">Amazon Redshift 형식</span><span class="sxs-lookup"><span data-stu-id="31892-207">Amazon Redshift Type</span></span> | <span data-ttu-id="31892-208">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="31892-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="31892-209">SmallInt</span><span class="sxs-lookup"><span data-stu-id="31892-209">SMALLINT</span></span> |<span data-ttu-id="31892-210">Int16</span><span class="sxs-lookup"><span data-stu-id="31892-210">Int16</span></span> |
| <span data-ttu-id="31892-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="31892-211">INTEGER</span></span> |<span data-ttu-id="31892-212">Int32</span><span class="sxs-lookup"><span data-stu-id="31892-212">Int32</span></span> |
| <span data-ttu-id="31892-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="31892-213">BIGINT</span></span> |<span data-ttu-id="31892-214">Int64</span><span class="sxs-lookup"><span data-stu-id="31892-214">Int64</span></span> |
| <span data-ttu-id="31892-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="31892-215">DECIMAL</span></span> |<span data-ttu-id="31892-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="31892-216">Decimal</span></span> |
| <span data-ttu-id="31892-217">Real</span><span class="sxs-lookup"><span data-stu-id="31892-217">REAL</span></span> |<span data-ttu-id="31892-218">단일</span><span class="sxs-lookup"><span data-stu-id="31892-218">Single</span></span> |
| <span data-ttu-id="31892-219">double precision</span><span class="sxs-lookup"><span data-stu-id="31892-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="31892-220">Double</span><span class="sxs-lookup"><span data-stu-id="31892-220">Double</span></span> |
| <span data-ttu-id="31892-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="31892-221">BOOLEAN</span></span> |<span data-ttu-id="31892-222">문자열</span><span class="sxs-lookup"><span data-stu-id="31892-222">String</span></span> |
| <span data-ttu-id="31892-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="31892-223">CHAR</span></span> |<span data-ttu-id="31892-224">문자열</span><span class="sxs-lookup"><span data-stu-id="31892-224">String</span></span> |
| <span data-ttu-id="31892-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="31892-225">VARCHAR</span></span> |<span data-ttu-id="31892-226">문자열</span><span class="sxs-lookup"><span data-stu-id="31892-226">String</span></span> |
| <span data-ttu-id="31892-227">DATE</span><span class="sxs-lookup"><span data-stu-id="31892-227">DATE</span></span> |<span data-ttu-id="31892-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="31892-228">DateTime</span></span> |
| <span data-ttu-id="31892-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="31892-229">TIMESTAMP</span></span> |<span data-ttu-id="31892-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="31892-230">DateTime</span></span> |
| <span data-ttu-id="31892-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="31892-231">TEXT</span></span> |<span data-ttu-id="31892-232">String</span><span class="sxs-lookup"><span data-stu-id="31892-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="31892-233">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="31892-233">Map source to sink columns</span></span>
<span data-ttu-id="31892-234">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="31892-235">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="31892-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="31892-236">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="31892-237">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="31892-238">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31892-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="31892-239">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31892-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="31892-240">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="31892-241">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="31892-241">Performance and Tuning</span></span>
<span data-ttu-id="31892-242">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31892-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31892-243">Next Steps</span></span>
<span data-ttu-id="31892-244">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31892-244">See the following articles:</span></span>

* <span data-ttu-id="31892-245">[복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="31892-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
