---
title: "데이터 팩터리를 사용 하 여 Salesforce에서 aaaMove 데이터 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 Salesforce에서 toomove 데이터입니다."
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
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="c1241-103">Azure Data Factory를 사용하여 Salesforce에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="c1241-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="c1241-104">이 문서는 Azure 데이터 팩터리 toocopy 데이터 hello 싱크 열의 hello에 나열 된 Salesforce tooany 데이터 저장소에서 복사 작업을 사용 하는 방법을 간략하게 설명 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c1241-105">Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 복사 작업 및 지원 되는 데이터 저장소 조합이 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="c1241-106">Azure Data Factory에는 현재 너무 Salesforce 로부터 데이터를 이동만 지원[싱크 데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats), 하지만 다른 데이터 저장소 tooSalesforce에서 데이터 이동을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="c1241-107">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="c1241-107">Supported versions</span></span>
<span data-ttu-id="c1241-108">이 커넥터는 지원의 Salesforce 버전에 따라 hello: Developer Edition, Professional Edition, Enterprise Edition 또는 무제한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="c1241-109">그리고 Salesforce 프로덕션, 샌드박스 및 사용자 지정 도메인에서 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1241-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1241-110">Prerequisites</span></span>
* <span data-ttu-id="c1241-111">API 권한을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-111">API permission must be enabled.</span></span> <span data-ttu-id="c1241-112">[권한 집합에 따라 Salesforce에서 API 액세스를 사용하도록 설정하는 방법](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="c1241-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="c1241-113">Salesforce tooon 온-프레미스 데이터 저장소에서 데이터 toocopy 있어야 이상 데이터 관리 게이트웨이 2.0 온-프레미스 환경에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="c1241-114">Salesforce 요청 제한</span><span class="sxs-lookup"><span data-stu-id="c1241-114">Salesforce request limits</span></span>
<span data-ttu-id="c1241-115">Salesforce에는 총 API 요청 수와 동시 API 요청 수에 대한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="c1241-116">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="c1241-116">Note hello following points:</span></span>

