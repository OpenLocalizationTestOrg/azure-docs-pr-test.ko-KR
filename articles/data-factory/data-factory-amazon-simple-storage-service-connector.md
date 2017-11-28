---
title: "데이터 팩터리를 사용 하 여 Amazon 간단한 저장소 서비스에서 데이터를 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 toomove 데이터로 Amazon 간단한 저장소 서비스 (S3)."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="b19c1-103">Azure Data Factory를 사용하여 Amazon 단순 저장소 서비스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="b19c1-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="b19c1-104">이 문서에서는 어떻게 toouse hello 활동의 Azure Data Factory toomove 데이터에서에서 복사 Amazon 간단한 저장소 서비스 (S3).</span><span class="sxs-lookup"><span data-stu-id="b19c1-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="b19c1-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="b19c1-106">Amazon S3 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="b19c1-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b19c1-108">data Factory에는 현재만 Amazon S3 tooother 데이터 저장소에서 데이터를 이동 지원 하지만 tooAmazon S3 저장 다른 데이터에서 데이터를 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="b19c1-109">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="b19c1-109">Required permissions</span></span>
<span data-ttu-id="b19c1-110">Amazon s 3에서 toocopy 데이터 hello 다음 권한을 부여 받은 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="b19c1-111">Amazon S3 개체 작업에 대한 `s3:GetObject` 및 `s3:GetObjectVersion`.</span><span class="sxs-lookup"><span data-stu-id="b19c1-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="b19c1-112">Amazon S3 버킷 작업에 대한 `s3:ListBucket`.</span><span class="sxs-lookup"><span data-stu-id="b19c1-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="b19c1-113">Hello 데이터 팩터리 복사 마법사를 사용 하는 경우 `s3:ListAllMyBuckets` 은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="b19c1-114">Amazon S3 사용 권한의 전체 목록 hello에 대 한 세부 정보를 참조 하십시오. [정책에서 사용 권한 지정](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="b19c1-115">시작</span><span class="sxs-lookup"><span data-stu-id="b19c1-115">Getting started</span></span>
<span data-ttu-id="b19c1-116">다른 도구 또는 API를 사용하여 Amazon S3 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="b19c1-117">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b19c1-118">빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="b19c1-119">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b19c1-120">단계별 지침은 toocreate 복사 작업으로 파이프라인에 대 한 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="b19c1-121">도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b19c1-122">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b19c1-123">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="b19c1-124">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="b19c1-125">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b19c1-126">도구 또는 Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="b19c1-127">Data Factory 된 엔터티를 Amazon S3 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 hello [JSON의 예: Amazon S3 tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-amazon-s3-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b19c1-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="b19c1-128">복사 작업에 대해 지원되는 파일 및 압축 형식에 대한 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="b19c1-129">다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooAmazon S3는 JSON 속성에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b19c1-130">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-130">Linked service properties</span></span>
<span data-ttu-id="b19c1-131">연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="b19c1-132">형식의 연결 된 서비스를 만들면 **AwsAccessKey** toolink Amazon S3 데이터 tooyour 데이터 팩터리를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="b19c1-133">다음 표에서 hello에 대 한 설명 JSON 요소 특정 tooAmazon S3 (AwsAccessKey) 연결 된 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="b19c1-134">속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-134">Property</span></span> | <span data-ttu-id="b19c1-135">설명</span><span class="sxs-lookup"><span data-stu-id="b19c1-135">Description</span></span> | <span data-ttu-id="b19c1-136">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b19c1-136">Allowed values</span></span> | <span data-ttu-id="b19c1-137">필수</span><span class="sxs-lookup"><span data-stu-id="b19c1-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b19c1-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="b19c1-138">accessKeyID</span></span> |<span data-ttu-id="b19c1-139">Hello 비밀 선택 키의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-139">ID of hello secret access key.</span></span> |<span data-ttu-id="b19c1-140">string</span><span class="sxs-lookup"><span data-stu-id="b19c1-140">string</span></span> |<span data-ttu-id="b19c1-141">예</span><span class="sxs-lookup"><span data-stu-id="b19c1-141">Yes</span></span> |
| <span data-ttu-id="b19c1-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="b19c1-142">secretAccessKey</span></span> |<span data-ttu-id="b19c1-143">자체 hello 비밀 선택 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-143">hello secret access key itself.</span></span> |<span data-ttu-id="b19c1-144">암호화된 비밀 문자열</span><span class="sxs-lookup"><span data-stu-id="b19c1-144">Encrypted secret string</span></span> |<span data-ttu-id="b19c1-145">예</span><span class="sxs-lookup"><span data-stu-id="b19c1-145">Yes</span></span> |

<span data-ttu-id="b19c1-146">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="b19c1-147">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-147">Dataset properties</span></span>
<span data-ttu-id="b19c1-148">데이터 집합 toorepresent toospecify 입력 데이터 집합 hello type 속성 hello 데이터 집합의 Azure Blob 저장소에 너무**AmazonS3**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="b19c1-149">집합 hello **linkedServiceName** hello Amazon S3의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="b19c1-150">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="b19c1-151">구조, 가용성 및 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(예: SQL Database, Azure Blob, Azure 테이블).</span><span class="sxs-lookup"><span data-stu-id="b19c1-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="b19c1-152">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b19c1-153">hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **AmazonS3** hello 다음과 같은 속성에 (Amazon S3 hello 데이터 집합 포함):</span><span class="sxs-lookup"><span data-stu-id="b19c1-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="b19c1-154">속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-154">Property</span></span> | <span data-ttu-id="b19c1-155">설명</span><span class="sxs-lookup"><span data-stu-id="b19c1-155">Description</span></span> | <span data-ttu-id="b19c1-156">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b19c1-156">Allowed values</span></span> | <span data-ttu-id="b19c1-157">필수</span><span class="sxs-lookup"><span data-stu-id="b19c1-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b19c1-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="b19c1-158">bucketName</span></span> |<span data-ttu-id="b19c1-159">hello S3 버킷 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-159">hello S3 bucket name.</span></span> |<span data-ttu-id="b19c1-160">문자열</span><span class="sxs-lookup"><span data-stu-id="b19c1-160">String</span></span> |<span data-ttu-id="b19c1-161">예</span><span class="sxs-lookup"><span data-stu-id="b19c1-161">Yes</span></span> |
| <span data-ttu-id="b19c1-162">key</span><span class="sxs-lookup"><span data-stu-id="b19c1-162">key</span></span> |<span data-ttu-id="b19c1-163">S3 hello 개체 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-163">hello S3 object key.</span></span> |<span data-ttu-id="b19c1-164">문자열</span><span class="sxs-lookup"><span data-stu-id="b19c1-164">String</span></span> |<span data-ttu-id="b19c1-165">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-165">No</span></span> |
| <span data-ttu-id="b19c1-166">접두사</span><span class="sxs-lookup"><span data-stu-id="b19c1-166">prefix</span></span> |<span data-ttu-id="b19c1-167">Hello S3 개체 키에 대 한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="b19c1-168">이 접두사로 시작하는 키를 가진 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="b19c1-169">키가 비어 있을 때에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-169">Applies only when key is empty.</span></span> |<span data-ttu-id="b19c1-170">string</span><span class="sxs-lookup"><span data-stu-id="b19c1-170">String</span></span> |<span data-ttu-id="b19c1-171">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-171">No</span></span> |
| <span data-ttu-id="b19c1-172">버전</span><span class="sxs-lookup"><span data-stu-id="b19c1-172">version</span></span> |<span data-ttu-id="b19c1-173">S3 버전 관리를 사용 하는 경우 hello S3 개체의 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="b19c1-174">문자열</span><span class="sxs-lookup"><span data-stu-id="b19c1-174">String</span></span> |<span data-ttu-id="b19c1-175">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-175">No</span></span> |
| <span data-ttu-id="b19c1-176">format</span><span class="sxs-lookup"><span data-stu-id="b19c1-176">format</span></span> | <span data-ttu-id="b19c1-177">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b19c1-178">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="b19c1-179">자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션.</span><span class="sxs-lookup"><span data-stu-id="b19c1-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="b19c1-180">으로 toocopy 파일-파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의에서 skip hello 형식 섹션 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="b19c1-181">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-181">No</span></span> | |
| <span data-ttu-id="b19c1-182">압축</span><span class="sxs-lookup"><span data-stu-id="b19c1-182">compression</span></span> | <span data-ttu-id="b19c1-183">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="b19c1-184">지원 되는 hello 유형은: **GZip**, **Deflate**, **BZip2**, 및 **ZipDeflate**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b19c1-185">지원 되는 hello 수준은: **최적** 및 **fastest 이면**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b19c1-186">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b19c1-187">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="b19c1-188">**bucketName + 키** hello S3 개체, 여기서 버킷에 S3 개체에 대 한 hello 루트 컨테이너 하 고 키가 hello 전체 경로 toohello S3 개체의 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="b19c1-189">접두사를 사용한 샘플 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b19c1-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="b19c1-190">샘플 데이터 집합(버전 포함)</span><span class="sxs-lookup"><span data-stu-id="b19c1-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="b19c1-191">S3에 대한 동적 경로</span><span class="sxs-lookup"><span data-stu-id="b19c1-191">Dynamic paths for S3</span></span>
<span data-ttu-id="b19c1-192">hello 위의 샘플에서는 고정된 값 hello에 대 한 **키** 및 **bucketName** hello Amazon S3 데이터 집합의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="b19c1-193">SliceStart와 같은 시스템 변수를 사용하여 Data Factory가 런타임에 동적으로 이러한 속성을 계산하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="b19c1-194">작업을 수행할 수 동일 hello에 대 한 hello **접두사** Amazon S3 데이터 집합의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="b19c1-195">지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b19c1-196">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-196">Copy activity properties</span></span>
<span data-ttu-id="b19c1-197">작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b19c1-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="b19c1-198">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="b19c1-199">Hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="b19c1-200">Hello 복사 작업에 대 한 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="b19c1-201">Hello 복사 작업의 원본 유형의 경우 **FileSystemSource** (Amazon S3 포함), hello 다음 속성은 영어로 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="b19c1-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="b19c1-202">속성</span><span class="sxs-lookup"><span data-stu-id="b19c1-202">Property</span></span> | <span data-ttu-id="b19c1-203">설명</span><span class="sxs-lookup"><span data-stu-id="b19c1-203">Description</span></span> | <span data-ttu-id="b19c1-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b19c1-204">Allowed values</span></span> | <span data-ttu-id="b19c1-205">필수</span><span class="sxs-lookup"><span data-stu-id="b19c1-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b19c1-206">recursive</span><span class="sxs-lookup"><span data-stu-id="b19c1-206">recursive</span></span> |<span data-ttu-id="b19c1-207">Hello 디렉터리 개체 toorecursively 목록 S3 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="b19c1-208">True/False</span><span class="sxs-lookup"><span data-stu-id="b19c1-208">true/false</span></span> |<span data-ttu-id="b19c1-209">아니요</span><span class="sxs-lookup"><span data-stu-id="b19c1-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="b19c1-210">JSON의 예: Amazon S3 tooAzure Blob 저장소에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b19c1-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="b19c1-211">이 샘플은 어떻게 Amazon S3 tooan Azure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="b19c1-212">그러나 데이터 복사할 수 직접 너무[지원 되는 hello 싱크 중](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Data Factory에 hello 복사 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="b19c1-213">hello 예제 Data Factory 엔터티에 따라 hello에 대 한 JSON 정의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="b19c1-214">이러한 정의 toocreate Amazon S3 tooBlob 저장소에서 파이프라인 toocopy 데이터를 사용 하 여 hello를 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="b19c1-215">[AwsAccessKey](#linked-service-properties)형식의 연결된 서비스.</span><span class="sxs-lookup"><span data-stu-id="b19c1-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="b19c1-216">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b19c1-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="b19c1-217">[AmazonS3](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="b19c1-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="b19c1-218">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="b19c1-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="b19c1-219">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b19c1-220">hello 샘플 데이터 복사 Amazon S3 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="b19c1-221">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="b19c1-222">Amazon S3 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b19c1-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="b19c1-223">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b19c1-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="b19c1-224">Amazon S3 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b19c1-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="b19c1-225">설정 **"외부": true** 해당 hello 데이터 집합은 외부 toohello 데이터 팩터리 hello 데이터 팩터리 서비스에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="b19c1-226">이 속성 tootrue 하지 hello 파이프라인의 활동에 의해 생성 되는 입력된 데이터 집합에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b19c1-227">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b19c1-227">Azure Blob output dataset</span></span>

<span data-ttu-id="b19c1-228">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="b19c1-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b19c1-229">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b19c1-230">hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="b19c1-231">Amazon S3 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업</span><span class="sxs-lookup"><span data-stu-id="b19c1-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="b19c1-232">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="b19c1-233">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="b19c1-234">싱크 데이터 집합에서 원본 데이터 집합 toocolumns toomap 열 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b19c1-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b19c1-235">Next steps</span></span>
<span data-ttu-id="b19c1-236">Hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b19c1-236">See hello following articles:</span></span>

* <span data-ttu-id="b19c1-237">키에 대 한 toolearn Data Factory에서 데이터 이동을 (복사 작업) 및 다양 한 방법으로 toooptimize의 성능에 영향을 해당 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="b19c1-238">복사 작업을 사용 하 여 파이프라인 만들기에 대 한 단계별 지침은 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19c1-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
