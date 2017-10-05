---
title: "OData 소스에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 OData 소스에서 데이터를 이동하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="a5b05-103">Azure Data Factory를 사용하여 OData 소스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="a5b05-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="a5b05-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 OData 소스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="a5b05-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="a5b05-106">OData 소스에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="a5b05-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a5b05-108">현재 데이터 팩터리는 OData 소스에서 다른 데이터 저장소로의 데이터 이동만 지원하며, 다른 데이터 저장소에서 OData 소스로의 데이터 이동은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="a5b05-109">지원되는 버전 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="a5b05-109">Supported versions and authentication types</span></span>
<span data-ttu-id="a5b05-110">이 OData 커넥터는 OData 버전 3.0 및 4.0을 지원하며, 클라우드 OData 소스와 온-프레미스 OData 소스에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="a5b05-111">후자의 경우 데이터 관리 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="a5b05-112">데이터 관리 게이트웨이에 대한 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="a5b05-113">지원되는 인증 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="a5b05-114">**클라우드** OData 피드에 액세스하려면 익명, 기본(사용자 이름 및 암호) 또는 Azure Active Directory OAuth 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="a5b05-115">**온-프레미스** OData 피드에 액세스하려면 익명, 기본(사용자 이름 및 암호) 또는 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a5b05-116">시작</span><span class="sxs-lookup"><span data-stu-id="a5b05-116">Getting started</span></span>
<span data-ttu-id="a5b05-117">다른 도구/API를 사용하여 OData 소스의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="a5b05-118">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a5b05-119">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a5b05-120">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a5b05-121">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a5b05-122">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a5b05-123">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a5b05-124">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a5b05-125">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a5b05-126">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a5b05-127">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a5b05-128">OData 소스의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예: OData 소스에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-odata-source-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a5b05-129">다음 섹션에서는 OData 소스에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a5b05-130">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-130">Linked Service properties</span></span>
<span data-ttu-id="a5b05-131">다음 테이블은 OData 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="a5b05-132">속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-132">Property</span></span> | <span data-ttu-id="a5b05-133">설명</span><span class="sxs-lookup"><span data-stu-id="a5b05-133">Description</span></span> | <span data-ttu-id="a5b05-134">필수</span><span class="sxs-lookup"><span data-stu-id="a5b05-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5b05-135">type</span><span class="sxs-lookup"><span data-stu-id="a5b05-135">type</span></span> |<span data-ttu-id="a5b05-136">형식 속성은 **OData**</span><span class="sxs-lookup"><span data-stu-id="a5b05-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="a5b05-137">예</span><span class="sxs-lookup"><span data-stu-id="a5b05-137">Yes</span></span> |
| <span data-ttu-id="a5b05-138">URL</span><span class="sxs-lookup"><span data-stu-id="a5b05-138">url</span></span> |<span data-ttu-id="a5b05-139">OData 서비스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-139">Url of the OData service.</span></span> |<span data-ttu-id="a5b05-140">예</span><span class="sxs-lookup"><span data-stu-id="a5b05-140">Yes</span></span> |
| <span data-ttu-id="a5b05-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a5b05-141">authenticationType</span></span> |<span data-ttu-id="a5b05-142">OData 소스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="a5b05-143">클라우드 OData의 경우 가능한 값은 익명, 기본 및 OAuth입니다(Azure Data Factory는 현재 Azure Active Directory 기반 OAuth만 지원).</span><span class="sxs-lookup"><span data-stu-id="a5b05-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="a5b05-144">온-프레미스 OData의 경우 가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a5b05-145">예</span><span class="sxs-lookup"><span data-stu-id="a5b05-145">Yes</span></span> |
| <span data-ttu-id="a5b05-146">username</span><span class="sxs-lookup"><span data-stu-id="a5b05-146">username</span></span> |<span data-ttu-id="a5b05-147">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="a5b05-148">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="a5b05-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a5b05-149">password</span><span class="sxs-lookup"><span data-stu-id="a5b05-149">password</span></span> |<span data-ttu-id="a5b05-150">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="a5b05-151">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="a5b05-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="a5b05-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="a5b05-152">authorizedCredential</span></span> |<span data-ttu-id="a5b05-153">OAuth를 사용하는 경우 Data Factory Copy Wizard 또는 Editor에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 이 속성의 값이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="a5b05-154">예(OAuth 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="a5b05-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="a5b05-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a5b05-155">gatewayName</span></span> |<span data-ttu-id="a5b05-156">데이터 팩터리 서비스가 온-프레미스 OData 서비스에 연결하는 데 사용해야 하는 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="a5b05-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="a5b05-157">온-프레미스 OData 소스의 데이터를 복사하는 경우에만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="a5b05-158">아니요</span><span class="sxs-lookup"><span data-stu-id="a5b05-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="a5b05-159">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a5b05-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a5b05-160">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a5b05-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="a5b05-161">온-프레미스 OData 소스에 액세스하는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a5b05-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="a5b05-162">OAuth 인증을 사용하여 클라우드 OData 소스 액세스</span><span class="sxs-lookup"><span data-stu-id="a5b05-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a5b05-163">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-163">Dataset properties</span></span>
<span data-ttu-id="a5b05-164">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a5b05-165">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="a5b05-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a5b05-166">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a5b05-167">**ODataResource** 형식(OData 데이터 집합 포함)의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="a5b05-168">속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-168">Property</span></span> | <span data-ttu-id="a5b05-169">설명</span><span class="sxs-lookup"><span data-stu-id="a5b05-169">Description</span></span> | <span data-ttu-id="a5b05-170">필수</span><span class="sxs-lookup"><span data-stu-id="a5b05-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5b05-171">경로</span><span class="sxs-lookup"><span data-stu-id="a5b05-171">path</span></span> |<span data-ttu-id="a5b05-172">OData 리소스에 대한 경로</span><span class="sxs-lookup"><span data-stu-id="a5b05-172">Path to the OData resource</span></span> |<span data-ttu-id="a5b05-173">아니요</span><span class="sxs-lookup"><span data-stu-id="a5b05-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a5b05-174">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-174">Copy activity properties</span></span>
<span data-ttu-id="a5b05-175">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a5b05-176">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a5b05-177">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="a5b05-178">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a5b05-179">원본이 **RelationalSource** (OData 포함) 형식인 경우 typeProperties섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a5b05-180">속성</span><span class="sxs-lookup"><span data-stu-id="a5b05-180">Property</span></span> | <span data-ttu-id="a5b05-181">설명</span><span class="sxs-lookup"><span data-stu-id="a5b05-181">Description</span></span> | <span data-ttu-id="a5b05-182">예</span><span class="sxs-lookup"><span data-stu-id="a5b05-182">Example</span></span> | <span data-ttu-id="a5b05-183">필수</span><span class="sxs-lookup"><span data-stu-id="a5b05-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a5b05-184">쿼리</span><span class="sxs-lookup"><span data-stu-id="a5b05-184">query</span></span> |<span data-ttu-id="a5b05-185">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-185">Use the custom query to read data.</span></span> |<span data-ttu-id="a5b05-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="a5b05-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="a5b05-187">아니요</span><span class="sxs-lookup"><span data-stu-id="a5b05-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="a5b05-188">OData에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="a5b05-188">Type Mapping for OData</span></span>
<span data-ttu-id="a5b05-189">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="a5b05-190">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="a5b05-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a5b05-191">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="a5b05-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a5b05-192">OData의 데이터를 이동하는 경우 OData 형식에서 .NET 형식으로 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="a5b05-193">OData 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="a5b05-193">OData Data Type</span></span> | <span data-ttu-id="a5b05-194">.NET 형식</span><span class="sxs-lookup"><span data-stu-id="a5b05-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="a5b05-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="a5b05-195">Edm.Binary</span></span> |<span data-ttu-id="a5b05-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a5b05-196">Byte[]</span></span> |
| <span data-ttu-id="a5b05-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="a5b05-197">Edm.Boolean</span></span> |<span data-ttu-id="a5b05-198">Bool</span><span class="sxs-lookup"><span data-stu-id="a5b05-198">Bool</span></span> |
| <span data-ttu-id="a5b05-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="a5b05-199">Edm.Byte</span></span> |<span data-ttu-id="a5b05-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a5b05-200">Byte[]</span></span> |
| <span data-ttu-id="a5b05-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="a5b05-201">Edm.DateTime</span></span> |<span data-ttu-id="a5b05-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="a5b05-202">DateTime</span></span> |
| <span data-ttu-id="a5b05-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="a5b05-203">Edm.Decimal</span></span> |<span data-ttu-id="a5b05-204">10진수</span><span class="sxs-lookup"><span data-stu-id="a5b05-204">Decimal</span></span> |
| <span data-ttu-id="a5b05-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="a5b05-205">Edm.Double</span></span> |<span data-ttu-id="a5b05-206">Double</span><span class="sxs-lookup"><span data-stu-id="a5b05-206">Double</span></span> |
| <span data-ttu-id="a5b05-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="a5b05-207">Edm.Single</span></span> |<span data-ttu-id="a5b05-208">Single</span><span class="sxs-lookup"><span data-stu-id="a5b05-208">Single</span></span> |
| <span data-ttu-id="a5b05-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="a5b05-209">Edm.Guid</span></span> |<span data-ttu-id="a5b05-210">Guid</span><span class="sxs-lookup"><span data-stu-id="a5b05-210">Guid</span></span> |
| <span data-ttu-id="a5b05-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="a5b05-211">Edm.Int16</span></span> |<span data-ttu-id="a5b05-212">Int16</span><span class="sxs-lookup"><span data-stu-id="a5b05-212">Int16</span></span> |
| <span data-ttu-id="a5b05-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="a5b05-213">Edm.Int32</span></span> |<span data-ttu-id="a5b05-214">Int32</span><span class="sxs-lookup"><span data-stu-id="a5b05-214">Int32</span></span> |
| <span data-ttu-id="a5b05-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="a5b05-215">Edm.Int64</span></span> |<span data-ttu-id="a5b05-216">Int64</span><span class="sxs-lookup"><span data-stu-id="a5b05-216">Int64</span></span> |
| <span data-ttu-id="a5b05-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="a5b05-217">Edm.SByte</span></span> |<span data-ttu-id="a5b05-218">Int16</span><span class="sxs-lookup"><span data-stu-id="a5b05-218">Int16</span></span> |
| <span data-ttu-id="a5b05-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="a5b05-219">Edm.String</span></span> |<span data-ttu-id="a5b05-220">문자열</span><span class="sxs-lookup"><span data-stu-id="a5b05-220">String</span></span> |
| <span data-ttu-id="a5b05-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="a5b05-221">Edm.Time</span></span> |<span data-ttu-id="a5b05-222">timespan</span><span class="sxs-lookup"><span data-stu-id="a5b05-222">TimeSpan</span></span> |
| <span data-ttu-id="a5b05-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a5b05-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="a5b05-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a5b05-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="a5b05-225">OData 복합 데이터 형식 예: 개체는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="a5b05-226">JSON 예: OData 소스에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="a5b05-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="a5b05-227">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a5b05-228">이 샘플은 OData 소스에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="a5b05-229">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="a5b05-230">샘플에 포함된 Data Factory 엔터티는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="a5b05-231">[OData](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="a5b05-232">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a5b05-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a5b05-233">[ODataResource](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="a5b05-234">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="a5b05-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a5b05-235">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="a5b05-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a5b05-236">이 샘플은 OData 소스에 쿼리한 데이터를 매시간 Azure blob에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="a5b05-237">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a5b05-238">**OData 연결된 서비스:** 이 예제에서는 익명 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="a5b05-239">사용할 수 있는 다른 유형의 인증은 [OData 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="a5b05-240">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="a5b05-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="a5b05-241">**OData 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="a5b05-241">**OData input dataset:**</span></span>

<span data-ttu-id="a5b05-242">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="a5b05-243">데이터 집합 정의에서 **경로** 를 지정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="a5b05-244">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="a5b05-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a5b05-245">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="a5b05-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a5b05-246">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a5b05-247">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="a5b05-248">**OData 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="a5b05-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="a5b05-249">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a5b05-250">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a5b05-251">**query** 속성에 지정된 SQL 쿼리는 OData 소스에서 최신 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

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

<span data-ttu-id="a5b05-252">파이프라인 정의에서 **쿼리** 를 지정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="a5b05-253">데이터 팩터리 서비스에서 데이터를 검색하는 데 사용하는 **URL** 은 연결된 서비스에 지정된 URL(필수) + 데이터 집합에 지정된 경로(선택) + 파이프라인의 쿼리(선택)입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="a5b05-254">OData에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="a5b05-254">Type mapping for OData</span></span>
<span data-ttu-id="a5b05-255">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a5b05-256">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="a5b05-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a5b05-257">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="a5b05-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a5b05-258">OData 데이터 저장소에서 데이터를 이동할 때 OData 데이터 형식은 .NET 형식에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a5b05-259">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="a5b05-259">Map source to sink columns</span></span>
<span data-ttu-id="a5b05-260">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a5b05-261">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="a5b05-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="a5b05-262">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a5b05-263">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a5b05-264">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a5b05-265">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b05-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a5b05-266">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a5b05-267">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="a5b05-267">Performance and Tuning</span></span>
<span data-ttu-id="a5b05-268">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5b05-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
