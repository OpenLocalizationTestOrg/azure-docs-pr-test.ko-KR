---
title: "데이터 팩터리를 사용하여 Search 인덱스에 데이터 푸시 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 Azure Search 인덱스에 데이터를 푸시하는 방법을 알아봅니다."
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
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="4b63b-103">Azure 데이터 팩터리를 사용하여 Azure Search 인덱스에 데이터 푸시</span><span class="sxs-lookup"><span data-stu-id="4b63b-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="4b63b-104">이 문서에서는 복사 작업을 사용하여 지원되는 원본 데이터 저장소에서 Azure Search 인덱스로 데이터를 푸시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="4b63b-105">지원되는 원본 데이터 저장소는 [지원되는 원본 및 싱크](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블의 원본 열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4b63b-106">이 문서는 복사 작업 및 지원되는 데이터 저장소 조합을 사용하여 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="4b63b-107">연결 사용</span><span class="sxs-lookup"><span data-stu-id="4b63b-107">Enabling connectivity</span></span>
<span data-ttu-id="4b63b-108">데이터 팩터리 서비스에서 온-프레미스 데이터 저장소에 연결하도록 허용하려면 온-프레미스 환경에 데이터 관리 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="4b63b-109">원본 데이터 저장소를 호스트하는 동일한 컴퓨터에 게이트웨이를 설치하거나, 데이터 저장소와의 리소스 경합을 방지하기 위해 별도의 컴퓨터에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="4b63b-110">데이터 관리 게이트웨이는 온-프레미스 데이터 원본을 클라우드 서비스에 안전하고 관리되는 방식으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="4b63b-111">데이터 관리 게이트웨이에 대한 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4b63b-112">시작</span><span class="sxs-lookup"><span data-stu-id="4b63b-112">Getting started</span></span>
<span data-ttu-id="4b63b-113">다른 도구/API를 사용하여 원본 데이터 저장소에서 Azure Search 인덱스로 데이터를 푸시하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="4b63b-114">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4b63b-115">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="4b63b-116">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4b63b-117">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4b63b-118">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="4b63b-119">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="4b63b-120">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="4b63b-121">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4b63b-122">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4b63b-123">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="4b63b-124">Azure Search 인덱스로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON 예: 온-프레미스 SQL Server에서 Azure Search 인덱스로 데이터 복사](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="4b63b-125">다음 섹션에서는 Azure Search 인덱스에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4b63b-126">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-126">Linked service properties</span></span>

<span data-ttu-id="4b63b-127">다음 표에는 Azure Search 연결된 서비스에 지정된 JSON 요소에 대한 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="4b63b-128">속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-128">Property</span></span> | <span data-ttu-id="4b63b-129">설명</span><span class="sxs-lookup"><span data-stu-id="4b63b-129">Description</span></span> | <span data-ttu-id="4b63b-130">필수</span><span class="sxs-lookup"><span data-stu-id="4b63b-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4b63b-131">type</span><span class="sxs-lookup"><span data-stu-id="4b63b-131">type</span></span> | <span data-ttu-id="4b63b-132">형식 속성은 **AzureSearch**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="4b63b-133">예</span><span class="sxs-lookup"><span data-stu-id="4b63b-133">Yes</span></span> |
| <span data-ttu-id="4b63b-134">URL</span><span class="sxs-lookup"><span data-stu-id="4b63b-134">url</span></span> | <span data-ttu-id="4b63b-135">Azure Search 서비스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="4b63b-136">예</span><span class="sxs-lookup"><span data-stu-id="4b63b-136">Yes</span></span> |
| <span data-ttu-id="4b63b-137">key</span><span class="sxs-lookup"><span data-stu-id="4b63b-137">key</span></span> | <span data-ttu-id="4b63b-138">Azure Search 서비스의 관리자 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="4b63b-139">예</span><span class="sxs-lookup"><span data-stu-id="4b63b-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4b63b-140">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-140">Dataset properties</span></span>

