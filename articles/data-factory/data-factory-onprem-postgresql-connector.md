---
title: "Azure Data Factory를 사용하여 PostgreSQL에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 PostgreSQL 데이터베이스에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: fd26f0d03f8b0b352a6544a81ad952d2e2a1b7a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="c269a-103">Azure 데이터 팩터리를 사용하여 PostgreSQL에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="c269a-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="c269a-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 PostgreSQL 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="c269a-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c269a-106">온-프레미스 PostgreSQL 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="c269a-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c269a-108">현재 데이터 팩터리는 다른 데이터 저장소에서 PostgreSQL 데이터베이스로 데이터 이동이 아닌 PostgreSQL 데이터베이스에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-108">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c269a-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c269a-109">prerequisites</span></span>

<span data-ttu-id="c269a-110">데이터 팩터리 서비스는 데이터 관리 게이트웨이를 사용하여 온-프레미스 PostgreSQL 원본에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="c269a-111">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="c269a-112">게이트웨이는 PostgreSQL 데이터베이스가 Azure IaaS VM에 호스팅되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="c269a-113">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 IaaS VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-113">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="c269a-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c269a-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="c269a-115">Supported versions and installation</span></span>
<span data-ttu-id="c269a-116">PostgreSQL 데이터베이스에 연결할 데이터 관리 게이트웨이의 경우 데이터 관리 게이트웨이와 동일한 시스템에 [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-116">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="c269a-117">PostgreSQL 버전 7.4 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c269a-118">시작</span><span class="sxs-lookup"><span data-stu-id="c269a-118">Getting started</span></span>
<span data-ttu-id="c269a-119">여러 도구/API를 사용하여 온-프레미스 PostgreSQL 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c269a-120">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c269a-121">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c269a-122">또한 다음 도구를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-122">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="c269a-123">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c269a-123">Azure portal</span></span>
    - <span data-ttu-id="c269a-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c269a-124">Visual Studio</span></span>
    - <span data-ttu-id="c269a-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c269a-125">Azure PowerShell</span></span>
    - <span data-ttu-id="c269a-126">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c269a-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="c269a-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="c269a-127">.NET API</span></span>
    - <span data-ttu-id="c269a-128">REST API</span><span class="sxs-lookup"><span data-stu-id="c269a-128">REST API</span></span>

     <span data-ttu-id="c269a-129">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c269a-130">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c269a-131">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c269a-132">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c269a-133">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c269a-134">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c269a-135">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c269a-136">온-프레미스 PostgreSQL의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: PostgreSQL에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-postgresql-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c269a-137">다음 섹션에서는 PostgreSQL 데이터 저장소에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c269a-138">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="c269a-138">Linked service properties</span></span>
<span data-ttu-id="c269a-139">다음 표에서는 PostgreSQL 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-139">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="c269a-140">속성</span><span class="sxs-lookup"><span data-stu-id="c269a-140">Property</span></span> | <span data-ttu-id="c269a-141">설명</span><span class="sxs-lookup"><span data-stu-id="c269a-141">Description</span></span> | <span data-ttu-id="c269a-142">필수</span><span class="sxs-lookup"><span data-stu-id="c269a-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c269a-143">type</span><span class="sxs-lookup"><span data-stu-id="c269a-143">type</span></span> |<span data-ttu-id="c269a-144">형식 속성은 **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="c269a-144">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="c269a-145">예</span><span class="sxs-lookup"><span data-stu-id="c269a-145">Yes</span></span> |
| <span data-ttu-id="c269a-146">server</span><span class="sxs-lookup"><span data-stu-id="c269a-146">server</span></span> |<span data-ttu-id="c269a-147">PostgreSQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-147">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="c269a-148">예</span><span class="sxs-lookup"><span data-stu-id="c269a-148">Yes</span></span> |
| <span data-ttu-id="c269a-149">database</span><span class="sxs-lookup"><span data-stu-id="c269a-149">database</span></span> |<span data-ttu-id="c269a-150">PostgreSQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-150">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="c269a-151">예</span><span class="sxs-lookup"><span data-stu-id="c269a-151">Yes</span></span> |
| <span data-ttu-id="c269a-152">schema</span><span class="sxs-lookup"><span data-stu-id="c269a-152">schema</span></span> |<span data-ttu-id="c269a-153">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-153">Name of the schema in the database.</span></span> <span data-ttu-id="c269a-154">schema 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-154">The schema name is case-sensitive.</span></span> |<span data-ttu-id="c269a-155">아니요</span><span class="sxs-lookup"><span data-stu-id="c269a-155">No</span></span> |
| <span data-ttu-id="c269a-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c269a-156">authenticationType</span></span> |<span data-ttu-id="c269a-157">PostgreSQL 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-157">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="c269a-158">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="c269a-159">예</span><span class="sxs-lookup"><span data-stu-id="c269a-159">Yes</span></span> |
| <span data-ttu-id="c269a-160">username</span><span class="sxs-lookup"><span data-stu-id="c269a-160">username</span></span> |<span data-ttu-id="c269a-161">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="c269a-162">아니요</span><span class="sxs-lookup"><span data-stu-id="c269a-162">No</span></span> |
| <span data-ttu-id="c269a-163">password</span><span class="sxs-lookup"><span data-stu-id="c269a-163">password</span></span> |<span data-ttu-id="c269a-164">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="c269a-165">아니요</span><span class="sxs-lookup"><span data-stu-id="c269a-165">No</span></span> |
| <span data-ttu-id="c269a-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c269a-166">gatewayName</span></span> |<span data-ttu-id="c269a-167">데이터 팩터리 서비스가 온-프레미스 PostgreSQL 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-167">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="c269a-168">예</span><span class="sxs-lookup"><span data-stu-id="c269a-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c269a-169">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="c269a-169">Dataset properties</span></span>
<span data-ttu-id="c269a-170">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c269a-171">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="c269a-172">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-172">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c269a-173">**RelationalTable** 형식의 데이터 집합(PostgreSQL 데이터 집합을 포함)에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-173">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="c269a-174">속성</span><span class="sxs-lookup"><span data-stu-id="c269a-174">Property</span></span> | <span data-ttu-id="c269a-175">설명</span><span class="sxs-lookup"><span data-stu-id="c269a-175">Description</span></span> | <span data-ttu-id="c269a-176">필수</span><span class="sxs-lookup"><span data-stu-id="c269a-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c269a-177">tableName</span><span class="sxs-lookup"><span data-stu-id="c269a-177">tableName</span></span> |<span data-ttu-id="c269a-178">연결된 서비스가 참조하는 PostgreSQL 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-178">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="c269a-179">tableName은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-179">The tableName is case-sensitive.</span></span> |<span data-ttu-id="c269a-180">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="c269a-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c269a-181">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="c269a-181">Copy activity properties</span></span>
<span data-ttu-id="c269a-182">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-182">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c269a-183">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c269a-184">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-184">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="c269a-185">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-185">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c269a-186">원본이 **RelationalSource**(PostgreSQL 포함) 형식인 경우 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-186">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c269a-187">속성</span><span class="sxs-lookup"><span data-stu-id="c269a-187">Property</span></span> | <span data-ttu-id="c269a-188">설명</span><span class="sxs-lookup"><span data-stu-id="c269a-188">Description</span></span> | <span data-ttu-id="c269a-189">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="c269a-189">Allowed values</span></span> | <span data-ttu-id="c269a-190">필수</span><span class="sxs-lookup"><span data-stu-id="c269a-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c269a-191">쿼리</span><span class="sxs-lookup"><span data-stu-id="c269a-191">query</span></span> |<span data-ttu-id="c269a-192">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-192">Use the custom query to read data.</span></span> |<span data-ttu-id="c269a-193">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="c269a-193">SQL query string.</span></span> <span data-ttu-id="c269a-194">예: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="c269a-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="c269a-195">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="c269a-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="c269a-196">스키마 및 테이블 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="c269a-197">쿼리에서 `""`(큰따옴표)로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-197">Enclose them in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="c269a-198">**예제:**</span><span class="sxs-lookup"><span data-stu-id="c269a-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="c269a-199">JSON 예: PostgreSQL에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="c269a-199">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="c269a-200">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c269a-201">이 샘플은 PostgreSQL 데이터베이스에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-201">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="c269a-202">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="c269a-203">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="c269a-204">데이터 팩터리를 만들기 위한 단계별 지침은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-204">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="c269a-205">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="c269a-206">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-206">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c269a-207">[OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c269a-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="c269a-208">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c269a-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c269a-209">[RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="c269a-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c269a-210">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="c269a-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c269a-211">[RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="c269a-211">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c269a-212">샘플은 PostgreSQL 데이터베이스의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-212">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="c269a-213">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-213">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c269a-214">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-214">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c269a-215">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-215">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c269a-216">**PostgreSQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="c269a-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="c269a-217">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="c269a-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="c269a-218">**PostgreSQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="c269a-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="c269a-219">샘플은 PostgreSQL에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestamp"라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-219">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="c269a-220">`"external": true` 설정을 사용하는 경우 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-220">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
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

<span data-ttu-id="c269a-221">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="c269a-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c269a-222">데이터는 매시간 새 blob에 기록됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c269a-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c269a-223">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-223">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c269a-224">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c269a-225">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="c269a-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="c269a-226">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="c269a-227">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c269a-228">**query** 속성에 지정된 SQL 쿼리는 PostgreSQL 데이터베이스의 public.usstates 테이블에서 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-228">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="c269a-229">PostgreSQL에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="c269a-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="c269a-230">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="c269a-231">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="c269a-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c269a-232">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="c269a-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c269a-233">PostgreSQL로 데이터를 이동하는 경우 PostgreSQL 형식에서 .NET 형식으로 이동에 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-233">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="c269a-234">PostgreSQL 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="c269a-234">PostgreSQL Database type</span></span> | <span data-ttu-id="c269a-235">PostgresSQL 별칭</span><span class="sxs-lookup"><span data-stu-id="c269a-235">PostgresSQL aliases</span></span> | <span data-ttu-id="c269a-236">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="c269a-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c269a-237">abstime</span><span class="sxs-lookup"><span data-stu-id="c269a-237">abstime</span></span> | |<span data-ttu-id="c269a-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="c269a-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="c269a-239">bigint</span><span class="sxs-lookup"><span data-stu-id="c269a-239">bigint</span></span> |<span data-ttu-id="c269a-240">int8</span><span class="sxs-lookup"><span data-stu-id="c269a-240">int8</span></span> |<span data-ttu-id="c269a-241">Int64</span><span class="sxs-lookup"><span data-stu-id="c269a-241">Int64</span></span> |
| <span data-ttu-id="c269a-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="c269a-242">bigserial</span></span> |<span data-ttu-id="c269a-243">serial8</span><span class="sxs-lookup"><span data-stu-id="c269a-243">serial8</span></span> |<span data-ttu-id="c269a-244">Int64</span><span class="sxs-lookup"><span data-stu-id="c269a-244">Int64</span></span> |
| <span data-ttu-id="c269a-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-245">bit [ (n) ]</span></span> | |<span data-ttu-id="c269a-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="c269a-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="c269a-248">varbit</span><span class="sxs-lookup"><span data-stu-id="c269a-248">varbit</span></span> |<span data-ttu-id="c269a-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-249">Byte[], String</span></span> |
| <span data-ttu-id="c269a-250">부울</span><span class="sxs-lookup"><span data-stu-id="c269a-250">boolean</span></span> |<span data-ttu-id="c269a-251">bool</span><span class="sxs-lookup"><span data-stu-id="c269a-251">bool</span></span> |<span data-ttu-id="c269a-252">부울</span><span class="sxs-lookup"><span data-stu-id="c269a-252">Boolean</span></span> |
| <span data-ttu-id="c269a-253">box</span><span class="sxs-lookup"><span data-stu-id="c269a-253">box</span></span> | |<span data-ttu-id="c269a-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-255">bytea</span><span class="sxs-lookup"><span data-stu-id="c269a-255">bytea</span></span> | |<span data-ttu-id="c269a-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-257">character [ (n) ]</span></span> |<span data-ttu-id="c269a-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-258">char [ (n) ]</span></span> |<span data-ttu-id="c269a-259">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-259">String</span></span> |
| <span data-ttu-id="c269a-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-260">character varying [ (n) ]</span></span> |<span data-ttu-id="c269a-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-261">varchar [ (n) ]</span></span> |<span data-ttu-id="c269a-262">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-262">String</span></span> |
| <span data-ttu-id="c269a-263">cid</span><span class="sxs-lookup"><span data-stu-id="c269a-263">cid</span></span> | |<span data-ttu-id="c269a-264">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-264">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-265">cidr</span><span class="sxs-lookup"><span data-stu-id="c269a-265">cidr</span></span> | |<span data-ttu-id="c269a-266">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-266">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-267">circle</span><span class="sxs-lookup"><span data-stu-id="c269a-267">circle</span></span> | |<span data-ttu-id="c269a-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-269">date</span><span class="sxs-lookup"><span data-stu-id="c269a-269">date</span></span> | |<span data-ttu-id="c269a-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="c269a-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="c269a-271">daterange</span><span class="sxs-lookup"><span data-stu-id="c269a-271">daterange</span></span> | |<span data-ttu-id="c269a-272">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-272">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-273">double precision</span><span class="sxs-lookup"><span data-stu-id="c269a-273">double precision</span></span> |<span data-ttu-id="c269a-274">float8</span><span class="sxs-lookup"><span data-stu-id="c269a-274">float8</span></span> |<span data-ttu-id="c269a-275">Double</span><span class="sxs-lookup"><span data-stu-id="c269a-275">Double</span></span> |
| <span data-ttu-id="c269a-276">inet</span><span class="sxs-lookup"><span data-stu-id="c269a-276">inet</span></span> | |<span data-ttu-id="c269a-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-278">intarry</span><span class="sxs-lookup"><span data-stu-id="c269a-278">intarry</span></span> | |<span data-ttu-id="c269a-279">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-279">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-280">int4range</span><span class="sxs-lookup"><span data-stu-id="c269a-280">int4range</span></span> | |<span data-ttu-id="c269a-281">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-281">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-282">int8range</span><span class="sxs-lookup"><span data-stu-id="c269a-282">int8range</span></span> | |<span data-ttu-id="c269a-283">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-283">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-284">정수</span><span class="sxs-lookup"><span data-stu-id="c269a-284">integer</span></span> |<span data-ttu-id="c269a-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="c269a-285">int, int4</span></span> |<span data-ttu-id="c269a-286">Int32</span><span class="sxs-lookup"><span data-stu-id="c269a-286">Int32</span></span> |
| <span data-ttu-id="c269a-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="c269a-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="c269a-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="c269a-289">json :</span><span class="sxs-lookup"><span data-stu-id="c269a-289">json</span></span> | |<span data-ttu-id="c269a-290">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-290">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="c269a-291">jsonb</span></span> | |<span data-ttu-id="c269a-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c269a-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="c269a-293">line</span><span class="sxs-lookup"><span data-stu-id="c269a-293">line</span></span> | |<span data-ttu-id="c269a-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-295">lseg</span><span class="sxs-lookup"><span data-stu-id="c269a-295">lseg</span></span> | |<span data-ttu-id="c269a-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="c269a-297">macaddr</span></span> | |<span data-ttu-id="c269a-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-299">money</span><span class="sxs-lookup"><span data-stu-id="c269a-299">money</span></span> | |<span data-ttu-id="c269a-300">10진수</span><span class="sxs-lookup"><span data-stu-id="c269a-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="c269a-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="c269a-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="c269a-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="c269a-303">10진수</span><span class="sxs-lookup"><span data-stu-id="c269a-303">Decimal</span></span> |
| <span data-ttu-id="c269a-304">numrange</span><span class="sxs-lookup"><span data-stu-id="c269a-304">numrange</span></span> | |<span data-ttu-id="c269a-305">문자열</span><span class="sxs-lookup"><span data-stu-id="c269a-305">String</span></span> |&nbsp;
| <span data-ttu-id="c269a-306">oid</span><span class="sxs-lookup"><span data-stu-id="c269a-306">oid</span></span> | |<span data-ttu-id="c269a-307">Int32</span><span class="sxs-lookup"><span data-stu-id="c269a-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="c269a-308">path</span><span class="sxs-lookup"><span data-stu-id="c269a-308">path</span></span> | |<span data-ttu-id="c269a-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="c269a-310">pg_lsn</span></span> | |<span data-ttu-id="c269a-311">Int64</span><span class="sxs-lookup"><span data-stu-id="c269a-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="c269a-312">point</span><span class="sxs-lookup"><span data-stu-id="c269a-312">point</span></span> | |<span data-ttu-id="c269a-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-314">polygon</span><span class="sxs-lookup"><span data-stu-id="c269a-314">polygon</span></span> | |<span data-ttu-id="c269a-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="c269a-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="c269a-316">real</span><span class="sxs-lookup"><span data-stu-id="c269a-316">real</span></span> |<span data-ttu-id="c269a-317">float4</span><span class="sxs-lookup"><span data-stu-id="c269a-317">float4</span></span> |<span data-ttu-id="c269a-318">Single</span><span class="sxs-lookup"><span data-stu-id="c269a-318">Single</span></span> |
| <span data-ttu-id="c269a-319">smallint</span><span class="sxs-lookup"><span data-stu-id="c269a-319">smallint</span></span> |<span data-ttu-id="c269a-320">int2</span><span class="sxs-lookup"><span data-stu-id="c269a-320">int2</span></span> |<span data-ttu-id="c269a-321">Int16</span><span class="sxs-lookup"><span data-stu-id="c269a-321">Int16</span></span> |
| <span data-ttu-id="c269a-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="c269a-322">smallserial</span></span> |<span data-ttu-id="c269a-323">serial2</span><span class="sxs-lookup"><span data-stu-id="c269a-323">serial2</span></span> |<span data-ttu-id="c269a-324">Int16</span><span class="sxs-lookup"><span data-stu-id="c269a-324">Int16</span></span> |
| <span data-ttu-id="c269a-325">serial</span><span class="sxs-lookup"><span data-stu-id="c269a-325">serial</span></span> |<span data-ttu-id="c269a-326">serial4</span><span class="sxs-lookup"><span data-stu-id="c269a-326">serial4</span></span> |<span data-ttu-id="c269a-327">Int32</span><span class="sxs-lookup"><span data-stu-id="c269a-327">Int32</span></span> |
| <span data-ttu-id="c269a-328">텍스트</span><span class="sxs-lookup"><span data-stu-id="c269a-328">text</span></span> | |<span data-ttu-id="c269a-329">String</span><span class="sxs-lookup"><span data-stu-id="c269a-329">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c269a-330">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="c269a-330">Map source to sink columns</span></span>
<span data-ttu-id="c269a-331">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-331">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c269a-332">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="c269a-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="c269a-333">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-333">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c269a-334">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c269a-335">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c269a-336">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c269a-336">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c269a-337">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c269a-338">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="c269a-338">Performance and Tuning</span></span>
<span data-ttu-id="c269a-339">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c269a-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
