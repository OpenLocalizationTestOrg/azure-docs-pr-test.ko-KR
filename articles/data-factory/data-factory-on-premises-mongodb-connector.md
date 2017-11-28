---
title: "데이터 팩터리를 사용 하 여 MongoDB aaaMove 데이터로 | Microsoft Docs"
description: "Toomove 데이터로 MongoDB 데이터베이스 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="73326-103">Azure Data Factory를 사용하여 MongoDB에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="73326-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="73326-104">이 문서에서는 Azure Data Factory toomove 데이터베이스의에서 데이터를 온-프레미스 MongoDB에 toouse 복사 작업 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="73326-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="73326-106">온-프레미스 MongoDB 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="73326-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="73326-108">데이터 팩터리는 현재 이동 MongoDB 데이터에서 데이터 저장 tooother 데이터 저장소 뿐만 아니라 다른 데이터 저장소 tooan MongoDB 데이터 저장소에서 데이터 이동에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="73326-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="73326-109">Prerequisites</span></span>
<span data-ttu-id="73326-110">Hello Azure Data Factory 서비스 toobe 수 tooconnect tooyour 온-프레미스 MongoDB 데이터베이스에 대 한 다음과 같은 구성 요소가 hello를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="73326-111">지원되는 MongoDB 버전:  2.4, 2.6, 3.0 및 3.2.</span><span class="sxs-lookup"><span data-stu-id="73326-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="73326-112">데이터 관리 게이트웨이를 동일한 컴퓨터를 hello 데이터베이스를 호스팅 함 hello 또는 경쟁 hello 데이터베이스와 리소스에 대 한 별도 컴퓨터 tooavoid 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="73326-113">데이터 관리 게이트웨이 온-프레미스 데이터 원본 toocloud 서비스를 안전 하 고 관리 되는 방식으로 연결 하는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="73326-114">데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73326-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="73326-115">참조 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 toomove 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="73326-116">Hello 게이트웨이 설치할 때 자동으로 Microsoft MongoDB ODBC 사용 되는 드라이버 tooconnect tooMongoDB를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="73326-117">Azure IaaS Vm에서 호스팅되는 경우에 toouse hello 게이트웨이 tooconnect tooMongoDB 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="73326-118">Tooconnect tooan 인스턴스의 클라우드에서 호스트 되는 MongoDB 시도 하는 경우에 hello IaaS VM에에서 hello 게이트웨이 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="73326-119">시작</span><span class="sxs-lookup"><span data-stu-id="73326-119">Getting started</span></span>
<span data-ttu-id="73326-120">여러 도구/API를 사용하여 온-프레미스 MongoDB 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="73326-121">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="73326-122">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="73326-123">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="73326-124">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="73326-125">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="73326-126">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="73326-127">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="73326-128">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73326-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="73326-129">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73326-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="73326-130">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="73326-131">Data Factory 된 엔터티를 온-프레미스 MongoDB 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: MongoDB tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-mongodb-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="73326-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="73326-132">사용 되는 toodefine Data Factory 엔터티에 특정 tooMongoDB 소스는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="73326-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="73326-133">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="73326-133">Linked service properties</span></span>
<span data-ttu-id="73326-134">hello 다음 표에서 설명 특정 JSON 요소에 대 한 너무**OnPremisesMongoDB** 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="73326-135">속성</span><span class="sxs-lookup"><span data-stu-id="73326-135">Property</span></span> | <span data-ttu-id="73326-136">설명</span><span class="sxs-lookup"><span data-stu-id="73326-136">Description</span></span> | <span data-ttu-id="73326-137">필수</span><span class="sxs-lookup"><span data-stu-id="73326-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73326-138">type</span><span class="sxs-lookup"><span data-stu-id="73326-138">type</span></span> |<span data-ttu-id="73326-139">hello type 속성 설정 해야 합니다: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="73326-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="73326-140">예</span><span class="sxs-lookup"><span data-stu-id="73326-140">Yes</span></span> |
| <span data-ttu-id="73326-141">server</span><span class="sxs-lookup"><span data-stu-id="73326-141">server</span></span> |<span data-ttu-id="73326-142">Hello MongoDB 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="73326-143">예</span><span class="sxs-lookup"><span data-stu-id="73326-143">Yes</span></span> |
| <span data-ttu-id="73326-144">포트</span><span class="sxs-lookup"><span data-stu-id="73326-144">port</span></span> |<span data-ttu-id="73326-145">MongoDB 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="73326-146">선택 사항, 기본값: 27017</span><span class="sxs-lookup"><span data-stu-id="73326-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="73326-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="73326-147">authenticationType</span></span> |<span data-ttu-id="73326-148">Basic 또는 Anonymous입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="73326-149">예</span><span class="sxs-lookup"><span data-stu-id="73326-149">Yes</span></span> |
| <span data-ttu-id="73326-150">username</span><span class="sxs-lookup"><span data-stu-id="73326-150">username</span></span> |<span data-ttu-id="73326-151">사용자 계정 tooaccess MongoDB 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="73326-152">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="73326-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="73326-153">암호</span><span class="sxs-lookup"><span data-stu-id="73326-153">password</span></span> |<span data-ttu-id="73326-154">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-154">Password for hello user.</span></span> |<span data-ttu-id="73326-155">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="73326-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="73326-156">authSource</span><span class="sxs-lookup"><span data-stu-id="73326-156">authSource</span></span> |<span data-ttu-id="73326-157">원하는 toouse toocheck 자격 증명 인증에 대 한 hello MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="73326-158">선택 사항(기본 인증을 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="73326-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="73326-159">기본값: hello 관리자 계정 및 databaseName 속성을 사용 하 여 지정 하는 hello 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="73326-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="73326-160">databaseName</span></span> |<span data-ttu-id="73326-161">원하는 tooaccess hello MongoDB 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="73326-162">예</span><span class="sxs-lookup"><span data-stu-id="73326-162">Yes</span></span> |
| <span data-ttu-id="73326-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="73326-163">gatewayName</span></span> |<span data-ttu-id="73326-164">Hello 데이터 저장소에 액세스 하는 hello 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="73326-165">예</span><span class="sxs-lookup"><span data-stu-id="73326-165">Yes</span></span> |
| <span data-ttu-id="73326-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="73326-166">encryptedCredential</span></span> |<span data-ttu-id="73326-167">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="73326-168">옵션</span><span class="sxs-lookup"><span data-stu-id="73326-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="73326-169">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="73326-169">Dataset properties</span></span>
<span data-ttu-id="73326-170">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="73326-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="73326-171">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="73326-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="73326-172">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="73326-173">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **MongoDbCollection** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="73326-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="73326-174">속성</span><span class="sxs-lookup"><span data-stu-id="73326-174">Property</span></span> | <span data-ttu-id="73326-175">설명</span><span class="sxs-lookup"><span data-stu-id="73326-175">Description</span></span> | <span data-ttu-id="73326-176">필수</span><span class="sxs-lookup"><span data-stu-id="73326-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73326-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="73326-177">collectionName</span></span> |<span data-ttu-id="73326-178">MongoDB 데이터베이스의 hello 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="73326-179">예</span><span class="sxs-lookup"><span data-stu-id="73326-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="73326-180">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="73326-180">Copy activity properties</span></span>
<span data-ttu-id="73326-181">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="73326-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="73326-182">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="73326-183">Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="73326-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="73326-184">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="73326-185">Hello 원본 유형의 경우 **MongoDbSource** 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="73326-186">속성</span><span class="sxs-lookup"><span data-stu-id="73326-186">Property</span></span> | <span data-ttu-id="73326-187">설명</span><span class="sxs-lookup"><span data-stu-id="73326-187">Description</span></span> | <span data-ttu-id="73326-188">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="73326-188">Allowed values</span></span> | <span data-ttu-id="73326-189">필수</span><span class="sxs-lookup"><span data-stu-id="73326-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="73326-190">쿼리</span><span class="sxs-lookup"><span data-stu-id="73326-190">query</span></span> |<span data-ttu-id="73326-191">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="73326-192">SQL-92 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-192">SQL-92 query string.</span></span> <span data-ttu-id="73326-193">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="73326-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="73326-194">아니요(**데이터 집합**의 **collectionName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="73326-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="73326-195">JSON의 예: MongoDB tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="73326-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="73326-196">이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="73326-197">표시 방법을 온-프레미스 MongoDB tooan Azure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="73326-198">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="73326-199">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="73326-200">[OnPremisesMongoDb](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="73326-201">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="73326-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="73326-202">[MongoDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="73326-203">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="73326-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="73326-204">[MongoDbSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="73326-205">hello 샘플 데이터 복사 MongoDB 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="73326-206">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="73326-207">첫 번째 단계로, hello의 hello 지침에 따라 hello 데이터 관리 게이트웨이 설치 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="73326-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="73326-208">**MongoDB 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="73326-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="73326-209">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="73326-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="73326-210">**MongoDB 입력된 데이터 집합:** 설정 "외부": "true" 알립니다 hello 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="73326-211">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="73326-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="73326-212">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="73326-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="73326-213">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73326-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="73326-214">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="73326-215">**MongoDB 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="73326-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="73326-216">hello 파이프라인 입력 및 출력 데이터 집합 위에 구성 된 toouse hello 고 1 시간 마다 예정 된 toorun 길이가 복사 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="73326-217">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**MongoDbSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="73326-218">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="73326-219">Data Factory에서의 스키마</span><span class="sxs-lookup"><span data-stu-id="73326-219">Schema by Data Factory</span></span>
<span data-ttu-id="73326-220">Azure 데이터 팩터리 서비스는 hello 컬렉션에 있는 최신 100 hello 문서를 사용 하 여 MongoDB 컬렉션에서 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="73326-221">100 이러한 문서를 전체 스키마 포함 되어 있지 않으면 hello 복사 작업 중 일부 열을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="73326-222">MongoDB에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="73326-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="73326-223">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 단계 2 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="73326-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="73326-224">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="73326-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="73326-225">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="73326-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="73326-226">다음 데이터 tooMongoDB hello를 이동할 때 매핑이 MongoDB 형식 too.NET 형식에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73326-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="73326-227">MongoDB 형식</span><span class="sxs-lookup"><span data-stu-id="73326-227">MongoDB type</span></span> | <span data-ttu-id="73326-228">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="73326-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="73326-229">이진</span><span class="sxs-lookup"><span data-stu-id="73326-229">Binary</span></span> |<span data-ttu-id="73326-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="73326-230">Byte[]</span></span> |
| <span data-ttu-id="73326-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="73326-231">Boolean</span></span> |<span data-ttu-id="73326-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="73326-232">Boolean</span></span> |
| <span data-ttu-id="73326-233">Date</span><span class="sxs-lookup"><span data-stu-id="73326-233">Date</span></span> |<span data-ttu-id="73326-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="73326-234">DateTime</span></span> |
| <span data-ttu-id="73326-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="73326-235">NumberDouble</span></span> |<span data-ttu-id="73326-236">Double</span><span class="sxs-lookup"><span data-stu-id="73326-236">Double</span></span> |
| <span data-ttu-id="73326-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="73326-237">NumberInt</span></span> |<span data-ttu-id="73326-238">Int32</span><span class="sxs-lookup"><span data-stu-id="73326-238">Int32</span></span> |
| <span data-ttu-id="73326-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="73326-239">NumberLong</span></span> |<span data-ttu-id="73326-240">Int64</span><span class="sxs-lookup"><span data-stu-id="73326-240">Int64</span></span> |
| <span data-ttu-id="73326-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="73326-241">ObjectID</span></span> |<span data-ttu-id="73326-242">문자열</span><span class="sxs-lookup"><span data-stu-id="73326-242">String</span></span> |
| <span data-ttu-id="73326-243">문자열</span><span class="sxs-lookup"><span data-stu-id="73326-243">String</span></span> |<span data-ttu-id="73326-244">문자열</span><span class="sxs-lookup"><span data-stu-id="73326-244">String</span></span> |
| <span data-ttu-id="73326-245">UUID</span><span class="sxs-lookup"><span data-stu-id="73326-245">UUID</span></span> |<span data-ttu-id="73326-246">Guid</span><span class="sxs-lookup"><span data-stu-id="73326-246">Guid</span></span> |
| <span data-ttu-id="73326-247">Object</span><span class="sxs-lookup"><span data-stu-id="73326-247">Object</span></span> |<span data-ttu-id="73326-248">중첩 구분 기호로 “_”를 사용한 평면화된 열에 다시 정규화</span><span class="sxs-lookup"><span data-stu-id="73326-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="73326-249">가상 테이블을 사용 하 여 배열에 대 한 지원에 대 한 toolearn 너무 참조[가상 테이블을 사용 하는 복합 형식에 대 한 지원](#support-for-complex-types-using-virtual-tables) 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="73326-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="73326-250">현재 hello MongoDB 데이터 유형만 지원 되지 않습니다: DBPointer, JavaScript, 최대/최소 키, 정규식, 기호, 타임 스탬프, 정의 되지 않음</span><span class="sxs-lookup"><span data-stu-id="73326-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="73326-251">가상 테이블을 사용하는 복합 형식에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="73326-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="73326-252">Azure 데이터 팩터리는 기본 제공 ODBC 드라이버 tooconnect tooand에서에서 데이터 복사 MongoDB 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="73326-253">Hello 문서에서 여러 형식으로 배열 또는 개체와 같은 복합 형식에 대 한 hello 드라이버를 다시 데이터를 해당 가상 테이블로 정규화합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="73326-254">특히, 이러한 열을 포함 하는 테이블, hello 드라이버 hello 다음 가상 표를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="73326-255">A **기본 테이블**, 포함 된 hello hello 복합 유형 열을 제외한 실제 테이블 hello와 동일한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="73326-256">hello 기본 테이블 표시 되는 hello 실제 테이블 hello 이름과 같은 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="73326-257">A **가상 테이블** 각 복합 형식 열에 대 한 hello 중첩 된 데이터 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="73326-258">hello hello 실제 테이블 이름, 구분 기호 "_" 및 hello 배열 또는 개체의 hello 이름을 사용 하 여 가상 테이블 hello 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="73326-259">가상 테이블 참조 toohello hello 실제 테이블에는 데이터, 사용할 수 있도록 hello 드라이버 tooaccess hello 비 정규화 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="73326-260">자세한 내용은 아래의 예제 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73326-260">See Example section below details.</span></span> <span data-ttu-id="73326-261">쿼리 한 hello 가상 테이블을 조인 하 여 MongoDB 배열의 hello 콘텐츠를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="73326-262">Hello를 사용할 수 있습니다 [복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively hello 가상 테이블을 포함 한 MongoDB 데이터베이스에서 테이블 목록을 hello 뷰와 내부 hello 데이터를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="73326-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="73326-263">Hello 복사 마법사에서에서 쿼리를 작성 하 고 toosee hello 결과 유효성을 검사 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="73326-264">예제</span><span class="sxs-lookup"><span data-stu-id="73326-264">Example</span></span>
<span data-ttu-id="73326-265">예를 들어, 아래 "ExampleTable"은 MongoDB 테이블로, 각 셀의 개체 배열이 있는 하나의 열(송장)과 스칼라 형식의 배열이 있는 하나의 열(등급)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="73326-266">_id</span><span class="sxs-lookup"><span data-stu-id="73326-266">_id</span></span> | <span data-ttu-id="73326-267">고객 이름</span><span class="sxs-lookup"><span data-stu-id="73326-267">Customer Name</span></span> | <span data-ttu-id="73326-268">송장</span><span class="sxs-lookup"><span data-stu-id="73326-268">Invoices</span></span> | <span data-ttu-id="73326-269">서비스 수준</span><span class="sxs-lookup"><span data-stu-id="73326-269">Service Level</span></span> | <span data-ttu-id="73326-270">등급</span><span class="sxs-lookup"><span data-stu-id="73326-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="73326-271">1111</span><span class="sxs-lookup"><span data-stu-id="73326-271">1111</span></span> |<span data-ttu-id="73326-272">ABC</span><span class="sxs-lookup"><span data-stu-id="73326-272">ABC</span></span> |<span data-ttu-id="73326-273">[{송장_id:”123”, 항목:”토스터”, 가격:”456”, 할인:”0.2”}, {송장_id:”124”, 항목:”오븐”, 가격: ”1235”, 할인: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="73326-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="73326-274">Silver</span><span class="sxs-lookup"><span data-stu-id="73326-274">Silver</span></span> |<span data-ttu-id="73326-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="73326-275">[5,6]</span></span> |
| <span data-ttu-id="73326-276">2222</span><span class="sxs-lookup"><span data-stu-id="73326-276">2222</span></span> |<span data-ttu-id="73326-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="73326-277">XYZ</span></span> |<span data-ttu-id="73326-278">[{송장_id:”135”, 항목:”냉장고”, 가격: ”12543”, 할인: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="73326-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="73326-279">Gold</span><span class="sxs-lookup"><span data-stu-id="73326-279">Gold</span></span> |<span data-ttu-id="73326-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="73326-280">[1,2]</span></span> |

<span data-ttu-id="73326-281">hello 드라이버는이 단일 표에 여러 가상 테이블 toorepresent 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="73326-282">hello 첫 번째 가상 테이블은 아래에 표시 된 "ExampleTable" 라는 hello 기본 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="73326-283">hello 원래 테이블의 모든 hello 데이터를 포함 하는 기본 테이블 hello 되지만 hello 데이터 hello 배열에서 누락 되었습니다. hello 가상 테이블에 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73326-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="73326-284">_id</span><span class="sxs-lookup"><span data-stu-id="73326-284">_id</span></span> | <span data-ttu-id="73326-285">고객 이름</span><span class="sxs-lookup"><span data-stu-id="73326-285">Customer Name</span></span> | <span data-ttu-id="73326-286">서비스 수준</span><span class="sxs-lookup"><span data-stu-id="73326-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73326-287">1111</span><span class="sxs-lookup"><span data-stu-id="73326-287">1111</span></span> |<span data-ttu-id="73326-288">ABC</span><span class="sxs-lookup"><span data-stu-id="73326-288">ABC</span></span> |<span data-ttu-id="73326-289">Silver</span><span class="sxs-lookup"><span data-stu-id="73326-289">Silver</span></span> |
| <span data-ttu-id="73326-290">2222</span><span class="sxs-lookup"><span data-stu-id="73326-290">2222</span></span> |<span data-ttu-id="73326-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="73326-291">XYZ</span></span> |<span data-ttu-id="73326-292">Gold</span><span class="sxs-lookup"><span data-stu-id="73326-292">Gold</span></span> |

<span data-ttu-id="73326-293">hello 다음 표에서 보여 hello hello 예제에서 hello 원래 배열을 나타내는 가상 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="73326-294">이러한 테이블 hello 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-294">These tables contain hello following:</span></span>

* <span data-ttu-id="73326-295">에 대 한 역참조 (hello _id 열)를 통해 toohello 원래 기본 키 열 toohello의 해당 행 hello 원본 배열</span><span class="sxs-lookup"><span data-stu-id="73326-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="73326-296">hello 데이터 hello 원래 배열 내에서 hello 위치 표시</span><span class="sxs-lookup"><span data-stu-id="73326-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="73326-297">hello는 hello 배열 내의 각 요소에 대 한 데이터 확장</span><span class="sxs-lookup"><span data-stu-id="73326-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="73326-298">테이블 "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="73326-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="73326-299">_id</span><span class="sxs-lookup"><span data-stu-id="73326-299">_id</span></span> | <span data-ttu-id="73326-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="73326-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="73326-301">송장_id</span><span class="sxs-lookup"><span data-stu-id="73326-301">invoice_id</span></span> | <span data-ttu-id="73326-302">항목</span><span class="sxs-lookup"><span data-stu-id="73326-302">item</span></span> | <span data-ttu-id="73326-303">가격</span><span class="sxs-lookup"><span data-stu-id="73326-303">price</span></span> | <span data-ttu-id="73326-304">할인</span><span class="sxs-lookup"><span data-stu-id="73326-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="73326-305">1111</span><span class="sxs-lookup"><span data-stu-id="73326-305">1111</span></span> |<span data-ttu-id="73326-306">0</span><span class="sxs-lookup"><span data-stu-id="73326-306">0</span></span> |<span data-ttu-id="73326-307">123</span><span class="sxs-lookup"><span data-stu-id="73326-307">123</span></span> |<span data-ttu-id="73326-308">토스터</span><span class="sxs-lookup"><span data-stu-id="73326-308">toaster</span></span> |<span data-ttu-id="73326-309">456</span><span class="sxs-lookup"><span data-stu-id="73326-309">456</span></span> |<span data-ttu-id="73326-310">0.2</span><span class="sxs-lookup"><span data-stu-id="73326-310">0.2</span></span> |
| <span data-ttu-id="73326-311">1111</span><span class="sxs-lookup"><span data-stu-id="73326-311">1111</span></span> |<span data-ttu-id="73326-312">1</span><span class="sxs-lookup"><span data-stu-id="73326-312">1</span></span> |<span data-ttu-id="73326-313">124</span><span class="sxs-lookup"><span data-stu-id="73326-313">124</span></span> |<span data-ttu-id="73326-314">오븐</span><span class="sxs-lookup"><span data-stu-id="73326-314">oven</span></span> |<span data-ttu-id="73326-315">1235</span><span class="sxs-lookup"><span data-stu-id="73326-315">1235</span></span> |<span data-ttu-id="73326-316">0.2</span><span class="sxs-lookup"><span data-stu-id="73326-316">0.2</span></span> |
| <span data-ttu-id="73326-317">2222</span><span class="sxs-lookup"><span data-stu-id="73326-317">2222</span></span> |<span data-ttu-id="73326-318">0</span><span class="sxs-lookup"><span data-stu-id="73326-318">0</span></span> |<span data-ttu-id="73326-319">135</span><span class="sxs-lookup"><span data-stu-id="73326-319">135</span></span> |<span data-ttu-id="73326-320">냉장고</span><span class="sxs-lookup"><span data-stu-id="73326-320">fridge</span></span> |<span data-ttu-id="73326-321">12543</span><span class="sxs-lookup"><span data-stu-id="73326-321">12543</span></span> |<span data-ttu-id="73326-322">0.0</span><span class="sxs-lookup"><span data-stu-id="73326-322">0.0</span></span> |

<span data-ttu-id="73326-323">테이블 "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="73326-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="73326-324">_id</span><span class="sxs-lookup"><span data-stu-id="73326-324">_id</span></span> | <span data-ttu-id="73326-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="73326-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="73326-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="73326-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73326-327">1111</span><span class="sxs-lookup"><span data-stu-id="73326-327">1111</span></span> |<span data-ttu-id="73326-328">0</span><span class="sxs-lookup"><span data-stu-id="73326-328">0</span></span> |<span data-ttu-id="73326-329">5</span><span class="sxs-lookup"><span data-stu-id="73326-329">5</span></span> |
| <span data-ttu-id="73326-330">1111</span><span class="sxs-lookup"><span data-stu-id="73326-330">1111</span></span> |<span data-ttu-id="73326-331">1</span><span class="sxs-lookup"><span data-stu-id="73326-331">1</span></span> |<span data-ttu-id="73326-332">6</span><span class="sxs-lookup"><span data-stu-id="73326-332">6</span></span> |
| <span data-ttu-id="73326-333">2222</span><span class="sxs-lookup"><span data-stu-id="73326-333">2222</span></span> |<span data-ttu-id="73326-334">0</span><span class="sxs-lookup"><span data-stu-id="73326-334">0</span></span> |<span data-ttu-id="73326-335">1</span><span class="sxs-lookup"><span data-stu-id="73326-335">1</span></span> |
| <span data-ttu-id="73326-336">2222</span><span class="sxs-lookup"><span data-stu-id="73326-336">2222</span></span> |<span data-ttu-id="73326-337">1</span><span class="sxs-lookup"><span data-stu-id="73326-337">1</span></span> |<span data-ttu-id="73326-338">2</span><span class="sxs-lookup"><span data-stu-id="73326-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="73326-339">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="73326-339">Map source toosink columns</span></span>
<span data-ttu-id="73326-340">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73326-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="73326-341">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="73326-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="73326-342">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="73326-343">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="73326-344">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73326-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="73326-345">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73326-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="73326-346">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73326-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="73326-347">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="73326-347">Performance and Tuning</span></span>
<span data-ttu-id="73326-348">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73326-349">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73326-349">Next Steps</span></span>
<span data-ttu-id="73326-350">참조 [온-프레미스와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) tooan Azure 데이터 저장소를 저장 하는 데이터는 온-프레미스 데이터를 이동 하는 데이터 파이프라인 만들기에 대 한 단계별 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="73326-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