<span data-ttu-id="4b63b-141">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4b63b-142">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="4b63b-143">**typeProperties** 섹션은 데이터 집합의 각 형식마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="4b63b-144">**AzureSearchIndex** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="4b63b-145">속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-145">Property</span></span> | <span data-ttu-id="4b63b-146">설명</span><span class="sxs-lookup"><span data-stu-id="4b63b-146">Description</span></span> | <span data-ttu-id="4b63b-147">필수</span><span class="sxs-lookup"><span data-stu-id="4b63b-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4b63b-148">type</span><span class="sxs-lookup"><span data-stu-id="4b63b-148">type</span></span> | <span data-ttu-id="4b63b-149">형식 속성은 **AzureSearchIndex**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="4b63b-150">예</span><span class="sxs-lookup"><span data-stu-id="4b63b-150">Yes</span></span> |
| <span data-ttu-id="4b63b-151">indexName</span><span class="sxs-lookup"><span data-stu-id="4b63b-151">indexName</span></span> | <span data-ttu-id="4b63b-152">Azure 검색 인덱스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-152">Name of the Azure Search index.</span></span> <span data-ttu-id="4b63b-153">Data Factory는 인덱스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-153">Data Factory does not create the index.</span></span> <span data-ttu-id="4b63b-154">Azure Search에는 인덱스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="4b63b-155">예</span><span class="sxs-lookup"><span data-stu-id="4b63b-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="4b63b-156">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-156">Copy activity properties</span></span>
<span data-ttu-id="4b63b-157">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4b63b-158">이름, 설명, 입력/출력 테이블, 다양한 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="4b63b-159">반면 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="4b63b-160">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="4b63b-161">복사 작업의 경우 싱크가 **AzureSearchIndexSink** 형식이면 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4b63b-162">속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-162">Property</span></span> | <span data-ttu-id="4b63b-163">설명</span><span class="sxs-lookup"><span data-stu-id="4b63b-163">Description</span></span> | <span data-ttu-id="4b63b-164">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="4b63b-164">Allowed values</span></span> | <span data-ttu-id="4b63b-165">필수</span><span class="sxs-lookup"><span data-stu-id="4b63b-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="4b63b-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="4b63b-166">WriteBehavior</span></span> | <span data-ttu-id="4b63b-167">문서가 인덱스에 이미 있는 경우 병합할지 또는 바꿀지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="4b63b-168">[WriteBehavior 속성](#writebehavior-property)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="4b63b-169">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="4b63b-169">Merge (default)</span></span><br/><span data-ttu-id="4b63b-170">업로드</span><span class="sxs-lookup"><span data-stu-id="4b63b-170">Upload</span></span>| <span data-ttu-id="4b63b-171">아니요</span><span class="sxs-lookup"><span data-stu-id="4b63b-171">No</span></span> |
| <span data-ttu-id="4b63b-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="4b63b-172">WriteBatchSize</span></span> | <span data-ttu-id="4b63b-173">버퍼 크기가 writeBatchSize에 도달한 경우 Azure Search 인덱스에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="4b63b-174">자세한 내용은 [WriteBatchSize 속성](#writebatchsize-property)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="4b63b-175">1~1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-175">1 to 1,000.</span></span> <span data-ttu-id="4b63b-176">기본값은 1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-176">Default value is 1000.</span></span> | <span data-ttu-id="4b63b-177">아니요</span><span class="sxs-lookup"><span data-stu-id="4b63b-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="4b63b-178">WriteBehavior 속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-178">WriteBehavior property</span></span>
<span data-ttu-id="4b63b-179">데이터를 쓸 때 AzureSearchSink가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="4b63b-180">즉, 문서를 작성할 때 문서 키가 Azure Search 인덱스가 이미 있는 경우 Azure Search는 충돌 예외를 throw하지 않는 대신 기존 문서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="4b63b-181">AzureSearchSink는 AzureSearch SDK를 사용하여 다음 두 가지 삽입 동작을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="4b63b-182">**병합**: 새 문서의 모든 열을 기존 문서와 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="4b63b-183">새 문서에서 null 값을 가진 열의 경우 기존 문서의 값이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="4b63b-184">**업로드**: 새 문서가 기존 문서를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="4b63b-185">새 문서에 지정되지 않은 열의 경우 기본 문서에 null이 아닌 값이 있는지 여부에 상관없이 값이 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="4b63b-186">기본 동작은 **병합**입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="4b63b-187">writeBatchSize 속성</span><span class="sxs-lookup"><span data-stu-id="4b63b-187">WriteBatchSize Property</span></span>
<span data-ttu-id="4b63b-188">Azure Search 서비스는 일괄 처리로 문서 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="4b63b-189">일괄 처리는 1~1,000개의 동작을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="4b63b-190">하나의 동작에서 하나의 문서를 처리하여 업로드/병합 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="4b63b-191">데이터 형식 지원</span><span class="sxs-lookup"><span data-stu-id="4b63b-191">Data type support</span></span>
<span data-ttu-id="4b63b-192">다음 표에서는 Azure Search 데이터 형식이 지원되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="4b63b-193">Azure Search 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="4b63b-193">Azure Search data type</span></span> | <span data-ttu-id="4b63b-194">Azure Search 싱크에서 지원됨</span><span class="sxs-lookup"><span data-stu-id="4b63b-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="4b63b-195">String</span><span class="sxs-lookup"><span data-stu-id="4b63b-195">String</span></span> | <span data-ttu-id="4b63b-196">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-196">Y</span></span> |
| <span data-ttu-id="4b63b-197">Int32</span><span class="sxs-lookup"><span data-stu-id="4b63b-197">Int32</span></span> | <span data-ttu-id="4b63b-198">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-198">Y</span></span> |
| <span data-ttu-id="4b63b-199">Int64</span><span class="sxs-lookup"><span data-stu-id="4b63b-199">Int64</span></span> | <span data-ttu-id="4b63b-200">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-200">Y</span></span> |
| <span data-ttu-id="4b63b-201">Double</span><span class="sxs-lookup"><span data-stu-id="4b63b-201">Double</span></span> | <span data-ttu-id="4b63b-202">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-202">Y</span></span> |
| <span data-ttu-id="4b63b-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="4b63b-203">Boolean</span></span> | <span data-ttu-id="4b63b-204">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-204">Y</span></span> |
| <span data-ttu-id="4b63b-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4b63b-205">DataTimeOffset</span></span> | <span data-ttu-id="4b63b-206">Y</span><span class="sxs-lookup"><span data-stu-id="4b63b-206">Y</span></span> |
| <span data-ttu-id="4b63b-207">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="4b63b-207">String Array</span></span> | <span data-ttu-id="4b63b-208">N</span><span class="sxs-lookup"><span data-stu-id="4b63b-208">N</span></span> |
| <span data-ttu-id="4b63b-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="4b63b-209">GeographyPoint</span></span> | <span data-ttu-id="4b63b-210">N</span><span class="sxs-lookup"><span data-stu-id="4b63b-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="4b63b-211">JSON 예: 온-프레미스 SQL Server에서 Azure Search 인덱스로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="4b63b-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="4b63b-212">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-212">The following sample shows:</span></span>

