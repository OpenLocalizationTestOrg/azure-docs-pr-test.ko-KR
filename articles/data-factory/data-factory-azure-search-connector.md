---
title: "데이터 팩터리를 사용 하 여 aaaPush 데이터 tooSearch 인덱스 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 toopush 데이터 tooAzure 검색 인덱스입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="49501-103">Azure 데이터 팩터리를 사용 하 여 데이터 tooan Azure 검색 인덱스를 푸시</span><span class="sxs-lookup"><span data-stu-id="49501-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="49501-104">이 문서에서는 toouse hello 복사 작업 toopush 데이터를 지원 되는 원본 데이터에서에서 tooAzure 검색 인덱스를 저장 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="49501-105">지원 되는 원본 데이터 저장소의 hello hello 소스 열에 나열 됩니다 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="49501-106">Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 복사 작업 및 지원 되는 데이터 저장소 조합이 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="49501-107">연결 사용</span><span class="sxs-lookup"><span data-stu-id="49501-107">Enabling connectivity</span></span>
<span data-ttu-id="49501-108">데이터 팩터리 서비스 tooallow tooan 온-프레미스 데이터 저장소를 연결, 온-프레미스 환경에 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="49501-109">Hello 원본 데이터를 호스팅하는 동일한 컴퓨터에 저장 하거나 경쟁 hello 데이터를 사용 하 여 리소스에 대 한 별도 컴퓨터 tooavoid 저장소 hello에 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="49501-110">데이터 관리 게이트웨이 온-프레미스 데이터 원본 toocloud 서비스 안전 하 고 관리 되는 방식으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="49501-111">데이터 관리 게이트웨이에 대한 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49501-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="49501-112">시작</span><span class="sxs-lookup"><span data-stu-id="49501-112">Getting started</span></span>
<span data-ttu-id="49501-113">다른 도구/Api를 사용 하 여 원본 데이터 저장소 tooAzure 검색 인덱스에서 데이터를 밀어 넣는 복사 활동으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="49501-114">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="49501-115">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="49501-116">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="49501-117">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="49501-118">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="49501-119">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="49501-120">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="49501-121">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49501-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="49501-122">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="49501-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="49501-123">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="49501-124">Data Factory 된 엔터티를 사용 하는 toocopy 데이터 tooAzure 검색 인덱스에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: 온-프레미스 SQL Server tooAzure 검색 인덱스에서 데이터를 복사](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="49501-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="49501-125">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure 검색 인덱스에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="49501-126">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="49501-126">Linked service properties</span></span>

<span data-ttu-id="49501-127">다음 표에서 hello JSON 요소를 특정 toohello 연결 된 Azure 검색 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="49501-128">속성</span><span class="sxs-lookup"><span data-stu-id="49501-128">Property</span></span> | <span data-ttu-id="49501-129">설명</span><span class="sxs-lookup"><span data-stu-id="49501-129">Description</span></span> | <span data-ttu-id="49501-130">필수</span><span class="sxs-lookup"><span data-stu-id="49501-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="49501-131">type</span><span class="sxs-lookup"><span data-stu-id="49501-131">type</span></span> | <span data-ttu-id="49501-132">hello type 속성 설정 해야 합니다: **AzureSearch**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="49501-133">예</span><span class="sxs-lookup"><span data-stu-id="49501-133">Yes</span></span> |
| <span data-ttu-id="49501-134">url</span><span class="sxs-lookup"><span data-stu-id="49501-134">url</span></span> | <span data-ttu-id="49501-135">Hello Azure 검색 서비스에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="49501-136">예</span><span class="sxs-lookup"><span data-stu-id="49501-136">Yes</span></span> |
| <span data-ttu-id="49501-137">key</span><span class="sxs-lookup"><span data-stu-id="49501-137">key</span></span> | <span data-ttu-id="49501-138">Hello Azure 검색 서비스에 대 한 관리자 키입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="49501-139">예</span><span class="sxs-lookup"><span data-stu-id="49501-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="49501-140">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="49501-140">Dataset properties</span></span>

