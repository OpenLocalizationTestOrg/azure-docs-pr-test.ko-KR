---
title: "Data Factory를 사용하여 Salesforce에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Salesforce에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="40ca1-103">Azure Data Factory를 사용하여 Salesforce에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="40ca1-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="40ca1-104">이 문서에서는 Azure Data Factory의 복사 활동을 사용하여 Salesforce의 데이터를 [지원되는 원본 및 싱크](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블에 있는 싱크 열에 나열된 데이터 저장소에 복사하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="40ca1-105">이 문서는 복사 작업 및 지원되는 데이터 저장소 조합을 사용하여 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="40ca1-106">현재 Azure Data Factory는 Salesforce에서 [지원되는 싱크 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)로 데이터를 이동하도록 지원하며 다른 데이터 저장소에서 Salesforce로 데이터를 이동하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="40ca1-107">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="40ca1-107">Supported versions</span></span>
<span data-ttu-id="40ca1-108">이 커넥터는 Salesforce Developer Edition, Professional Edition, Enterprise Edition 또는 Unlimited Edition을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="40ca1-109">그리고 Salesforce 프로덕션, 샌드박스 및 사용자 지정 도메인에서 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ca1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="40ca1-110">Prerequisites</span></span>
* <span data-ttu-id="40ca1-111">API 권한을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-111">API permission must be enabled.</span></span> <span data-ttu-id="40ca1-112">[권한 집합에 따라 Salesforce에서 API 액세스를 사용하도록 설정하는 방법](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="40ca1-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="40ca1-113">Salesforce에서 온-프레미스 데이터 저장소로 데이터를 복사하려면 온-프레미스 환경에 데이터 관리 게이트웨이 2.0이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="40ca1-114">Salesforce 요청 제한</span><span class="sxs-lookup"><span data-stu-id="40ca1-114">Salesforce request limits</span></span>
<span data-ttu-id="40ca1-115">Salesforce에는 총 API 요청 수와 동시 API 요청 수에 대한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="40ca1-116">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-116">Note the following points:</span></span>

- <span data-ttu-id="40ca1-117">동시 요청 수가 이 제한을 초과하면 제한이 발생하며 임의 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="40ca1-118">총 요청 수가 이 제한을 초과하면 Salesforce 계정은 24시간 동안 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="40ca1-119">두 시나리오 모두에서 "REQUEST_LIMIT_EXCEEDED" 오류가 나타날 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="40ca1-120">자세한 내용은 [Salesforce 개발자 제한](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) 문서의 “API 요청 제한” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="40ca1-121">시작</span><span class="sxs-lookup"><span data-stu-id="40ca1-121">Getting started</span></span>
<span data-ttu-id="40ca1-122">다른 도구/API를 사용하여 Salesforce의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="40ca1-123">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="40ca1-124">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="40ca1-125">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="40ca1-126">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="40ca1-127">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="40ca1-128">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="40ca1-129">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="40ca1-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="40ca1-131">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="40ca1-132">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="40ca1-133">Salesforce의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예: Salesforce에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-salesforce-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="40ca1-134">다음 섹션에서는 Salesforce에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="40ca1-135">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-135">Linked service properties</span></span>
<span data-ttu-id="40ca1-136">다음 테이블에서는 Salesforce 연결된 서비스에 지정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="40ca1-137">속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-137">Property</span></span> | <span data-ttu-id="40ca1-138">설명</span><span class="sxs-lookup"><span data-stu-id="40ca1-138">Description</span></span> | <span data-ttu-id="40ca1-139">필수</span><span class="sxs-lookup"><span data-stu-id="40ca1-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40ca1-140">type</span><span class="sxs-lookup"><span data-stu-id="40ca1-140">type</span></span> |<span data-ttu-id="40ca1-141">형식 속성은 **Salesforce**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="40ca1-142">예</span><span class="sxs-lookup"><span data-stu-id="40ca1-142">Yes</span></span> |
| <span data-ttu-id="40ca1-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="40ca1-143">environmentUrl</span></span> | <span data-ttu-id="40ca1-144">Salesforce 인스턴스의 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="40ca1-145">-기본값은 " https://login.salesforce.com " 입니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="40ca1-146">-샌드박스에서 데이터를 복사하려면  " https://test.salesforce.com " 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="40ca1-147">-사용자 지정 도메인에서 데이터를 복사하려면 예를 들어 "https://[domain].my.salesforce.com"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="40ca1-148">아니요</span><span class="sxs-lookup"><span data-stu-id="40ca1-148">No</span></span> |
| <span data-ttu-id="40ca1-149">username</span><span class="sxs-lookup"><span data-stu-id="40ca1-149">username</span></span> |<span data-ttu-id="40ca1-150">사용자 계정의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="40ca1-151">예</span><span class="sxs-lookup"><span data-stu-id="40ca1-151">Yes</span></span> |
| <span data-ttu-id="40ca1-152">password</span><span class="sxs-lookup"><span data-stu-id="40ca1-152">password</span></span> |<span data-ttu-id="40ca1-153">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-153">Specify a password for the user account.</span></span> |<span data-ttu-id="40ca1-154">예</span><span class="sxs-lookup"><span data-stu-id="40ca1-154">Yes</span></span> |
| <span data-ttu-id="40ca1-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="40ca1-155">securityToken</span></span> |<span data-ttu-id="40ca1-156">사용자 계정에 대한 보안 토큰을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-156">Specify a security token for the user account.</span></span> <span data-ttu-id="40ca1-157">보안 토큰을 재설정하거나 가져오는 방법에 대한 자세한 내용은 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="40ca1-158">일반적인 보안 토큰에 대해 자세히 알아보려면 [보안 및 API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="40ca1-159">예</span><span class="sxs-lookup"><span data-stu-id="40ca1-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="40ca1-160">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-160">Dataset properties</span></span>
<span data-ttu-id="40ca1-161">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="40ca1-162">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="40ca1-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="40ca1-163">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="40ca1-164">**RelationalTable** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="40ca1-165">속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-165">Property</span></span> | <span data-ttu-id="40ca1-166">설명</span><span class="sxs-lookup"><span data-stu-id="40ca1-166">Description</span></span> | <span data-ttu-id="40ca1-167">필수</span><span class="sxs-lookup"><span data-stu-id="40ca1-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40ca1-168">tableName</span><span class="sxs-lookup"><span data-stu-id="40ca1-168">tableName</span></span> |<span data-ttu-id="40ca1-169">Salesforce에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="40ca1-170">아니요(**RelationalSource**의 **query**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="40ca1-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="40ca1-171">모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="40ca1-173">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-173">Copy activity properties</span></span>
<span data-ttu-id="40ca1-174">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="40ca1-175">이름, 설명, 입력과 출력 테이블 및 다양한 정책과 같은 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="40ca1-176">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="40ca1-177">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="40ca1-178">원본이 **RelationalSource** 형식인 복사 작업에서(Salesforce 포함) typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="40ca1-179">속성</span><span class="sxs-lookup"><span data-stu-id="40ca1-179">Property</span></span> | <span data-ttu-id="40ca1-180">설명</span><span class="sxs-lookup"><span data-stu-id="40ca1-180">Description</span></span> | <span data-ttu-id="40ca1-181">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="40ca1-181">Allowed values</span></span> | <span data-ttu-id="40ca1-182">필수</span><span class="sxs-lookup"><span data-stu-id="40ca1-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40ca1-183">쿼리</span><span class="sxs-lookup"><span data-stu-id="40ca1-183">query</span></span> |<span data-ttu-id="40ca1-184">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-184">Use the custom query to read data.</span></span> |<span data-ttu-id="40ca1-185">SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="40ca1-186">예제: `select * from MyTable__c`</span><span class="sxs-lookup"><span data-stu-id="40ca1-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="40ca1-187">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="40ca1-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="40ca1-188">모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="40ca1-190">쿼리 팁</span><span class="sxs-lookup"><span data-stu-id="40ca1-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="40ca1-191">DateTime 열에서 where 절을 사용하여 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="40ca1-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="40ca1-192">SOQL 또는 SQL 쿼리를 지정할 때 DateTime 형식 차이에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="40ca1-193">예:</span><span class="sxs-lookup"><span data-stu-id="40ca1-193">For example:</span></span>

* <span data-ttu-id="40ca1-194">**SOQL 샘플**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="40ca1-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="40ca1-195">**SQL 샘플**:</span><span class="sxs-lookup"><span data-stu-id="40ca1-195">**SQL sample**:</span></span>
    * <span data-ttu-id="40ca1-196">**복사 마법사를 사용하여 쿼리 지정:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="40ca1-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="40ca1-197">**JSON 편집을 사용하여 쿼리 지정(적절하게 문자 이스케이프):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="40ca1-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="40ca1-198">Salesforce 보고서에서 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="40ca1-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="40ca1-199">`{call "<report name>"}`과 같이 쿼리를 지정하여 Salesforce 보고서에서 데이터를 검색할 수 있으며 그 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="40ca1-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="40ca1-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="40ca1-201">Salesforce 휴지통에서 삭제된 레코드 검색</span><span class="sxs-lookup"><span data-stu-id="40ca1-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="40ca1-202">임시 삭제된 쿼리를 Salesforce 휴지통에서 쿼리하려면 쿼리에 **"IsDeleted = 1"**을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="40ca1-203">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-203">For example,</span></span>

* <span data-ttu-id="40ca1-204">삭제된 레코드만 쿼리하려면 "select * from MyTable__c **where IsDeleted= 1**"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="40ca1-205">기존 레코드와 삭제된 레코드를 포함하여 모든 레코드를 쿼리하려면 "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="40ca1-206">JSON 예: Salesforce에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="40ca1-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="40ca1-207">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공하며,</span><span class="sxs-lookup"><span data-stu-id="40ca1-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="40ca1-208">Salesforce에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="40ca1-209">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="40ca1-210">시나리오를 구현하도록 만들어야 하는 데이터 팩터리 아티팩트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="40ca1-211">목록 다음에 나오는 섹션에서는 이러한 단계에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="40ca1-212">[Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="40ca1-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="40ca1-213">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="40ca1-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="40ca1-214">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="40ca1-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="40ca1-215">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="40ca1-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="40ca1-216">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="40ca1-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="40ca1-217">**Salesforce 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="40ca1-217">**Salesforce linked service**</span></span>

<span data-ttu-id="40ca1-218">이 예제에서는 **Salesforce** 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="40ca1-219">이 연결된 서비스에서 지원하는 속성 목록은 [Salesforce 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="40ca1-220">보안 토큰을 재설정하거나 가져오는 방법에 대한 자세한 내용은 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="40ca1-221">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="40ca1-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="40ca1-222">**Salesforce 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="40ca1-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="40ca1-223">**external**을 **true**로 설정하면 데이터 집합이 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40ca1-224">모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="40ca1-226">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="40ca1-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="40ca1-227">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="40ca1-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="40ca1-228">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="40ca1-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="40ca1-229">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하며, 매시간 실행되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="40ca1-230">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="40ca1-231">RelationalSource에서 지원하는 속성 목록은 [RelationalSource 형식 속성](#copy-activity-properties) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="40ca1-232">모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ca1-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="40ca1-234">Salesforce에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="40ca1-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="40ca1-235">Salesforce 형식</span><span class="sxs-lookup"><span data-stu-id="40ca1-235">Salesforce type</span></span> | <span data-ttu-id="40ca1-236">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="40ca1-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="40ca1-237">자동 번호</span><span class="sxs-lookup"><span data-stu-id="40ca1-237">Auto Number</span></span> |<span data-ttu-id="40ca1-238">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-238">String</span></span> |
| <span data-ttu-id="40ca1-239">확인란</span><span class="sxs-lookup"><span data-stu-id="40ca1-239">Checkbox</span></span> |<span data-ttu-id="40ca1-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="40ca1-240">Boolean</span></span> |
| <span data-ttu-id="40ca1-241">통화</span><span class="sxs-lookup"><span data-stu-id="40ca1-241">Currency</span></span> |<span data-ttu-id="40ca1-242">Double</span><span class="sxs-lookup"><span data-stu-id="40ca1-242">Double</span></span> |
| <span data-ttu-id="40ca1-243">Date</span><span class="sxs-lookup"><span data-stu-id="40ca1-243">Date</span></span> |<span data-ttu-id="40ca1-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="40ca1-244">DateTime</span></span> |
| <span data-ttu-id="40ca1-245">날짜/시간</span><span class="sxs-lookup"><span data-stu-id="40ca1-245">Date/Time</span></span> |<span data-ttu-id="40ca1-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="40ca1-246">DateTime</span></span> |
| <span data-ttu-id="40ca1-247">Email</span><span class="sxs-lookup"><span data-stu-id="40ca1-247">Email</span></span> |<span data-ttu-id="40ca1-248">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-248">String</span></span> |
| <span data-ttu-id="40ca1-249">Id</span><span class="sxs-lookup"><span data-stu-id="40ca1-249">Id</span></span> |<span data-ttu-id="40ca1-250">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-250">String</span></span> |
| <span data-ttu-id="40ca1-251">관계 조회</span><span class="sxs-lookup"><span data-stu-id="40ca1-251">Lookup Relationship</span></span> |<span data-ttu-id="40ca1-252">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-252">String</span></span> |
| <span data-ttu-id="40ca1-253">다중 선택 선택 목록</span><span class="sxs-lookup"><span data-stu-id="40ca1-253">Multi-Select Picklist</span></span> |<span data-ttu-id="40ca1-254">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-254">String</span></span> |
| <span data-ttu-id="40ca1-255">Number</span><span class="sxs-lookup"><span data-stu-id="40ca1-255">Number</span></span> |<span data-ttu-id="40ca1-256">Double</span><span class="sxs-lookup"><span data-stu-id="40ca1-256">Double</span></span> |
| <span data-ttu-id="40ca1-257">백분율</span><span class="sxs-lookup"><span data-stu-id="40ca1-257">Percent</span></span> |<span data-ttu-id="40ca1-258">Double</span><span class="sxs-lookup"><span data-stu-id="40ca1-258">Double</span></span> |
| <span data-ttu-id="40ca1-259">Phone</span><span class="sxs-lookup"><span data-stu-id="40ca1-259">Phone</span></span> |<span data-ttu-id="40ca1-260">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-260">String</span></span> |
| <span data-ttu-id="40ca1-261">선택 목록</span><span class="sxs-lookup"><span data-stu-id="40ca1-261">Picklist</span></span> |<span data-ttu-id="40ca1-262">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-262">String</span></span> |
| <span data-ttu-id="40ca1-263">텍스트</span><span class="sxs-lookup"><span data-stu-id="40ca1-263">Text</span></span> |<span data-ttu-id="40ca1-264">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-264">String</span></span> |
| <span data-ttu-id="40ca1-265">텍스트 영역</span><span class="sxs-lookup"><span data-stu-id="40ca1-265">Text Area</span></span> |<span data-ttu-id="40ca1-266">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-266">String</span></span> |
| <span data-ttu-id="40ca1-267">텍스트 영역(Long)</span><span class="sxs-lookup"><span data-stu-id="40ca1-267">Text Area (Long)</span></span> |<span data-ttu-id="40ca1-268">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-268">String</span></span> |
| <span data-ttu-id="40ca1-269">텍스트 영역(Rich)</span><span class="sxs-lookup"><span data-stu-id="40ca1-269">Text Area (Rich)</span></span> |<span data-ttu-id="40ca1-270">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-270">String</span></span> |
| <span data-ttu-id="40ca1-271">텍스트(암호화됨)</span><span class="sxs-lookup"><span data-stu-id="40ca1-271">Text (Encrypted)</span></span> |<span data-ttu-id="40ca1-272">문자열</span><span class="sxs-lookup"><span data-stu-id="40ca1-272">String</span></span> |
| <span data-ttu-id="40ca1-273">URL</span><span class="sxs-lookup"><span data-stu-id="40ca1-273">URL</span></span> |<span data-ttu-id="40ca1-274">String</span><span class="sxs-lookup"><span data-stu-id="40ca1-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="40ca1-275">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="40ca1-276">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="40ca1-276">Performance and tuning</span></span>
<span data-ttu-id="40ca1-277">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ca1-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
