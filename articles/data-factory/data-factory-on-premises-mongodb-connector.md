---
title: "Data Factory를 사용하여 MongoDB에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 MongoDB 데이터베이스에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="616bc-103">Azure Data Factory를 사용하여 MongoDB에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="616bc-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="616bc-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 MongoDB 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="616bc-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="616bc-106">온-프레미스 MongoDB 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="616bc-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="616bc-108">현재 데이터 팩터리는 다른 데이터 저장소에서 MongoDB 데이터 저장소로 데이터 이동이 아닌 MongoDB 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="616bc-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="616bc-109">Prerequisites</span></span>
<span data-ttu-id="616bc-110">Azure Data Factory 서비스가 사용자의 온-프레미스 MongoDB 데이터베이스에 연결할 수 있도록 하려면 다음 구성 요소를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="616bc-111">지원되는 MongoDB 버전:  2.4, 2.6, 3.0 및 3.2.</span><span class="sxs-lookup"><span data-stu-id="616bc-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="616bc-112">데이터 관리 게이트웨이를 데이터베이스를 호스팅하는 컴퓨터와 같은 컴퓨터에 설치하거나 데이터베이스와 리소스 경쟁을 피하려면 별도의 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="616bc-113">데이터 관리 게이트웨이는 온-프레미스 데이터 원본을 클라우드 서비스에 안전하고 관리되는 방식으로 연결하는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="616bc-114">데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="616bc-115">데이터 이동을 위한 데이터 파이프라인 및 게이트웨이 설정에 대한 단계별 지침은 [온-프레미스에서 클라우드로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="616bc-116">게이트웨이를 설치하면 MongoDB에 연결하는 데 사용되는 Microsoft MongoDB ODBC 드라이버가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="616bc-117">Azure IaaS VM에서 호스팅되는 경우에도 MongoDB에 연결하려면 게이트웨이를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="616bc-118">또한 클라우드에서 호스트되는 MongoDB의 인스턴스에 연결하려고 하는 경우 IaaS VM에 게이트웨이 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="616bc-119">시작</span><span class="sxs-lookup"><span data-stu-id="616bc-119">Getting started</span></span>
<span data-ttu-id="616bc-120">여러 도구/API를 사용하여 온-프레미스 MongoDB 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="616bc-121">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="616bc-122">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="616bc-123">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="616bc-124">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="616bc-125">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="616bc-126">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="616bc-127">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="616bc-128">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="616bc-129">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="616bc-130">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="616bc-131">온-프레미스 MongoDB 데이터 저장소의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: MongoDB에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-mongodb-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="616bc-132">다음 섹션에서는 MongoDB 소스에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="616bc-133">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="616bc-133">Linked service properties</span></span>
<span data-ttu-id="616bc-134">다음 테이블은 **OnPremisesMongoDB** 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="616bc-135">속성</span><span class="sxs-lookup"><span data-stu-id="616bc-135">Property</span></span> | <span data-ttu-id="616bc-136">설명</span><span class="sxs-lookup"><span data-stu-id="616bc-136">Description</span></span> | <span data-ttu-id="616bc-137">필수</span><span class="sxs-lookup"><span data-stu-id="616bc-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="616bc-138">type</span><span class="sxs-lookup"><span data-stu-id="616bc-138">type</span></span> |<span data-ttu-id="616bc-139">형식 속성은 **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="616bc-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="616bc-140">예</span><span class="sxs-lookup"><span data-stu-id="616bc-140">Yes</span></span> |
| <span data-ttu-id="616bc-141">server</span><span class="sxs-lookup"><span data-stu-id="616bc-141">server</span></span> |<span data-ttu-id="616bc-142">MongoDB 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="616bc-143">예</span><span class="sxs-lookup"><span data-stu-id="616bc-143">Yes</span></span> |
| <span data-ttu-id="616bc-144">포트</span><span class="sxs-lookup"><span data-stu-id="616bc-144">port</span></span> |<span data-ttu-id="616bc-145">MongoDB 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="616bc-146">선택 사항, 기본값: 27017</span><span class="sxs-lookup"><span data-stu-id="616bc-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="616bc-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="616bc-147">authenticationType</span></span> |<span data-ttu-id="616bc-148">Basic 또는 Anonymous입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="616bc-149">예</span><span class="sxs-lookup"><span data-stu-id="616bc-149">Yes</span></span> |
| <span data-ttu-id="616bc-150">username</span><span class="sxs-lookup"><span data-stu-id="616bc-150">username</span></span> |<span data-ttu-id="616bc-151">MongoDB에 액세스하는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-151">User account to access MongoDB.</span></span> |<span data-ttu-id="616bc-152">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="616bc-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="616bc-153">password</span><span class="sxs-lookup"><span data-stu-id="616bc-153">password</span></span> |<span data-ttu-id="616bc-154">사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-154">Password for the user.</span></span> |<span data-ttu-id="616bc-155">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="616bc-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="616bc-156">authSource</span><span class="sxs-lookup"><span data-stu-id="616bc-156">authSource</span></span> |<span data-ttu-id="616bc-157">인증에 대한 자격 증명을 확인하는 데 사용하려는 MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="616bc-158">선택 사항(기본 인증을 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="616bc-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="616bc-159">기본값: 관리자 계정 및 databaseName 속성을 사용하는 지정된 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="616bc-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="616bc-160">databaseName</span></span> |<span data-ttu-id="616bc-161">액세스하려는 MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="616bc-162">예</span><span class="sxs-lookup"><span data-stu-id="616bc-162">Yes</span></span> |
| <span data-ttu-id="616bc-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="616bc-163">gatewayName</span></span> |<span data-ttu-id="616bc-164">데이터 저장소에 액세스하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="616bc-165">예</span><span class="sxs-lookup"><span data-stu-id="616bc-165">Yes</span></span> |
| <span data-ttu-id="616bc-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="616bc-166">encryptedCredential</span></span> |<span data-ttu-id="616bc-167">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="616bc-168">옵션</span><span class="sxs-lookup"><span data-stu-id="616bc-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="616bc-169">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="616bc-169">Dataset properties</span></span>
<span data-ttu-id="616bc-170">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="616bc-171">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="616bc-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="616bc-172">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="616bc-173">**MongoDbCollection** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="616bc-174">속성</span><span class="sxs-lookup"><span data-stu-id="616bc-174">Property</span></span> | <span data-ttu-id="616bc-175">설명</span><span class="sxs-lookup"><span data-stu-id="616bc-175">Description</span></span> | <span data-ttu-id="616bc-176">필수</span><span class="sxs-lookup"><span data-stu-id="616bc-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="616bc-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="616bc-177">collectionName</span></span> |<span data-ttu-id="616bc-178">MongoDB 데이터베이스에 있는 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="616bc-179">예</span><span class="sxs-lookup"><span data-stu-id="616bc-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="616bc-180">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="616bc-180">Copy activity properties</span></span>
<span data-ttu-id="616bc-181">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="616bc-182">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="616bc-183">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="616bc-184">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="616bc-185">원본이 **MongoDbSource** 형식인 경우 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="616bc-186">속성</span><span class="sxs-lookup"><span data-stu-id="616bc-186">Property</span></span> | <span data-ttu-id="616bc-187">설명</span><span class="sxs-lookup"><span data-stu-id="616bc-187">Description</span></span> | <span data-ttu-id="616bc-188">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="616bc-188">Allowed values</span></span> | <span data-ttu-id="616bc-189">필수</span><span class="sxs-lookup"><span data-stu-id="616bc-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="616bc-190">쿼리</span><span class="sxs-lookup"><span data-stu-id="616bc-190">query</span></span> |<span data-ttu-id="616bc-191">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-191">Use the custom query to read data.</span></span> |<span data-ttu-id="616bc-192">SQL-92 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-192">SQL-92 query string.</span></span> <span data-ttu-id="616bc-193">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="616bc-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="616bc-194">아니요(**데이터 집합**의 **collectionName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="616bc-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="616bc-195">JSON 예: MongoDB에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="616bc-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="616bc-196">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="616bc-197">온-프레미스 MongoDB에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="616bc-198">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="616bc-199">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="616bc-200">[OnPremisesMongoDb](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="616bc-201">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="616bc-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="616bc-202">[MongoDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="616bc-203">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="616bc-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="616bc-204">[MongoDbSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="616bc-205">샘플은 MongoDB 데이터베이스의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="616bc-206">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="616bc-207">첫 번째 단계로 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서의 지침에 따라 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="616bc-208">**MongoDB 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="616bc-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="616bc-209">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="616bc-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="616bc-210">**MongoDB 입력 데이터 집합** "external": "true"를 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="616bc-211">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="616bc-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="616bc-212">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="616bc-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="616bc-213">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="616bc-214">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="616bc-215">**MongoDB 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="616bc-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="616bc-216">파이프라인은 위의 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="616bc-217">파이프라인 JSON 정의에서 **source** 형식은 **MongoDbSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="616bc-218">**query** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="616bc-219">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="616bc-219">Schema by Data Factory</span></span>
<span data-ttu-id="616bc-220">Azure Data Factory 서비스는 컬렉션에 있는 최신 100개의 문서를 사용하여 MongoDB 컬렉션에서 스키마를 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="616bc-221">이러한 100개의 문서에 전체 스키마가 포함되어 있지 않는 경우, 일부 열은 복사 작업 중 무시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="616bc-222">MongoDB에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="616bc-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="616bc-223">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="616bc-224">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="616bc-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="616bc-225">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="616bc-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="616bc-226">MongoDB에 데이터를 이동하는 경우 MongoDB 형식에서 .NET 형식으로 이동에 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="616bc-227">MongoDB 형식</span><span class="sxs-lookup"><span data-stu-id="616bc-227">MongoDB type</span></span> | <span data-ttu-id="616bc-228">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="616bc-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="616bc-229">이진</span><span class="sxs-lookup"><span data-stu-id="616bc-229">Binary</span></span> |<span data-ttu-id="616bc-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="616bc-230">Byte[]</span></span> |
| <span data-ttu-id="616bc-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="616bc-231">Boolean</span></span> |<span data-ttu-id="616bc-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="616bc-232">Boolean</span></span> |
| <span data-ttu-id="616bc-233">Date</span><span class="sxs-lookup"><span data-stu-id="616bc-233">Date</span></span> |<span data-ttu-id="616bc-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="616bc-234">DateTime</span></span> |
| <span data-ttu-id="616bc-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="616bc-235">NumberDouble</span></span> |<span data-ttu-id="616bc-236">Double</span><span class="sxs-lookup"><span data-stu-id="616bc-236">Double</span></span> |
| <span data-ttu-id="616bc-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="616bc-237">NumberInt</span></span> |<span data-ttu-id="616bc-238">Int32</span><span class="sxs-lookup"><span data-stu-id="616bc-238">Int32</span></span> |
| <span data-ttu-id="616bc-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="616bc-239">NumberLong</span></span> |<span data-ttu-id="616bc-240">Int64</span><span class="sxs-lookup"><span data-stu-id="616bc-240">Int64</span></span> |
| <span data-ttu-id="616bc-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="616bc-241">ObjectID</span></span> |<span data-ttu-id="616bc-242">문자열</span><span class="sxs-lookup"><span data-stu-id="616bc-242">String</span></span> |
| <span data-ttu-id="616bc-243">문자열</span><span class="sxs-lookup"><span data-stu-id="616bc-243">String</span></span> |<span data-ttu-id="616bc-244">문자열</span><span class="sxs-lookup"><span data-stu-id="616bc-244">String</span></span> |
| <span data-ttu-id="616bc-245">UUID</span><span class="sxs-lookup"><span data-stu-id="616bc-245">UUID</span></span> |<span data-ttu-id="616bc-246">Guid</span><span class="sxs-lookup"><span data-stu-id="616bc-246">Guid</span></span> |
| <span data-ttu-id="616bc-247">Object</span><span class="sxs-lookup"><span data-stu-id="616bc-247">Object</span></span> |<span data-ttu-id="616bc-248">중첩 구분 기호로 “_”를 사용한 평면화된 열에 다시 정규화</span><span class="sxs-lookup"><span data-stu-id="616bc-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="616bc-249">가상 테이블을 사용한 배열 지원에 대해 알아보려면 아래의 [가상 테이블을 사용하는 복합 형식에 대한 지원](#support-for-complex-types-using-virtual-tables) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="616bc-250">현재 DBPointer, JavaScript, 최대/최소 키, 정규식, 기호, 타임 스탬프, 그리고 정의되지 않은 MongoDB 데이터 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="616bc-251">가상 테이블을 사용하는 복합 형식에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="616bc-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="616bc-252">Azure Data Factory는 기본 제공 ODBC 드라이버를 사용하여 MongoDB 데이터베이스에 연결하고 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="616bc-253">서로 다른 형식의 문서 간에 배열 또는 개체와 같은 복합 형식의 경우, 드라이버는 해당 가상 테이블에 데이터를 다시 정규화합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="616bc-254">특히, 테이블에 그러한 열이 포함되어 있으면 드라이버는 다음 가상 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="616bc-255">**기본 테이블**: 복합 형식 열을 제외하고 실제 테이블과 동일한 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="616bc-256">기본 테이블은 나타내는 실제 테이블과 동일한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="616bc-257">**가상 테이블** : 각 복합 형식 열에 대해 생성되며, 중첩된 데이터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="616bc-258">가상 테이블 이름은 실제 테이블의 이름, 구분 기호 “_” 그리고 배열 및 개체 이름을 사용하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="616bc-259">가상 테이블은 실제 테이블의 데이터를 나타내며, 드라이버가 정규화되지 않은 데이터에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="616bc-260">자세한 내용은 아래의 예제 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-260">See Example section below details.</span></span> <span data-ttu-id="616bc-261">가상 테이블을 쿼리 및 조인하여 MongoDB 배열의 콘텐츠에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="616bc-262">[복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) 를 사용하여 가상 테이블을 비롯한 MongoDB 데이터베이스의 테이블 목록을 표시하고 내부의 데이터를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="616bc-263">또한 복사 마법사에서 쿼리를 생성하고 결과가 유효한지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="616bc-264">예</span><span class="sxs-lookup"><span data-stu-id="616bc-264">Example</span></span>
<span data-ttu-id="616bc-265">예를 들어, 아래 "ExampleTable"은 MongoDB 테이블로, 각 셀의 개체 배열이 있는 하나의 열(송장)과 스칼라 형식의 배열이 있는 하나의 열(등급)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="616bc-266">_id</span><span class="sxs-lookup"><span data-stu-id="616bc-266">_id</span></span> | <span data-ttu-id="616bc-267">고객 이름</span><span class="sxs-lookup"><span data-stu-id="616bc-267">Customer Name</span></span> | <span data-ttu-id="616bc-268">송장</span><span class="sxs-lookup"><span data-stu-id="616bc-268">Invoices</span></span> | <span data-ttu-id="616bc-269">서비스 수준</span><span class="sxs-lookup"><span data-stu-id="616bc-269">Service Level</span></span> | <span data-ttu-id="616bc-270">등급</span><span class="sxs-lookup"><span data-stu-id="616bc-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="616bc-271">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-271">1111</span></span> |<span data-ttu-id="616bc-272">ABC</span><span class="sxs-lookup"><span data-stu-id="616bc-272">ABC</span></span> |<span data-ttu-id="616bc-273">[{송장_id:”123”, 항목:”토스터”, 가격:”456”, 할인:”0.2”}, {송장_id:”124”, 항목:”오븐”, 가격: ”1235”, 할인: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="616bc-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="616bc-274">Silver</span><span class="sxs-lookup"><span data-stu-id="616bc-274">Silver</span></span> |<span data-ttu-id="616bc-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="616bc-275">[5,6]</span></span> |
| <span data-ttu-id="616bc-276">2222</span><span class="sxs-lookup"><span data-stu-id="616bc-276">2222</span></span> |<span data-ttu-id="616bc-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="616bc-277">XYZ</span></span> |<span data-ttu-id="616bc-278">[{송장_id:”135”, 항목:”냉장고”, 가격: ”12543”, 할인: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="616bc-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="616bc-279">Gold</span><span class="sxs-lookup"><span data-stu-id="616bc-279">Gold</span></span> |<span data-ttu-id="616bc-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="616bc-280">[1,2]</span></span> |

<span data-ttu-id="616bc-281">드라이버는 이 단일 테이블을 나타내는 여러 개의 가상 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="616bc-282">첫 번째 가상 테이블은 아래에 표시된 "ExampleTable"이라는 기본 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="616bc-283">기본 테이블에는 모든 원본 테이블의 데이터가 있지만, 배열의 데이터는 생략되었으며 가상 테이블에서 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="616bc-284">_id</span><span class="sxs-lookup"><span data-stu-id="616bc-284">_id</span></span> | <span data-ttu-id="616bc-285">고객 이름</span><span class="sxs-lookup"><span data-stu-id="616bc-285">Customer Name</span></span> | <span data-ttu-id="616bc-286">서비스 수준</span><span class="sxs-lookup"><span data-stu-id="616bc-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="616bc-287">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-287">1111</span></span> |<span data-ttu-id="616bc-288">ABC</span><span class="sxs-lookup"><span data-stu-id="616bc-288">ABC</span></span> |<span data-ttu-id="616bc-289">Silver</span><span class="sxs-lookup"><span data-stu-id="616bc-289">Silver</span></span> |
| <span data-ttu-id="616bc-290">2222</span><span class="sxs-lookup"><span data-stu-id="616bc-290">2222</span></span> |<span data-ttu-id="616bc-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="616bc-291">XYZ</span></span> |<span data-ttu-id="616bc-292">Gold</span><span class="sxs-lookup"><span data-stu-id="616bc-292">Gold</span></span> |

<span data-ttu-id="616bc-293">다음 표는 예제에서 원본 배열을 나타내는 가상 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="616bc-294">이들 테이블은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-294">These tables contain the following:</span></span>

* <span data-ttu-id="616bc-295">원본 배열의 행에 해당하는 원본 기본 키 열에 역참조(_id 열을 통해)</span><span class="sxs-lookup"><span data-stu-id="616bc-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="616bc-296">원본 배열 내에서 데이터의 위치 표시</span><span class="sxs-lookup"><span data-stu-id="616bc-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="616bc-297">배열 내의 각 요소에 대해 확장된 데이터</span><span class="sxs-lookup"><span data-stu-id="616bc-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="616bc-298">테이블 "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="616bc-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="616bc-299">_id</span><span class="sxs-lookup"><span data-stu-id="616bc-299">_id</span></span> | <span data-ttu-id="616bc-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="616bc-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="616bc-301">송장_id</span><span class="sxs-lookup"><span data-stu-id="616bc-301">invoice_id</span></span> | <span data-ttu-id="616bc-302">항목</span><span class="sxs-lookup"><span data-stu-id="616bc-302">item</span></span> | <span data-ttu-id="616bc-303">가격</span><span class="sxs-lookup"><span data-stu-id="616bc-303">price</span></span> | <span data-ttu-id="616bc-304">할인</span><span class="sxs-lookup"><span data-stu-id="616bc-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="616bc-305">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-305">1111</span></span> |<span data-ttu-id="616bc-306">0</span><span class="sxs-lookup"><span data-stu-id="616bc-306">0</span></span> |<span data-ttu-id="616bc-307">123</span><span class="sxs-lookup"><span data-stu-id="616bc-307">123</span></span> |<span data-ttu-id="616bc-308">토스터</span><span class="sxs-lookup"><span data-stu-id="616bc-308">toaster</span></span> |<span data-ttu-id="616bc-309">456</span><span class="sxs-lookup"><span data-stu-id="616bc-309">456</span></span> |<span data-ttu-id="616bc-310">0.2</span><span class="sxs-lookup"><span data-stu-id="616bc-310">0.2</span></span> |
| <span data-ttu-id="616bc-311">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-311">1111</span></span> |<span data-ttu-id="616bc-312">1</span><span class="sxs-lookup"><span data-stu-id="616bc-312">1</span></span> |<span data-ttu-id="616bc-313">124</span><span class="sxs-lookup"><span data-stu-id="616bc-313">124</span></span> |<span data-ttu-id="616bc-314">오븐</span><span class="sxs-lookup"><span data-stu-id="616bc-314">oven</span></span> |<span data-ttu-id="616bc-315">1235</span><span class="sxs-lookup"><span data-stu-id="616bc-315">1235</span></span> |<span data-ttu-id="616bc-316">0.2</span><span class="sxs-lookup"><span data-stu-id="616bc-316">0.2</span></span> |
| <span data-ttu-id="616bc-317">2222</span><span class="sxs-lookup"><span data-stu-id="616bc-317">2222</span></span> |<span data-ttu-id="616bc-318">0</span><span class="sxs-lookup"><span data-stu-id="616bc-318">0</span></span> |<span data-ttu-id="616bc-319">135</span><span class="sxs-lookup"><span data-stu-id="616bc-319">135</span></span> |<span data-ttu-id="616bc-320">냉장고</span><span class="sxs-lookup"><span data-stu-id="616bc-320">fridge</span></span> |<span data-ttu-id="616bc-321">12543</span><span class="sxs-lookup"><span data-stu-id="616bc-321">12543</span></span> |<span data-ttu-id="616bc-322">0.0</span><span class="sxs-lookup"><span data-stu-id="616bc-322">0.0</span></span> |

<span data-ttu-id="616bc-323">테이블 "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="616bc-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="616bc-324">_id</span><span class="sxs-lookup"><span data-stu-id="616bc-324">_id</span></span> | <span data-ttu-id="616bc-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="616bc-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="616bc-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="616bc-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="616bc-327">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-327">1111</span></span> |<span data-ttu-id="616bc-328">0</span><span class="sxs-lookup"><span data-stu-id="616bc-328">0</span></span> |<span data-ttu-id="616bc-329">5</span><span class="sxs-lookup"><span data-stu-id="616bc-329">5</span></span> |
| <span data-ttu-id="616bc-330">1111</span><span class="sxs-lookup"><span data-stu-id="616bc-330">1111</span></span> |<span data-ttu-id="616bc-331">1</span><span class="sxs-lookup"><span data-stu-id="616bc-331">1</span></span> |<span data-ttu-id="616bc-332">6</span><span class="sxs-lookup"><span data-stu-id="616bc-332">6</span></span> |
| <span data-ttu-id="616bc-333">2222</span><span class="sxs-lookup"><span data-stu-id="616bc-333">2222</span></span> |<span data-ttu-id="616bc-334">0</span><span class="sxs-lookup"><span data-stu-id="616bc-334">0</span></span> |<span data-ttu-id="616bc-335">1</span><span class="sxs-lookup"><span data-stu-id="616bc-335">1</span></span> |
| <span data-ttu-id="616bc-336">2222</span><span class="sxs-lookup"><span data-stu-id="616bc-336">2222</span></span> |<span data-ttu-id="616bc-337">1</span><span class="sxs-lookup"><span data-stu-id="616bc-337">1</span></span> |<span data-ttu-id="616bc-338">2</span><span class="sxs-lookup"><span data-stu-id="616bc-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="616bc-339">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="616bc-339">Map source to sink columns</span></span>
<span data-ttu-id="616bc-340">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="616bc-341">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="616bc-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="616bc-342">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="616bc-343">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="616bc-344">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="616bc-345">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="616bc-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="616bc-346">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="616bc-347">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="616bc-347">Performance and Tuning</span></span>
<span data-ttu-id="616bc-348">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="616bc-349">다음 단계</span><span class="sxs-lookup"><span data-stu-id="616bc-349">Next Steps</span></span>
<span data-ttu-id="616bc-350">온-프레미스 데이터 저장소에서 Azure 데이터 저장소로 데이터를 이동시키는 데이터 파이프라인을 만드는 단계별 지침은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="616bc-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