<span data-ttu-id="49501-141">섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="49501-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="49501-142">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="49501-143">hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="49501-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="49501-144">hello typeProperties hello 형식의 데이터 집합에 대 한 섹션 **AzureSearchIndex** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="49501-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="49501-145">속성</span><span class="sxs-lookup"><span data-stu-id="49501-145">Property</span></span> | <span data-ttu-id="49501-146">설명</span><span class="sxs-lookup"><span data-stu-id="49501-146">Description</span></span> | <span data-ttu-id="49501-147">필수</span><span class="sxs-lookup"><span data-stu-id="49501-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="49501-148">type</span><span class="sxs-lookup"><span data-stu-id="49501-148">type</span></span> | <span data-ttu-id="49501-149">너무 hello 유형 속성을 설정 해야**AzureSearchIndex**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="49501-150">예</span><span class="sxs-lookup"><span data-stu-id="49501-150">Yes</span></span> |
| <span data-ttu-id="49501-151">indexName</span><span class="sxs-lookup"><span data-stu-id="49501-151">indexName</span></span> | <span data-ttu-id="49501-152">Hello Azure 검색 인덱스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="49501-153">데이터 팩터리 hello 인덱스가 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="49501-154">hello 인덱스 Azure 검색에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="49501-155">예</span><span class="sxs-lookup"><span data-stu-id="49501-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="49501-156">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="49501-156">Copy activity properties</span></span>
<span data-ttu-id="49501-157">섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="49501-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="49501-158">이름, 설명, 입력/출력 테이블, 다양한 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="49501-159">반면 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="49501-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="49501-160">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="49501-161">Hello 싱크 hello 유형인 경우 복사 작업에 대 한 **AzureSearchIndexSink**, 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="49501-162">속성</span><span class="sxs-lookup"><span data-stu-id="49501-162">Property</span></span> | <span data-ttu-id="49501-163">설명</span><span class="sxs-lookup"><span data-stu-id="49501-163">Description</span></span> | <span data-ttu-id="49501-164">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="49501-164">Allowed values</span></span> | <span data-ttu-id="49501-165">필수</span><span class="sxs-lookup"><span data-stu-id="49501-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="49501-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="49501-166">WriteBehavior</span></span> | <span data-ttu-id="49501-167">Toomerge 또는 교체 때 문서에에서 이미 있는지 hello 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="49501-168">Hello 참조 [WriteBehavior 속성](#writebehavior-property)합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="49501-169">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="49501-169">Merge (default)</span></span><br/><span data-ttu-id="49501-170">업로드</span><span class="sxs-lookup"><span data-stu-id="49501-170">Upload</span></span>| <span data-ttu-id="49501-171">아니요</span><span class="sxs-lookup"><span data-stu-id="49501-171">No</span></span> |
| <span data-ttu-id="49501-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="49501-172">WriteBatchSize</span></span> | <span data-ttu-id="49501-173">WriteBatchSize hello 버퍼 크기에 이르면 hello Azure 검색 인덱스에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="49501-174">Hello 참조 [WriteBatchSize 속성](#writebatchsize-property) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="49501-175">too1이 1, 000입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-175">1 too1,000.</span></span> <span data-ttu-id="49501-176">기본값은 1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-176">Default value is 1000.</span></span> | <span data-ttu-id="49501-177">아니요</span><span class="sxs-lookup"><span data-stu-id="49501-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="49501-178">WriteBehavior 속성</span><span class="sxs-lookup"><span data-stu-id="49501-178">WriteBehavior property</span></span>
<span data-ttu-id="49501-179">데이터를 쓸 때 AzureSearchSink가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="49501-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="49501-180">즉, 문서 키 hello hello Azure 검색 인덱스에 이미 있는 경우 문서를 작성, Azure 검색 충돌 예외를 throw 하지 않고 hello 기존 문서를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="49501-181">hello를 AzureSearchSink hello를 두 가지 upsert 동작 (AzureSearch SDK 사용)에서 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="49501-182">**병합**: hello 새 문서에서 모든 hello 열 하나 기존 hello로 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="49501-183">Hello 새 문서에 null 값을 가진 열에 대 한 기존 자동 압축 hello hello 값 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49501-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="49501-184">**업로드**: hello 새 문서 대체 hello 기존 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="49501-185">열의 hello 새 문서에 지정 되지 않은 경우 null이 아닌 값에에서 여부 hello 기존 문서 또는 not hello 값 toonull에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49501-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="49501-186">hello 기본 동작은 **병합**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="49501-187">writeBatchSize 속성</span><span class="sxs-lookup"><span data-stu-id="49501-187">WriteBatchSize Property</span></span>
<span data-ttu-id="49501-188">Azure Search 서비스는 일괄 처리로 문서 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="49501-189">일괄 처리 too1 1, 000 동작을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="49501-190">작업 한 문서 tooperform hello 업로드/병합 작업을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="49501-191">데이터 형식 지원</span><span class="sxs-lookup"><span data-stu-id="49501-191">Data type support</span></span>
<span data-ttu-id="49501-192">hello 다음 표에서 Azure 검색 데이터 형식을 지원 되는지 여부.</span><span class="sxs-lookup"><span data-stu-id="49501-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="49501-193">Azure Search 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="49501-193">Azure Search data type</span></span> | <span data-ttu-id="49501-194">Azure Search 싱크에서 지원됨</span><span class="sxs-lookup"><span data-stu-id="49501-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="49501-195">String</span><span class="sxs-lookup"><span data-stu-id="49501-195">String</span></span> | <span data-ttu-id="49501-196">Y</span><span class="sxs-lookup"><span data-stu-id="49501-196">Y</span></span> |
| <span data-ttu-id="49501-197">Int32</span><span class="sxs-lookup"><span data-stu-id="49501-197">Int32</span></span> | <span data-ttu-id="49501-198">Y</span><span class="sxs-lookup"><span data-stu-id="49501-198">Y</span></span> |
| <span data-ttu-id="49501-199">Int64</span><span class="sxs-lookup"><span data-stu-id="49501-199">Int64</span></span> | <span data-ttu-id="49501-200">Y</span><span class="sxs-lookup"><span data-stu-id="49501-200">Y</span></span> |
| <span data-ttu-id="49501-201">Double</span><span class="sxs-lookup"><span data-stu-id="49501-201">Double</span></span> | <span data-ttu-id="49501-202">Y</span><span class="sxs-lookup"><span data-stu-id="49501-202">Y</span></span> |
| <span data-ttu-id="49501-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="49501-203">Boolean</span></span> | <span data-ttu-id="49501-204">Y</span><span class="sxs-lookup"><span data-stu-id="49501-204">Y</span></span> |
| <span data-ttu-id="49501-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="49501-205">DataTimeOffset</span></span> | <span data-ttu-id="49501-206">Y</span><span class="sxs-lookup"><span data-stu-id="49501-206">Y</span></span> |
| <span data-ttu-id="49501-207">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="49501-207">String Array</span></span> | <span data-ttu-id="49501-208">N</span><span class="sxs-lookup"><span data-stu-id="49501-208">N</span></span> |
| <span data-ttu-id="49501-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="49501-209">GeographyPoint</span></span> | <span data-ttu-id="49501-210">N</span><span class="sxs-lookup"><span data-stu-id="49501-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="49501-211">JSON의 예: 온-프레미스 SQL Server tooAzure 검색 인덱스에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="49501-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="49501-212">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="49501-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="49501-213">[AzureSearch](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="49501-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="49501-214">[OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="49501-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="49501-215">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="49501-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="49501-216">[AzureSearchIndex](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="49501-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="49501-217">[SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 및 [AzureSearchIndexSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="49501-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="49501-218">hello 샘플 시계열 데이터에서에서 복사 온-프레미스 SQL Server 데이터베이스 tooan Azure 검색 인덱스 매시간 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="49501-219">이 샘플에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="49501-220">첫 번째 단계로, 온-프레미스 컴퓨터에 hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="49501-221">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="49501-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="49501-222">**Azure Search 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="49501-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="49501-223">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="49501-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="49501-224">**SQL Server 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="49501-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="49501-225">hello 샘플 테이블 "MyTable" SQL Server에서 만들고 시계열 데이터에 대 한 "timestampcolumn" 라는 열이 포함 된 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="49501-226">TableName typeProperty hello 데이터 집합의 단일 데이터 집합 이지만 단일 테이블을 사용 하 여 동일한 데이터베이스를 사용 해야 하는 hello 내에서 여러 테이블에 대해 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="49501-227">설정 "외부": "true" 알리고 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="49501-228">**Azure Search 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="49501-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="49501-229">명명 된 hello 샘플 복사본 데이터 tooan Azure 검색 인덱스 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="49501-230">데이터 팩터리 hello 인덱스가 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="49501-231">tootest hello 샘플,이 이름을 가진 인덱스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="49501-232">Hello로 hello Azure 검색 인덱스를 만들 hello 입력된 데이터 집합에서와 같이 열 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="49501-233">새 항목을 1 시간 마다 toohello Azure 검색 인덱스를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49501-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="49501-234">**SQL 원본 및 Azure Search 인덱스 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="49501-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="49501-235">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="49501-236">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**AzureSearchIndexSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="49501-237">hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="49501-238">클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="49501-239">hello 다음 JSON 코드 조각은 hello 변경 사항이 표시 복사 작업에서 필요한 `typeProperties` 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="49501-240">지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="49501-241">클라우드 원본에서 복사</span><span class="sxs-lookup"><span data-stu-id="49501-241">Copy from a cloud source</span></span>
<span data-ttu-id="49501-242">클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="49501-243">hello 다음 JSON 코드 조각은 hello 변경 사항이 표시 복사 작업에서 필요한 `typeProperties` 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="49501-244">지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49501-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="49501-245">원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49501-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="49501-246">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49501-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="49501-247">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="49501-247">Performance and tuning</span></span>  
<span data-ttu-id="49501-248">Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 데이터 이동 (복사 작업)의 성능에는 영향 및 다양 한 방법으로 toooptimize 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="49501-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49501-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49501-249">Next steps</span></span>
<span data-ttu-id="49501-250">Hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="49501-250">See hello following articles:</span></span>

* <span data-ttu-id="49501-251">[복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="49501-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
