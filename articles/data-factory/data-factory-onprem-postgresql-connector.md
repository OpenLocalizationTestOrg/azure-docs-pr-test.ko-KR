---
title: "aaaMove 데이터에서 PostgreSQL Azure 데이터 팩터리를 사용 하 여 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 PostgreSQL 데이터베이스에서 toomove 데이터입니다."
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
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="f4e0d-103">Azure 데이터 팩터리를 사용하여 PostgreSQL에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="f4e0d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="f4e0d-104">이 문서에서는 toouse 온-프레미스 PostgreSQL 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="f4e0d-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="f4e0d-106">온-프레미스 PostgreSQL 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="f4e0d-107">목록이 hello 복사 작업에서 싱크를 지 원하는 데이터 저장소에 대 한 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f4e0d-108">데이터 팩터리의 현재 tooother 데이터 저장소에서 데이터베이스를 한 PostgreSQL에서 데이터를 이동 하는 원하는 하지만 하지 tooan PostgreSQL 데이터베이스 저장 다른 데이터에서 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4e0d-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4e0d-109">prerequisites</span></span>

<span data-ttu-id="f4e0d-110">데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 PostgreSQL 원본을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="f4e0d-111">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="f4e0d-112">게이트웨이 hello PostgreSQL 데이터베이스 Azure IaaS VM에서 호스팅되는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="f4e0d-113">Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="f4e0d-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="f4e0d-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="f4e0d-115">Supported versions and installation</span></span>
<span data-ttu-id="f4e0d-116">데이터 관리 게이트웨이 tooconnect toohello PostgreSQL 데이터베이스를 설치 hello [PostgreSQL Ngpsql 데이터 공급자](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 위에 hello 동일 또는 데이터 관리 게이트웨이 hello 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="f4e0d-117">PostgreSQL 버전 7.4 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f4e0d-118">시작</span><span class="sxs-lookup"><span data-stu-id="f4e0d-118">Getting started</span></span>
<span data-ttu-id="f4e0d-119">여러 도구/API를 사용하여 온-프레미스 PostgreSQL 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="f4e0d-120">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f4e0d-121">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="f4e0d-122">다음 도구 toocreate 파이프라인 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="f4e0d-123">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f4e0d-123">Azure portal</span></span>
    - <span data-ttu-id="f4e0d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4e0d-124">Visual Studio</span></span>
    - <span data-ttu-id="f4e0d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4e0d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="f4e0d-126">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="f4e0d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="f4e0d-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="f4e0d-127">.NET API</span></span>
    - <span data-ttu-id="f4e0d-128">REST API</span><span class="sxs-lookup"><span data-stu-id="f4e0d-128">REST API</span></span>

     <span data-ttu-id="f4e0d-129">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f4e0d-130">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="f4e0d-131">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f4e0d-132">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="f4e0d-133">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f4e0d-134">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f4e0d-135">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f4e0d-136">Data Factory 된 엔터티를 온-프레미스 PostgreSQL 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: PostgreSQL tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-postgresql-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f4e0d-137">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa PostgreSQL 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f4e0d-138">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-138">Linked service properties</span></span>
<span data-ttu-id="f4e0d-139">다음 표에서 hello JSON 요소 특정 tooPostgreSQL 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="f4e0d-140">속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-140">Property</span></span> | <span data-ttu-id="f4e0d-141">설명</span><span class="sxs-lookup"><span data-stu-id="f4e0d-141">Description</span></span> | <span data-ttu-id="f4e0d-142">필수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4e0d-143">type</span><span class="sxs-lookup"><span data-stu-id="f4e0d-143">type</span></span> |<span data-ttu-id="f4e0d-144">hello type 속성 설정 해야 합니다: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="f4e0d-145">예</span><span class="sxs-lookup"><span data-stu-id="f4e0d-145">Yes</span></span> |
| <span data-ttu-id="f4e0d-146">server</span><span class="sxs-lookup"><span data-stu-id="f4e0d-146">server</span></span> |<span data-ttu-id="f4e0d-147">Hello PostgreSQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="f4e0d-148">예</span><span class="sxs-lookup"><span data-stu-id="f4e0d-148">Yes</span></span> |
| <span data-ttu-id="f4e0d-149">database</span><span class="sxs-lookup"><span data-stu-id="f4e0d-149">database</span></span> |<span data-ttu-id="f4e0d-150">Hello PostgreSQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="f4e0d-151">예</span><span class="sxs-lookup"><span data-stu-id="f4e0d-151">Yes</span></span> |
| <span data-ttu-id="f4e0d-152">schema</span><span class="sxs-lookup"><span data-stu-id="f4e0d-152">schema</span></span> |<span data-ttu-id="f4e0d-153">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="f4e0d-154">hello 스키마 이름이 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="f4e0d-155">아니요</span><span class="sxs-lookup"><span data-stu-id="f4e0d-155">No</span></span> |
| <span data-ttu-id="f4e0d-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f4e0d-156">authenticationType</span></span> |<span data-ttu-id="f4e0d-157">Tooconnect toohello PostgreSQL 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="f4e0d-158">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f4e0d-159">예</span><span class="sxs-lookup"><span data-stu-id="f4e0d-159">Yes</span></span> |
| <span data-ttu-id="f4e0d-160">username</span><span class="sxs-lookup"><span data-stu-id="f4e0d-160">username</span></span> |<span data-ttu-id="f4e0d-161">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="f4e0d-162">아니요</span><span class="sxs-lookup"><span data-stu-id="f4e0d-162">No</span></span> |
| <span data-ttu-id="f4e0d-163">암호</span><span class="sxs-lookup"><span data-stu-id="f4e0d-163">password</span></span> |<span data-ttu-id="f4e0d-164">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="f4e0d-165">아니요</span><span class="sxs-lookup"><span data-stu-id="f4e0d-165">No</span></span> |
| <span data-ttu-id="f4e0d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f4e0d-166">gatewayName</span></span> |<span data-ttu-id="f4e0d-167">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 PostgreSQL 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="f4e0d-168">예</span><span class="sxs-lookup"><span data-stu-id="f4e0d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f4e0d-169">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-169">Dataset properties</span></span>
<span data-ttu-id="f4e0d-170">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f4e0d-171">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="f4e0d-172">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f4e0d-173">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **RelationalTable** hello 다음과 같은 속성에 (PostgreSQL 데이터 집합 포함):</span><span class="sxs-lookup"><span data-stu-id="f4e0d-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="f4e0d-174">속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-174">Property</span></span> | <span data-ttu-id="f4e0d-175">설명</span><span class="sxs-lookup"><span data-stu-id="f4e0d-175">Description</span></span> | <span data-ttu-id="f4e0d-176">필수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4e0d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="f4e0d-177">tableName</span></span> |<span data-ttu-id="f4e0d-178">PostgreSQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="f4e0d-179">hello tableName은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="f4e0d-180">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="f4e0d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f4e0d-181">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-181">Copy activity properties</span></span>
<span data-ttu-id="f4e0d-182">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f4e0d-183">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f4e0d-184">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="f4e0d-185">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="f4e0d-186">원본 유형의 경우 **RelationalSource** (PostgreSQL 포함), 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f4e0d-187">속성</span><span class="sxs-lookup"><span data-stu-id="f4e0d-187">Property</span></span> | <span data-ttu-id="f4e0d-188">설명</span><span class="sxs-lookup"><span data-stu-id="f4e0d-188">Description</span></span> | <span data-ttu-id="f4e0d-189">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="f4e0d-189">Allowed values</span></span> | <span data-ttu-id="f4e0d-190">필수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f4e0d-191">쿼리</span><span class="sxs-lookup"><span data-stu-id="f4e0d-191">query</span></span> |<span data-ttu-id="f4e0d-192">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="f4e0d-193">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-193">SQL query string.</span></span> <span data-ttu-id="f4e0d-194">예: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="f4e0d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="f4e0d-195">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="f4e0d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="f4e0d-196">스키마 및 테이블 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="f4e0d-197">로 둘러쌀 `""` (큰따옴표) hello 쿼리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="f4e0d-198">**예제:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="f4e0d-199">JSON의 예: PostgreSQL tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="f4e0d-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="f4e0d-200">이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f4e0d-201">Toocopy 데이터로 PostgreSQL 데이터베이스 tooAzure Blob 저장소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="f4e0d-202">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="f4e0d-203">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="f4e0d-204">Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="f4e0d-205">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="f4e0d-206">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="f4e0d-207">[OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="f4e0d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="f4e0d-208">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="f4e0d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f4e0d-209">[RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="f4e0d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f4e0d-210">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="f4e0d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f4e0d-211">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f4e0d-212">hello 샘플 데이터 복사 PostgreSQL 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="f4e0d-213">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f4e0d-214">첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="f4e0d-215">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f4e0d-216">**PostgreSQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-216">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="f4e0d-217">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-217">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f4e0d-218">**PostgreSQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="f4e0d-219">hello 샘플 테이블 "MyTable"에서 만든 PostgreSQL 가정 시계열 데이터에 대 한 "timestamp" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="f4e0d-220">설정 `"external": true` 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="f4e0d-221">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f4e0d-222">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="f4e0d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f4e0d-223">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f4e0d-224">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="f4e0d-225">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="f4e0d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="f4e0d-226">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="f4e0d-227">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f4e0d-228">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello PostgreSQL 데이터베이스의 hello public.usstates 테이블에서 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="f4e0d-229">PostgreSQL에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="f4e0d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="f4e0d-230">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="f4e0d-231">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="f4e0d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="f4e0d-232">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="f4e0d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="f4e0d-233">데이터 tooPostgreSQL를 이동할 때는 hello 다음 매핑은 사용 하는 PostgreSQL 형식 too.NET 형식에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="f4e0d-234">PostgreSQL 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="f4e0d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="f4e0d-235">PostgresSQL 별칭</span><span class="sxs-lookup"><span data-stu-id="f4e0d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="f4e0d-236">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="f4e0d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4e0d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="f4e0d-237">abstime</span></span> | |<span data-ttu-id="f4e0d-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="f4e0d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="f4e0d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="f4e0d-239">bigint</span></span> |<span data-ttu-id="f4e0d-240">int8</span><span class="sxs-lookup"><span data-stu-id="f4e0d-240">int8</span></span> |<span data-ttu-id="f4e0d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="f4e0d-241">Int64</span></span> |
| <span data-ttu-id="f4e0d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="f4e0d-242">bigserial</span></span> |<span data-ttu-id="f4e0d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="f4e0d-243">serial8</span></span> |<span data-ttu-id="f4e0d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="f4e0d-244">Int64</span></span> |
| <span data-ttu-id="f4e0d-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="f4e0d-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="f4e0d-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="f4e0d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="f4e0d-248">varbit</span></span> |<span data-ttu-id="f4e0d-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-249">Byte[], String</span></span> |
| <span data-ttu-id="f4e0d-250">부울</span><span class="sxs-lookup"><span data-stu-id="f4e0d-250">boolean</span></span> |<span data-ttu-id="f4e0d-251">bool</span><span class="sxs-lookup"><span data-stu-id="f4e0d-251">bool</span></span> |<span data-ttu-id="f4e0d-252">부울</span><span class="sxs-lookup"><span data-stu-id="f4e0d-252">Boolean</span></span> |
| <span data-ttu-id="f4e0d-253">box</span><span class="sxs-lookup"><span data-stu-id="f4e0d-253">box</span></span> | |<span data-ttu-id="f4e0d-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="f4e0d-255">bytea</span></span> | |<span data-ttu-id="f4e0d-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-257">character [ (n) ]</span></span> |<span data-ttu-id="f4e0d-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-258">char [ (n) ]</span></span> |<span data-ttu-id="f4e0d-259">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-259">String</span></span> |
| <span data-ttu-id="f4e0d-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="f4e0d-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="f4e0d-262">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-262">String</span></span> |
| <span data-ttu-id="f4e0d-263">cid</span><span class="sxs-lookup"><span data-stu-id="f4e0d-263">cid</span></span> | |<span data-ttu-id="f4e0d-264">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-264">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-265">cidr</span><span class="sxs-lookup"><span data-stu-id="f4e0d-265">cidr</span></span> | |<span data-ttu-id="f4e0d-266">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-266">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-267">circle</span><span class="sxs-lookup"><span data-stu-id="f4e0d-267">circle</span></span> | |<span data-ttu-id="f4e0d-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-269">date</span><span class="sxs-lookup"><span data-stu-id="f4e0d-269">date</span></span> | |<span data-ttu-id="f4e0d-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="f4e0d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-271">daterange</span><span class="sxs-lookup"><span data-stu-id="f4e0d-271">daterange</span></span> | |<span data-ttu-id="f4e0d-272">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-272">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-273">double precision</span><span class="sxs-lookup"><span data-stu-id="f4e0d-273">double precision</span></span> |<span data-ttu-id="f4e0d-274">float8</span><span class="sxs-lookup"><span data-stu-id="f4e0d-274">float8</span></span> |<span data-ttu-id="f4e0d-275">Double</span><span class="sxs-lookup"><span data-stu-id="f4e0d-275">Double</span></span> |
| <span data-ttu-id="f4e0d-276">inet</span><span class="sxs-lookup"><span data-stu-id="f4e0d-276">inet</span></span> | |<span data-ttu-id="f4e0d-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="f4e0d-278">intarry</span></span> | |<span data-ttu-id="f4e0d-279">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-279">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="f4e0d-280">int4range</span></span> | |<span data-ttu-id="f4e0d-281">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-281">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="f4e0d-282">int8range</span></span> | |<span data-ttu-id="f4e0d-283">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-283">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-284">정수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-284">integer</span></span> |<span data-ttu-id="f4e0d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="f4e0d-285">int, int4</span></span> |<span data-ttu-id="f4e0d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="f4e0d-286">Int32</span></span> |
| <span data-ttu-id="f4e0d-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="f4e0d-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="f4e0d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-289">json :</span><span class="sxs-lookup"><span data-stu-id="f4e0d-289">json</span></span> | |<span data-ttu-id="f4e0d-290">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-290">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="f4e0d-291">jsonb</span></span> | |<span data-ttu-id="f4e0d-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-293">line</span><span class="sxs-lookup"><span data-stu-id="f4e0d-293">line</span></span> | |<span data-ttu-id="f4e0d-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="f4e0d-295">lseg</span></span> | |<span data-ttu-id="f4e0d-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="f4e0d-297">macaddr</span></span> | |<span data-ttu-id="f4e0d-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-299">money</span><span class="sxs-lookup"><span data-stu-id="f4e0d-299">money</span></span> | |<span data-ttu-id="f4e0d-300">10진수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="f4e0d-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="f4e0d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="f4e0d-303">10진수</span><span class="sxs-lookup"><span data-stu-id="f4e0d-303">Decimal</span></span> |
| <span data-ttu-id="f4e0d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="f4e0d-304">numrange</span></span> | |<span data-ttu-id="f4e0d-305">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-305">String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-306">oid</span><span class="sxs-lookup"><span data-stu-id="f4e0d-306">oid</span></span> | |<span data-ttu-id="f4e0d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="f4e0d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-308">path</span><span class="sxs-lookup"><span data-stu-id="f4e0d-308">path</span></span> | |<span data-ttu-id="f4e0d-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="f4e0d-310">pg_lsn</span></span> | |<span data-ttu-id="f4e0d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="f4e0d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-312">point</span><span class="sxs-lookup"><span data-stu-id="f4e0d-312">point</span></span> | |<span data-ttu-id="f4e0d-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-314">polygon</span><span class="sxs-lookup"><span data-stu-id="f4e0d-314">polygon</span></span> | |<span data-ttu-id="f4e0d-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="f4e0d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="f4e0d-316">real</span><span class="sxs-lookup"><span data-stu-id="f4e0d-316">real</span></span> |<span data-ttu-id="f4e0d-317">float4</span><span class="sxs-lookup"><span data-stu-id="f4e0d-317">float4</span></span> |<span data-ttu-id="f4e0d-318">Single</span><span class="sxs-lookup"><span data-stu-id="f4e0d-318">Single</span></span> |
| <span data-ttu-id="f4e0d-319">smallint</span><span class="sxs-lookup"><span data-stu-id="f4e0d-319">smallint</span></span> |<span data-ttu-id="f4e0d-320">int2</span><span class="sxs-lookup"><span data-stu-id="f4e0d-320">int2</span></span> |<span data-ttu-id="f4e0d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="f4e0d-321">Int16</span></span> |
| <span data-ttu-id="f4e0d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="f4e0d-322">smallserial</span></span> |<span data-ttu-id="f4e0d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="f4e0d-323">serial2</span></span> |<span data-ttu-id="f4e0d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="f4e0d-324">Int16</span></span> |
| <span data-ttu-id="f4e0d-325">serial</span><span class="sxs-lookup"><span data-stu-id="f4e0d-325">serial</span></span> |<span data-ttu-id="f4e0d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="f4e0d-326">serial4</span></span> |<span data-ttu-id="f4e0d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="f4e0d-327">Int32</span></span> |
| <span data-ttu-id="f4e0d-328">텍스트</span><span class="sxs-lookup"><span data-stu-id="f4e0d-328">text</span></span> | |<span data-ttu-id="f4e0d-329">문자열</span><span class="sxs-lookup"><span data-stu-id="f4e0d-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="f4e0d-330">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="f4e0d-330">Map source toosink columns</span></span>
<span data-ttu-id="f4e0d-331">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f4e0d-332">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="f4e0d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="f4e0d-333">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="f4e0d-334">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f4e0d-335">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f4e0d-336">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f4e0d-337">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f4e0d-338">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="f4e0d-338">Performance and Tuning</span></span>
<span data-ttu-id="f4e0d-339">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4e0d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
