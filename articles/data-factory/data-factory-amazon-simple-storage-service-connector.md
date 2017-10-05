---
title: "Data Factory를 사용하여 Amazon 단순 저장소 서비스에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Amazon 단순 저장소 서비스(S3)에서 데이터를 이동하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="4238c-103">Azure Data Factory를 사용하여 Amazon 단순 저장소 서비스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="4238c-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="4238c-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Amazon Simple Storage Service(S3)에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="4238c-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="4238c-106">Amazon S3에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="4238c-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4238c-108">현재 Data Factory는 Amazon S3에서 다른 데이터 저장소로의 데이터 이동 만을 지원하지만, 다른 데이터 저장소에서 Amazon S3로 데이터 이동은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="4238c-109">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="4238c-109">Required permissions</span></span>
<span data-ttu-id="4238c-110">Amazon S3에서 데이터를 복사하려면 다음과 같은 권한이 부여되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="4238c-111">Amazon S3 개체 작업에 대한 `s3:GetObject` 및 `s3:GetObjectVersion`.</span><span class="sxs-lookup"><span data-stu-id="4238c-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="4238c-112">Amazon S3 버킷 작업에 대한 `s3:ListBucket`.</span><span class="sxs-lookup"><span data-stu-id="4238c-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="4238c-113">Data Factory 복사 마법사를 사용하는 경우 `s3:ListAllMyBuckets`도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="4238c-114">Amazon S3 사용 권한의 전체 목록은 [정책에서 사용 권한 지정](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="4238c-115">시작</span><span class="sxs-lookup"><span data-stu-id="4238c-115">Getting started</span></span>
<span data-ttu-id="4238c-116">다른 도구 또는 API를 사용하여 Amazon S3 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="4238c-117">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4238c-118">빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="4238c-119">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4238c-120">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="4238c-121">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="4238c-122">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="4238c-123">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="4238c-124">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="4238c-125">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4238c-126">도구 또는 API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="4238c-127">Amazon S3 데이터 저장소의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: Amazon S3에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-amazon-s3-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4238c-128">복사 작업에 대해 지원되는 파일 및 압축 형식에 대한 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="4238c-129">다음 섹션에서는 Amazon S3에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4238c-130">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="4238c-130">Linked service properties</span></span>
<span data-ttu-id="4238c-131">연결된 서비스는 데이터 저장소를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="4238c-132">Amazon S3 데이터 저장소를 데이터 팩터리에 연결하는 **AwsAccessKey** 형식의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="4238c-133">다음 표는 Amazon S3(AwsAccessKey) 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="4238c-134">속성</span><span class="sxs-lookup"><span data-stu-id="4238c-134">Property</span></span> | <span data-ttu-id="4238c-135">설명</span><span class="sxs-lookup"><span data-stu-id="4238c-135">Description</span></span> | <span data-ttu-id="4238c-136">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="4238c-136">Allowed values</span></span> | <span data-ttu-id="4238c-137">필수</span><span class="sxs-lookup"><span data-stu-id="4238c-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4238c-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="4238c-138">accessKeyID</span></span> |<span data-ttu-id="4238c-139">비밀 액세스 키의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-139">ID of the secret access key.</span></span> |<span data-ttu-id="4238c-140">string</span><span class="sxs-lookup"><span data-stu-id="4238c-140">string</span></span> |<span data-ttu-id="4238c-141">예</span><span class="sxs-lookup"><span data-stu-id="4238c-141">Yes</span></span> |
| <span data-ttu-id="4238c-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="4238c-142">secretAccessKey</span></span> |<span data-ttu-id="4238c-143">비밀 액세스 키 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-143">The secret access key itself.</span></span> |<span data-ttu-id="4238c-144">암호화된 비밀 문자열</span><span class="sxs-lookup"><span data-stu-id="4238c-144">Encrypted secret string</span></span> |<span data-ttu-id="4238c-145">예</span><span class="sxs-lookup"><span data-stu-id="4238c-145">Yes</span></span> |

<span data-ttu-id="4238c-146">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="4238c-147">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="4238c-147">Dataset properties</span></span>
<span data-ttu-id="4238c-148">Azure Blob Storage에서 입력 데이터를 표시할 데이터 집합을 지정하려면 데이터 집합의 형식 속성을 **AmazonS3**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="4238c-149">데이터 집합의 **linkedServiceName** 속성을 Amazon S3 연결된 서비스의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="4238c-150">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="4238c-151">구조, 가용성 및 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(예: SQL Database, Azure Blob, Azure 테이블).</span><span class="sxs-lookup"><span data-stu-id="4238c-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="4238c-152">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="4238c-153">**AmazonS3** 형식(Amazon S3 데이터 집합을 포함)의 데이터 집합에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="4238c-154">속성</span><span class="sxs-lookup"><span data-stu-id="4238c-154">Property</span></span> | <span data-ttu-id="4238c-155">설명</span><span class="sxs-lookup"><span data-stu-id="4238c-155">Description</span></span> | <span data-ttu-id="4238c-156">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="4238c-156">Allowed values</span></span> | <span data-ttu-id="4238c-157">필수</span><span class="sxs-lookup"><span data-stu-id="4238c-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4238c-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="4238c-158">bucketName</span></span> |<span data-ttu-id="4238c-159">S3 버킷 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-159">The S3 bucket name.</span></span> |<span data-ttu-id="4238c-160">string</span><span class="sxs-lookup"><span data-stu-id="4238c-160">String</span></span> |<span data-ttu-id="4238c-161">예</span><span class="sxs-lookup"><span data-stu-id="4238c-161">Yes</span></span> |
| <span data-ttu-id="4238c-162">key</span><span class="sxs-lookup"><span data-stu-id="4238c-162">key</span></span> |<span data-ttu-id="4238c-163">S3 개체 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-163">The S3 object key.</span></span> |<span data-ttu-id="4238c-164">string</span><span class="sxs-lookup"><span data-stu-id="4238c-164">String</span></span> |<span data-ttu-id="4238c-165">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-165">No</span></span> |
| <span data-ttu-id="4238c-166">접두사</span><span class="sxs-lookup"><span data-stu-id="4238c-166">prefix</span></span> |<span data-ttu-id="4238c-167">S3 개체 키에 대한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="4238c-168">이 접두사로 시작하는 키를 가진 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="4238c-169">키가 비어 있을 때에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-169">Applies only when key is empty.</span></span> |<span data-ttu-id="4238c-170">string</span><span class="sxs-lookup"><span data-stu-id="4238c-170">String</span></span> |<span data-ttu-id="4238c-171">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-171">No</span></span> |
| <span data-ttu-id="4238c-172">버전</span><span class="sxs-lookup"><span data-stu-id="4238c-172">version</span></span> |<span data-ttu-id="4238c-173">S3 버전 관리를 사용하도록 설정하면 S3 개체의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="4238c-174">문자열</span><span class="sxs-lookup"><span data-stu-id="4238c-174">String</span></span> |<span data-ttu-id="4238c-175">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-175">No</span></span> |
| <span data-ttu-id="4238c-176">format</span><span class="sxs-lookup"><span data-stu-id="4238c-176">format</span></span> | <span data-ttu-id="4238c-177">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="4238c-178">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="4238c-179">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="4238c-180">파일 기반 저장소(이진 복사) 간에 파일을 있는 그대로 복사하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4238c-181">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-181">No</span></span> | |
| <span data-ttu-id="4238c-182">압축</span><span class="sxs-lookup"><span data-stu-id="4238c-182">compression</span></span> | <span data-ttu-id="4238c-183">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="4238c-184">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="4238c-185">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4238c-186">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4238c-187">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="4238c-188">**bucketName + 키**는 S3 개체의 위치를 지정합니다. 여기서 버킷은 S3 개체에 대한 루트 컨테이너이며 키는 S3 개체의 전체 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="4238c-189">접두사를 사용한 샘플 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4238c-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="4238c-190">샘플 데이터 집합(버전 포함)</span><span class="sxs-lookup"><span data-stu-id="4238c-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="4238c-191">S3에 대한 동적 경로</span><span class="sxs-lookup"><span data-stu-id="4238c-191">Dynamic paths for S3</span></span>
<span data-ttu-id="4238c-192">이전 샘플에서는 Amazon S3 데이터 집합의 **키** 및 **bucketName** 속성에 대해 고정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="4238c-193">SliceStart와 같은 시스템 변수를 사용하여 Data Factory가 런타임에 동적으로 이러한 속성을 계산하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="4238c-194">Amazon S3 데이터 집합의 **접두사** 속성에 대해서도 동일하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="4238c-195">지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="4238c-196">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="4238c-196">Copy activity properties</span></span>
<span data-ttu-id="4238c-197">작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="4238c-198">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="4238c-199">활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="4238c-200">복사 작업의 경우 속성은 원본 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="4238c-201">복사 작업의 원본이 **FileSystemSource** 형식인 경우(Amazon S3 포함) **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="4238c-202">속성</span><span class="sxs-lookup"><span data-stu-id="4238c-202">Property</span></span> | <span data-ttu-id="4238c-203">설명</span><span class="sxs-lookup"><span data-stu-id="4238c-203">Description</span></span> | <span data-ttu-id="4238c-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="4238c-204">Allowed values</span></span> | <span data-ttu-id="4238c-205">필수</span><span class="sxs-lookup"><span data-stu-id="4238c-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4238c-206">recursive</span><span class="sxs-lookup"><span data-stu-id="4238c-206">recursive</span></span> |<span data-ttu-id="4238c-207">S3 개체를 디렉터리 아래에 재귀적으로 나열할 것인지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="4238c-208">True/False</span><span class="sxs-lookup"><span data-stu-id="4238c-208">true/false</span></span> |<span data-ttu-id="4238c-209">아니요</span><span class="sxs-lookup"><span data-stu-id="4238c-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="4238c-210">JSON 예제: Amazon S3에서 Azure Blob Storage로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="4238c-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="4238c-211">이 샘플은 Amazon S3 데이터베이스에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="4238c-212">그러나 Data Factory의 복사 작업을 사용하여 [지원되는 싱크](data-factory-data-movement-activities.md#supported-data-stores-and-formats)로 직접 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="4238c-213">샘플은 다음 Data Factory 엔터티에 대한 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="4238c-214">이러한 정의에 따라 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 Amazon S3에서 Blob Storage로 데이터를 복사하는 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="4238c-215">[AwsAccessKey](#linked-service-properties)형식의 연결된 서비스.</span><span class="sxs-lookup"><span data-stu-id="4238c-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="4238c-216">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4238c-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4238c-217">[AmazonS3](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4238c-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="4238c-218">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4238c-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4238c-219">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4238c-220">샘플은 1시간마다 웹 테이블의 데이터를 Amazon S3으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="4238c-221">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="4238c-222">Amazon S3 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4238c-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="4238c-223">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4238c-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="4238c-224">Amazon S3 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4238c-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="4238c-225">**"external": true**로 설정하면 데이터 집합이 데이터 팩터리의 외부에 있다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="4238c-226">파이프라인에서의 작업에 의해 생성되지 않은 입력 데이터 집합에서 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="4238c-227">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4238c-227">Azure Blob output dataset</span></span>

<span data-ttu-id="4238c-228">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="4238c-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4238c-229">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4238c-230">폴더 경로는 시작 시간의 년, 월, 일 및 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="4238c-231">Amazon S3 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업</span><span class="sxs-lookup"><span data-stu-id="4238c-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="4238c-232">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="4238c-233">파이프라인 JSON 정의에서 **source** 형식은 **FileSystemSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4238c-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="4238c-234">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4238c-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4238c-235">Next steps</span></span>
<span data-ttu-id="4238c-236">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-236">See the following articles:</span></span>

* <span data-ttu-id="4238c-237">Data Factory에서 데이터 이동(복사 작업) 성능에 영향을 미치는 주요 요소 및 다양한 최적화 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="4238c-238">복사 작업이 포함된 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4238c-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