1.  <span data-ttu-id="4b63b-213">[AzureSearch](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4b63b-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="4b63b-214">[OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4b63b-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="4b63b-215">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4b63b-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="4b63b-216">[AzureSearchIndex](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4b63b-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="4b63b-217">[SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 및 [AzureSearchIndexSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="4b63b-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="4b63b-218">이 샘플은 온-프레미스 SQL Server 데이터베이스에서 Azure 검색 인덱스로 1시간마다 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="4b63b-219">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="4b63b-220">첫 번째 단계로 온-프레미스 컴퓨터에서 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="4b63b-221">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="4b63b-222">**Azure Search 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="4b63b-223">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="4b63b-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="4b63b-224">**SQL Server 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="4b63b-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="4b63b-225">샘플은 Azure SQL에서 만든 "MyTable" 테이블에 시계열 데이터에 대한 "timestampcolumn"이라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="4b63b-226">단일 데이터 집합을 사용하여 동일한 데이터베이스 내 여러 테이블에 대해 쿼리를 실행할 수 있지만, 데이터 집합의 tableName typeProperty에 대해서는 단일 테이블이 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="4b63b-227">"external": "true"를 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="4b63b-228">**Azure Search 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="4b63b-229">이 샘플은 **products**라는 Azure 검색 인덱스에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="4b63b-230">Data Factory는 인덱스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-230">Data Factory does not create the index.</span></span> <span data-ttu-id="4b63b-231">이 샘플을 테스트하려면 이 이름의 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="4b63b-232">입력 데이터 집합과 동일한 개수의 열이 있는 Azure 검색 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="4b63b-233">새 항목은 1시간마다 Azure 검색 인덱스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-233">New entries are added to the Azure Search index every hour.</span></span>

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

<span data-ttu-id="4b63b-234">**SQL 원본 및 Azure Search 인덱스 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="4b63b-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="4b63b-235">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="4b63b-236">파이프라인 JSON 정의에서 **source** 형식은 **SqlSource**로 설정되고 **sink** 형식은 **AzureSearchIndexSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="4b63b-237">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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

<span data-ttu-id="4b63b-238">클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4b63b-239">다음 JSON 조각은 복사 작업 `typeProperties`에서 필요한 변경 내용을 예제로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4b63b-240">지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="4b63b-241">클라우드 원본에서 복사</span><span class="sxs-lookup"><span data-stu-id="4b63b-241">Copy from a cloud source</span></span>
<span data-ttu-id="4b63b-242">클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4b63b-243">다음 JSON 조각은 복사 작업 `typeProperties`에서 필요한 변경 내용을 예제로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4b63b-244">지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="4b63b-245">복사 작업 정의에서 원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b63b-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="4b63b-246">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4b63b-247">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="4b63b-247">Performance and tuning</span></span>  
<span data-ttu-id="4b63b-248">데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b63b-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b63b-249">Next steps</span></span>
<span data-ttu-id="4b63b-250">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b63b-250">See the following articles:</span></span>

* <span data-ttu-id="4b63b-251">[복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="4b63b-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
