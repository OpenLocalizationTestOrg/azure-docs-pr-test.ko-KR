---
title: "OData 원본에서 데이터 aaaMove | Microsoft Docs"
description: "Odata에서 toomove 데이터 원본 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="722fe-103">Azure Data Factory를 사용하여 OData 소스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="722fe-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="722fe-104">이 문서에서는 toouse OData 원본에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="722fe-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="722fe-106">OData 소스 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="722fe-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="722fe-108">데이터 팩터리의 현재만 지 원하는 데이터를 OData 소스 tooother 데이터에서에서 저장 하지 않은 이동 tooan OData 원본 저장소 다른 데이터에서 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="722fe-109">지원되는 버전 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="722fe-109">Supported versions and authentication types</span></span>
<span data-ttu-id="722fe-110">이 OData 커넥터는 OData 버전 3.0 및 4.0을 지원하며, 클라우드 OData 소스와 온-프레미스 OData 소스에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="722fe-111">후자의 hello, tooinstall hello 데이터 관리 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="722fe-112">데이터 관리 게이트웨이에 대한 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="722fe-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="722fe-113">지원되는 인증 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="722fe-114">tooaccess **클라우드** OData 피드, 익명으로 사용할 수 있는데, 기본 (사용자 이름 및 암호) 또는 Azure Active Directory 기반 OAuth 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="722fe-115">tooaccess **온-프레미스** OData 피드, 익명으로 사용할 수 있습니다 (사용자 이름 및 암호) 기본 또는 Windows 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="722fe-116">시작</span><span class="sxs-lookup"><span data-stu-id="722fe-116">Getting started</span></span>
<span data-ttu-id="722fe-117">다른 도구/API를 사용하여 OData 소스의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="722fe-118">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="722fe-119">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="722fe-120">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="722fe-121">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="722fe-122">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="722fe-123">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="722fe-124">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="722fe-125">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="722fe-126">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="722fe-127">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="722fe-128">OData 원본에서 사용 되는 toocopy 데이터는 Data Factory 엔터티에 대 한 JSON 정의 가진 샘플을 보려면 [JSON의 예: OData 원본 tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-odata-source-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="722fe-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="722fe-129">사용 되는 toodefine Data Factory 엔터티에 특정 tooOData 소스는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="722fe-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="722fe-130">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="722fe-130">Linked Service properties</span></span>
<span data-ttu-id="722fe-131">다음 표에서 hello JSON 요소 특정 tooOData 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="722fe-132">속성</span><span class="sxs-lookup"><span data-stu-id="722fe-132">Property</span></span> | <span data-ttu-id="722fe-133">설명</span><span class="sxs-lookup"><span data-stu-id="722fe-133">Description</span></span> | <span data-ttu-id="722fe-134">필수</span><span class="sxs-lookup"><span data-stu-id="722fe-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="722fe-135">type</span><span class="sxs-lookup"><span data-stu-id="722fe-135">type</span></span> |<span data-ttu-id="722fe-136">hello type 속성 설정 해야 합니다: **OData**</span><span class="sxs-lookup"><span data-stu-id="722fe-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="722fe-137">예</span><span class="sxs-lookup"><span data-stu-id="722fe-137">Yes</span></span> |
| <span data-ttu-id="722fe-138">url</span><span class="sxs-lookup"><span data-stu-id="722fe-138">url</span></span> |<span data-ttu-id="722fe-139">Hello OData 서비스의 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-139">Url of hello OData service.</span></span> |<span data-ttu-id="722fe-140">예</span><span class="sxs-lookup"><span data-stu-id="722fe-140">Yes</span></span> |
| <span data-ttu-id="722fe-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="722fe-141">authenticationType</span></span> |<span data-ttu-id="722fe-142">Tooconnect toohello OData 원본을 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="722fe-143">클라우드 OData의 경우 가능한 값은 익명, 기본 및 OAuth입니다(Azure Data Factory는 현재 Azure Active Directory 기반 OAuth만 지원).</span><span class="sxs-lookup"><span data-stu-id="722fe-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="722fe-144">온-프레미스 OData의 경우 가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="722fe-145">예</span><span class="sxs-lookup"><span data-stu-id="722fe-145">Yes</span></span> |
| <span data-ttu-id="722fe-146">username</span><span class="sxs-lookup"><span data-stu-id="722fe-146">username</span></span> |<span data-ttu-id="722fe-147">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="722fe-148">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="722fe-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="722fe-149">암호</span><span class="sxs-lookup"><span data-stu-id="722fe-149">password</span></span> |<span data-ttu-id="722fe-150">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="722fe-151">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="722fe-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="722fe-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="722fe-152">authorizedCredential</span></span> |<span data-ttu-id="722fe-153">OAuth를 사용 하는 경우 클릭 **Authorize** hello 데이터 팩터리 복사 마법사 또는 편집기에서 단추 및이 속성의 hello 값 자동 생성 됩니다. 사용자의 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="722fe-154">예(OAuth 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="722fe-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="722fe-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="722fe-155">gatewayName</span></span> |<span data-ttu-id="722fe-156">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 OData 서비스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="722fe-157">온-프레미스 OData 소스의 데이터를 복사하는 경우에만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="722fe-158">아니요</span><span class="sxs-lookup"><span data-stu-id="722fe-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="722fe-159">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="722fe-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="722fe-160">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="722fe-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="722fe-161">온-프레미스 OData 소스에 액세스하는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="722fe-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="722fe-162">OAuth 인증을 사용하여 클라우드 OData 소스 액세스</span><span class="sxs-lookup"><span data-stu-id="722fe-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="722fe-163">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="722fe-163">Dataset properties</span></span>
<span data-ttu-id="722fe-164">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="722fe-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="722fe-165">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="722fe-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="722fe-166">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="722fe-167">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **ODataResource** hello 다음과 같은 속성에 (OData 데이터 집합 포함)</span><span class="sxs-lookup"><span data-stu-id="722fe-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="722fe-168">속성</span><span class="sxs-lookup"><span data-stu-id="722fe-168">Property</span></span> | <span data-ttu-id="722fe-169">설명</span><span class="sxs-lookup"><span data-stu-id="722fe-169">Description</span></span> | <span data-ttu-id="722fe-170">필수</span><span class="sxs-lookup"><span data-stu-id="722fe-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="722fe-171">path</span><span class="sxs-lookup"><span data-stu-id="722fe-171">path</span></span> |<span data-ttu-id="722fe-172">경로 toohello OData 리소스</span><span class="sxs-lookup"><span data-stu-id="722fe-172">Path toohello OData resource</span></span> |<span data-ttu-id="722fe-173">아니요</span><span class="sxs-lookup"><span data-stu-id="722fe-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="722fe-174">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="722fe-174">Copy activity properties</span></span>
<span data-ttu-id="722fe-175">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="722fe-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="722fe-176">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="722fe-177">속성 hello에 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 각 활동 유형에 다른 손 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="722fe-178">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="722fe-179">원본 유형의 경우 **RelationalSource** (OData 포함) 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="722fe-180">속성</span><span class="sxs-lookup"><span data-stu-id="722fe-180">Property</span></span> | <span data-ttu-id="722fe-181">설명</span><span class="sxs-lookup"><span data-stu-id="722fe-181">Description</span></span> | <span data-ttu-id="722fe-182">예</span><span class="sxs-lookup"><span data-stu-id="722fe-182">Example</span></span> | <span data-ttu-id="722fe-183">필수</span><span class="sxs-lookup"><span data-stu-id="722fe-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="722fe-184">쿼리</span><span class="sxs-lookup"><span data-stu-id="722fe-184">query</span></span> |<span data-ttu-id="722fe-185">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="722fe-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="722fe-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="722fe-187">아니요</span><span class="sxs-lookup"><span data-stu-id="722fe-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="722fe-188">OData에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="722fe-188">Type Mapping for OData</span></span>
<span data-ttu-id="722fe-189">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="722fe-190">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="722fe-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="722fe-191">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="722fe-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="722fe-192">OData에서 데이터를 이동할 때는 hello 다음 매핑은 사용 하는 OData 형식 too.NET 형식에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="722fe-193">OData 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="722fe-193">OData Data Type</span></span> | <span data-ttu-id="722fe-194">.NET 형식</span><span class="sxs-lookup"><span data-stu-id="722fe-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="722fe-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="722fe-195">Edm.Binary</span></span> |<span data-ttu-id="722fe-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="722fe-196">Byte[]</span></span> |
| <span data-ttu-id="722fe-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="722fe-197">Edm.Boolean</span></span> |<span data-ttu-id="722fe-198">Bool</span><span class="sxs-lookup"><span data-stu-id="722fe-198">Bool</span></span> |
| <span data-ttu-id="722fe-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="722fe-199">Edm.Byte</span></span> |<span data-ttu-id="722fe-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="722fe-200">Byte[]</span></span> |
| <span data-ttu-id="722fe-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="722fe-201">Edm.DateTime</span></span> |<span data-ttu-id="722fe-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="722fe-202">DateTime</span></span> |
| <span data-ttu-id="722fe-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="722fe-203">Edm.Decimal</span></span> |<span data-ttu-id="722fe-204">10진수</span><span class="sxs-lookup"><span data-stu-id="722fe-204">Decimal</span></span> |
| <span data-ttu-id="722fe-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="722fe-205">Edm.Double</span></span> |<span data-ttu-id="722fe-206">Double</span><span class="sxs-lookup"><span data-stu-id="722fe-206">Double</span></span> |
| <span data-ttu-id="722fe-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="722fe-207">Edm.Single</span></span> |<span data-ttu-id="722fe-208">Single</span><span class="sxs-lookup"><span data-stu-id="722fe-208">Single</span></span> |
| <span data-ttu-id="722fe-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="722fe-209">Edm.Guid</span></span> |<span data-ttu-id="722fe-210">Guid</span><span class="sxs-lookup"><span data-stu-id="722fe-210">Guid</span></span> |
| <span data-ttu-id="722fe-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="722fe-211">Edm.Int16</span></span> |<span data-ttu-id="722fe-212">Int16</span><span class="sxs-lookup"><span data-stu-id="722fe-212">Int16</span></span> |
| <span data-ttu-id="722fe-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="722fe-213">Edm.Int32</span></span> |<span data-ttu-id="722fe-214">Int32</span><span class="sxs-lookup"><span data-stu-id="722fe-214">Int32</span></span> |
| <span data-ttu-id="722fe-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="722fe-215">Edm.Int64</span></span> |<span data-ttu-id="722fe-216">Int64</span><span class="sxs-lookup"><span data-stu-id="722fe-216">Int64</span></span> |
| <span data-ttu-id="722fe-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="722fe-217">Edm.SByte</span></span> |<span data-ttu-id="722fe-218">Int16</span><span class="sxs-lookup"><span data-stu-id="722fe-218">Int16</span></span> |
| <span data-ttu-id="722fe-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="722fe-219">Edm.String</span></span> |<span data-ttu-id="722fe-220">문자열</span><span class="sxs-lookup"><span data-stu-id="722fe-220">String</span></span> |
| <span data-ttu-id="722fe-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="722fe-221">Edm.Time</span></span> |<span data-ttu-id="722fe-222">timespan</span><span class="sxs-lookup"><span data-stu-id="722fe-222">TimeSpan</span></span> |
| <span data-ttu-id="722fe-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="722fe-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="722fe-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="722fe-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="722fe-225">OData 복합 데이터 형식 예: 개체는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="722fe-226">JSON의 예: OData 원본 tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="722fe-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="722fe-227">이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="722fe-228">Odata에서 toocopy 데이터 tooan Azure Blob 저장소를 원본 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="722fe-229">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="722fe-230">hello 샘플 Data Factory 엔터티에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="722fe-231">[OData](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="722fe-232">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="722fe-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="722fe-233">[ODataResource](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="722fe-234">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="722fe-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="722fe-235">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="722fe-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="722fe-236">hello 샘플에서 Azure blob 1 시간 마다 OData 소스 tooan에 대 한 쿼리 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="722fe-237">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="722fe-238">**연결 된 서비스 OData:** 이 예제를 사용 하 여 hello 익명 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="722fe-239">사용할 수 있는 다른 유형의 인증은 [OData 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="722fe-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="722fe-240">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="722fe-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="722fe-241">**OData 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="722fe-241">**OData input dataset:**</span></span>

<span data-ttu-id="722fe-242">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="722fe-243">지정 **경로** hello 데이터 집합의 정의 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="722fe-244">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="722fe-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="722fe-245">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="722fe-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="722fe-246">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="722fe-247">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="722fe-248">**OData 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="722fe-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="722fe-249">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="722fe-250">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="722fe-251">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello OData 소스에서 hello 최신 (최신) 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="722fe-252">지정 **쿼리** hello 파이프라인 정의 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="722fe-253">hello **URL** 는 hello 데이터 팩터리 서비스 tooretrieve 데이터 사용 하 여: 연결 된 서비스 (필수) + (선택 사항) hello 데이터 집합에 지정 된 경로 hello + hello 파이프라인 (선택 사항)에서 쿼리 URL에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="722fe-254">OData에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="722fe-254">Type mapping for OData</span></span>
<span data-ttu-id="722fe-255">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 단계 2 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="722fe-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="722fe-256">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="722fe-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="722fe-257">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="722fe-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="722fe-258">OData 데이터 저장소에서 데이터를 이동할 때는 OData 데이터 형식이 매핑된 too.NET 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="722fe-259">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="722fe-259">Map source toosink columns</span></span>
<span data-ttu-id="722fe-260">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="722fe-261">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="722fe-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="722fe-262">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="722fe-263">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="722fe-264">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="722fe-265">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="722fe-266">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="722fe-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="722fe-267">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="722fe-267">Performance and Tuning</span></span>
<span data-ttu-id="722fe-268">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722fe-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