- <span data-ttu-id="c1241-117">동시 요청 수가 hello hello 제한을 초과 하면 조절 작업이 발생 하 고 임의 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="c1241-118">Hello 제한 hello 총 요청 수를 초과 하면 hello Salesforce 계정 24 시간 동안 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="c1241-119">또한 두 시나리오 모두에서 hello "REQUEST_LIMIT_EXCEEDED" 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="c1241-120">Hello hello "API 요청 제한" 섹션을 참조 [Salesforce 개발자 제한](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) 을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c1241-121">시작</span><span class="sxs-lookup"><span data-stu-id="c1241-121">Getting started</span></span>
<span data-ttu-id="c1241-122">다른 도구/API를 사용하여 Salesforce의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="c1241-123">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c1241-124">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="c1241-125">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c1241-126">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c1241-127">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="c1241-128">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c1241-129">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c1241-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c1241-131">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c1241-132">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c1241-133">Salesforce에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 샘플을 보려면 [JSON의 예: Salesforce tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-salesforce-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="c1241-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c1241-134">다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooSalesforce는 JSON 속성에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c1241-135">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="c1241-135">Linked service properties</span></span>
<span data-ttu-id="c1241-136">다음 표에서 hello JSON 요소를 특정 toohello Salesforce 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="c1241-137">속성</span><span class="sxs-lookup"><span data-stu-id="c1241-137">Property</span></span> | <span data-ttu-id="c1241-138">설명</span><span class="sxs-lookup"><span data-stu-id="c1241-138">Description</span></span> | <span data-ttu-id="c1241-139">필수</span><span class="sxs-lookup"><span data-stu-id="c1241-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1241-140">type</span><span class="sxs-lookup"><span data-stu-id="c1241-140">type</span></span> |<span data-ttu-id="c1241-141">hello type 속성 설정 해야 합니다: **Salesforce**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="c1241-142">예</span><span class="sxs-lookup"><span data-stu-id="c1241-142">Yes</span></span> |
| <span data-ttu-id="c1241-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="c1241-143">environmentUrl</span></span> | <span data-ttu-id="c1241-144">Hello URL의 Salesforce 인스턴스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="c1241-145">-기본값은 " https://login.salesforce.com " 입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="c1241-146">-toocopy 데이터로 샌드박스 "https://test.salesforce.com"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="c1241-147">-사용자 지정 도메인에서 toocopy 데이터 지정, 예를 들어 "https://[domain].my.salesforce.com"입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="c1241-148">아니요</span><span class="sxs-lookup"><span data-stu-id="c1241-148">No</span></span> |
| <span data-ttu-id="c1241-149">username</span><span class="sxs-lookup"><span data-stu-id="c1241-149">username</span></span> |<span data-ttu-id="c1241-150">Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="c1241-151">예</span><span class="sxs-lookup"><span data-stu-id="c1241-151">Yes</span></span> |
| <span data-ttu-id="c1241-152">암호</span><span class="sxs-lookup"><span data-stu-id="c1241-152">password</span></span> |<span data-ttu-id="c1241-153">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="c1241-154">예</span><span class="sxs-lookup"><span data-stu-id="c1241-154">Yes</span></span> |
| <span data-ttu-id="c1241-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="c1241-155">securityToken</span></span> |<span data-ttu-id="c1241-156">Hello 사용자 계정에 대 한 보안 토큰을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="c1241-157">참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 방법에 대 한 보안 토큰 tooreset/get입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="c1241-158">보안 토큰에 대 한 toolearn 일반적으로 참조 [보안과 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="c1241-159">예</span><span class="sxs-lookup"><span data-stu-id="c1241-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c1241-160">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="c1241-160">Dataset properties</span></span>
<span data-ttu-id="c1241-161">섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c1241-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c1241-162">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="c1241-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="c1241-163">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c1241-164">hello typeProperties hello 형식의 데이터 집합에 대 한 섹션 **RelationalTable** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="c1241-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="c1241-165">속성</span><span class="sxs-lookup"><span data-stu-id="c1241-165">Property</span></span> | <span data-ttu-id="c1241-166">설명</span><span class="sxs-lookup"><span data-stu-id="c1241-166">Description</span></span> | <span data-ttu-id="c1241-167">필수</span><span class="sxs-lookup"><span data-stu-id="c1241-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1241-168">tableName</span><span class="sxs-lookup"><span data-stu-id="c1241-168">tableName</span></span> |<span data-ttu-id="c1241-169">Salesforce에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="c1241-170">아니요(**RelationalSource**의 **query**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="c1241-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c1241-171">모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="c1241-173">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="c1241-173">Copy activity properties</span></span>
<span data-ttu-id="c1241-174">섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c1241-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c1241-175">이름, 설명, 입력과 출력 테이블 및 다양한 정책과 같은 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="c1241-176">사용할 수 있는 hello 속성 hello hello에 hello 활동의 typeProperties 섹션 반면, 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="c1241-177">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c1241-178">Hello 소스 hello 유형인 경우 복사 활동에서 **RelationalSource** (Salesforce 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="c1241-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c1241-179">속성</span><span class="sxs-lookup"><span data-stu-id="c1241-179">Property</span></span> | <span data-ttu-id="c1241-180">설명</span><span class="sxs-lookup"><span data-stu-id="c1241-180">Description</span></span> | <span data-ttu-id="c1241-181">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="c1241-181">Allowed values</span></span> | <span data-ttu-id="c1241-182">필수</span><span class="sxs-lookup"><span data-stu-id="c1241-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c1241-183">쿼리</span><span class="sxs-lookup"><span data-stu-id="c1241-183">query</span></span> |<span data-ttu-id="c1241-184">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="c1241-185">SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="c1241-186">예제: `select * from MyTable__c`</span><span class="sxs-lookup"><span data-stu-id="c1241-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="c1241-187">더 (경우 hello **tableName** 의 hello **dataset** 지정)</span><span class="sxs-lookup"><span data-stu-id="c1241-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c1241-188">모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="c1241-190">쿼리 팁</span><span class="sxs-lookup"><span data-stu-id="c1241-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="c1241-191">DateTime 열에서 where 절을 사용하여 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="c1241-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="c1241-192">때 hello SOQL 또는 SQL 쿼리, 사용량 기준 과금 주의 toohello 날짜/시간 형식 차이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="c1241-193">예:</span><span class="sxs-lookup"><span data-stu-id="c1241-193">For example:</span></span>

* <span data-ttu-id="c1241-194">**SOQL 샘플**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c1241-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="c1241-195">**SQL 샘플**:</span><span class="sxs-lookup"><span data-stu-id="c1241-195">**SQL sample**:</span></span>
    * <span data-ttu-id="c1241-196">**복사 마법사 toospecify hello 쿼리를 사용 하 여:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c1241-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="c1241-197">**Toospecify hello 쿼리를 편집 하는 JSON을 사용 하 여 (이스케이프 문자 제대로):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c1241-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="c1241-198">Salesforce 보고서에서 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="c1241-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="c1241-199">`{call "<report name>"}`과 같이 쿼리를 지정하여 Salesforce 보고서에서 데이터를 검색할 수 있으며 그 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="c1241-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="c1241-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="c1241-201">Salesforce 휴지통에서 삭제된 레코드 검색</span><span class="sxs-lookup"><span data-stu-id="c1241-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="c1241-202">Salesforce 휴지통에서 tooquery hello 소프트 삭제 된 레코드를 지정할 수 있습니다 **"IsDeleted = 1"** 쿼리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="c1241-203">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-203">For example,</span></span>

* <span data-ttu-id="c1241-204">유일한 hello 삭제 레코드 tooquery 지정 "선택 * MyTable__c에서 **여기서 IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="c1241-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="c1241-205">모든 기존 hello 및 hello 삭제를 비롯 한 레코드를 hello tooquery 지정 "선택 * MyTable__c에서 **여기서 IsDeleted = 0 또는 IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="c1241-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="c1241-206">JSON의 예: Salesforce tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="c1241-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="c1241-207">hello 다음 예에서는 샘플 JSON 정의 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c1241-208">표시 방법을 Salesforce tooAzure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="c1241-209">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="c1241-210">다음은 hello 데이터 팩터리 아티팩트의 toocreate tooimplement hello 시나리오 필요가 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="c1241-211">hello 목록 다음에 나오는 hello 섹션에서는 이러한 단계에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="c1241-212">Hello 형식의 연결 된 서비스 [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c1241-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="c1241-213">Hello 형식의 연결 된 서비스 [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c1241-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c1241-214">입력 [dataset](data-factory-create-datasets.md) hello 형식의 [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c1241-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="c1241-215">출력 [dataset](data-factory-create-datasets.md) hello 형식의 [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c1241-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="c1241-216">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="c1241-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="c1241-217">**Salesforce 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="c1241-217">**Salesforce linked service**</span></span>

<span data-ttu-id="c1241-218">이 예에서는 hello **Salesforce** 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="c1241-219">Hello 참조 [Salesforce에 연결 된 서비스](#linked-service-properties) 이 연결 된 서비스에서 지원 되는 hello 속성에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="c1241-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="c1241-220">참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) tooreset/get 보안 토큰을 hello 하는 방법에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

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
<span data-ttu-id="c1241-221">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="c1241-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="c1241-222">**Salesforce 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="c1241-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="c1241-223">설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1241-224">모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="c1241-226">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="c1241-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="c1241-227">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="c1241-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="c1241-228">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="c1241-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="c1241-229">hello 파이프라인에 포함 된 구성 된 복사 작업 toouse hello 입력 및 출력 데이터 집합 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="c1241-230">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource**, 및 hello **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="c1241-231">참조 [RelationalSource 형식 속성](#copy-activity-properties) hello hello RelationalSource에서 지원 되는 속성 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="c1241-232">모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="c1241-234">Salesforce에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="c1241-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="c1241-235">Salesforce 형식</span><span class="sxs-lookup"><span data-stu-id="c1241-235">Salesforce type</span></span> | <span data-ttu-id="c1241-236">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="c1241-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="c1241-237">자동 번호</span><span class="sxs-lookup"><span data-stu-id="c1241-237">Auto Number</span></span> |<span data-ttu-id="c1241-238">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-238">String</span></span> |
| <span data-ttu-id="c1241-239">확인란</span><span class="sxs-lookup"><span data-stu-id="c1241-239">Checkbox</span></span> |<span data-ttu-id="c1241-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="c1241-240">Boolean</span></span> |
| <span data-ttu-id="c1241-241">통화</span><span class="sxs-lookup"><span data-stu-id="c1241-241">Currency</span></span> |<span data-ttu-id="c1241-242">Double</span><span class="sxs-lookup"><span data-stu-id="c1241-242">Double</span></span> |
| <span data-ttu-id="c1241-243">Date</span><span class="sxs-lookup"><span data-stu-id="c1241-243">Date</span></span> |<span data-ttu-id="c1241-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="c1241-244">DateTime</span></span> |
| <span data-ttu-id="c1241-245">날짜/시간</span><span class="sxs-lookup"><span data-stu-id="c1241-245">Date/Time</span></span> |<span data-ttu-id="c1241-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="c1241-246">DateTime</span></span> |
| <span data-ttu-id="c1241-247">Email</span><span class="sxs-lookup"><span data-stu-id="c1241-247">Email</span></span> |<span data-ttu-id="c1241-248">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-248">String</span></span> |
| <span data-ttu-id="c1241-249">Id</span><span class="sxs-lookup"><span data-stu-id="c1241-249">Id</span></span> |<span data-ttu-id="c1241-250">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-250">String</span></span> |
| <span data-ttu-id="c1241-251">관계 조회</span><span class="sxs-lookup"><span data-stu-id="c1241-251">Lookup Relationship</span></span> |<span data-ttu-id="c1241-252">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-252">String</span></span> |
| <span data-ttu-id="c1241-253">다중 선택 선택 목록</span><span class="sxs-lookup"><span data-stu-id="c1241-253">Multi-Select Picklist</span></span> |<span data-ttu-id="c1241-254">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-254">String</span></span> |
| <span data-ttu-id="c1241-255">Number</span><span class="sxs-lookup"><span data-stu-id="c1241-255">Number</span></span> |<span data-ttu-id="c1241-256">Double</span><span class="sxs-lookup"><span data-stu-id="c1241-256">Double</span></span> |
| <span data-ttu-id="c1241-257">백분율</span><span class="sxs-lookup"><span data-stu-id="c1241-257">Percent</span></span> |<span data-ttu-id="c1241-258">Double</span><span class="sxs-lookup"><span data-stu-id="c1241-258">Double</span></span> |
| <span data-ttu-id="c1241-259">Phone</span><span class="sxs-lookup"><span data-stu-id="c1241-259">Phone</span></span> |<span data-ttu-id="c1241-260">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-260">String</span></span> |
| <span data-ttu-id="c1241-261">선택 목록</span><span class="sxs-lookup"><span data-stu-id="c1241-261">Picklist</span></span> |<span data-ttu-id="c1241-262">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-262">String</span></span> |
| <span data-ttu-id="c1241-263">텍스트</span><span class="sxs-lookup"><span data-stu-id="c1241-263">Text</span></span> |<span data-ttu-id="c1241-264">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-264">String</span></span> |
| <span data-ttu-id="c1241-265">텍스트 영역</span><span class="sxs-lookup"><span data-stu-id="c1241-265">Text Area</span></span> |<span data-ttu-id="c1241-266">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-266">String</span></span> |
| <span data-ttu-id="c1241-267">텍스트 영역(Long)</span><span class="sxs-lookup"><span data-stu-id="c1241-267">Text Area (Long)</span></span> |<span data-ttu-id="c1241-268">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-268">String</span></span> |
| <span data-ttu-id="c1241-269">텍스트 영역(Rich)</span><span class="sxs-lookup"><span data-stu-id="c1241-269">Text Area (Rich)</span></span> |<span data-ttu-id="c1241-270">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-270">String</span></span> |
| <span data-ttu-id="c1241-271">텍스트(암호화됨)</span><span class="sxs-lookup"><span data-stu-id="c1241-271">Text (Encrypted)</span></span> |<span data-ttu-id="c1241-272">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-272">String</span></span> |
| <span data-ttu-id="c1241-273">URL</span><span class="sxs-lookup"><span data-stu-id="c1241-273">URL</span></span> |<span data-ttu-id="c1241-274">문자열</span><span class="sxs-lookup"><span data-stu-id="c1241-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="c1241-275">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="c1241-276">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="c1241-276">Performance and tuning</span></span>
<span data-ttu-id="c1241-277">Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 요소 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1241-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
