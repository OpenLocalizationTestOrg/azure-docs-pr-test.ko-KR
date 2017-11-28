---
title: "Azure 데이터 팩터리를 사용 하 여 Sybase에서 aaaMove 데이터 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 Sybase 데이터베이스에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="cdfdf-103">Azure 데이터 팩터리를 사용하여 Sybase에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="cdfdf-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="cdfdf-104">이 문서에서는 toouse 복사 작업에서는 온-프레미스 Sybase 데이터베이스에서 Azure Data Factory toomove 데이터에서 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="cdfdf-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="cdfdf-106">온-프레미스 Sybase 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="cdfdf-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="cdfdf-108">데이터 팩터리는 현재 이동 Sybase 데이터에서 데이터 저장 tooother 데이터 저장소 뿐만 아니라 다른 데이터 저장소 tooa Sybase 데이터 저장소에서 데이터 이동에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cdfdf-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cdfdf-109">Prerequisites</span></span>
<span data-ttu-id="cdfdf-110">데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 Sybase 원본을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="cdfdf-111">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="cdfdf-112">게이트웨이 hello Sybase 데이터베이스 Azure IaaS VM에서 호스팅되는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="cdfdf-113">Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="cdfdf-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="cdfdf-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="cdfdf-115">Supported versions and installation</span></span>
<span data-ttu-id="cdfdf-116">Tooinstall hello 해야 데이터 관리 게이트웨이 tooconnect toohello Sybase 데이터베이스를 [Sybase iAnywhere.Data.SQLAnywhere에 대 한 데이터 공급자](http://go.microsoft.com/fwlink/?linkid=324846) 16 위에 hello 동일 또는 시스템 데이터 관리 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="cdfdf-117">Sybase 버전 16 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cdfdf-118">시작</span><span class="sxs-lookup"><span data-stu-id="cdfdf-118">Getting started</span></span>
<span data-ttu-id="cdfdf-119">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="cdfdf-120">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cdfdf-121">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="cdfdf-122">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cdfdf-123">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cdfdf-124">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cdfdf-125">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="cdfdf-126">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="cdfdf-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="cdfdf-128">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cdfdf-129">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cdfdf-130">Data Factory 된 엔터티를 온-프레미스 Sybase 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: Sybase tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-sybase-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="cdfdf-131">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa Sybase 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cdfdf-132">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-132">Linked service properties</span></span>
<span data-ttu-id="cdfdf-133">다음 표에서 hello JSON 요소 특정 tooSybase 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="cdfdf-134">속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-134">Property</span></span> | <span data-ttu-id="cdfdf-135">설명</span><span class="sxs-lookup"><span data-stu-id="cdfdf-135">Description</span></span> | <span data-ttu-id="cdfdf-136">필수</span><span class="sxs-lookup"><span data-stu-id="cdfdf-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdfdf-137">type</span><span class="sxs-lookup"><span data-stu-id="cdfdf-137">type</span></span> |<span data-ttu-id="cdfdf-138">hello type 속성 설정 해야 합니다: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="cdfdf-139">예</span><span class="sxs-lookup"><span data-stu-id="cdfdf-139">Yes</span></span> |
| <span data-ttu-id="cdfdf-140">server</span><span class="sxs-lookup"><span data-stu-id="cdfdf-140">server</span></span> |<span data-ttu-id="cdfdf-141">Hello Sybase 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="cdfdf-142">예</span><span class="sxs-lookup"><span data-stu-id="cdfdf-142">Yes</span></span> |
| <span data-ttu-id="cdfdf-143">database</span><span class="sxs-lookup"><span data-stu-id="cdfdf-143">database</span></span> |<span data-ttu-id="cdfdf-144">Hello Sybase 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="cdfdf-145">예</span><span class="sxs-lookup"><span data-stu-id="cdfdf-145">Yes</span></span> |
| <span data-ttu-id="cdfdf-146">schema</span><span class="sxs-lookup"><span data-stu-id="cdfdf-146">schema</span></span> |<span data-ttu-id="cdfdf-147">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="cdfdf-148">아니요</span><span class="sxs-lookup"><span data-stu-id="cdfdf-148">No</span></span> |
| <span data-ttu-id="cdfdf-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cdfdf-149">authenticationType</span></span> |<span data-ttu-id="cdfdf-150">Tooconnect toohello Sybase 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="cdfdf-151">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="cdfdf-152">예</span><span class="sxs-lookup"><span data-stu-id="cdfdf-152">Yes</span></span> |
| <span data-ttu-id="cdfdf-153">username</span><span class="sxs-lookup"><span data-stu-id="cdfdf-153">username</span></span> |<span data-ttu-id="cdfdf-154">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="cdfdf-155">아니요</span><span class="sxs-lookup"><span data-stu-id="cdfdf-155">No</span></span> |
| <span data-ttu-id="cdfdf-156">암호</span><span class="sxs-lookup"><span data-stu-id="cdfdf-156">password</span></span> |<span data-ttu-id="cdfdf-157">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="cdfdf-158">아니요</span><span class="sxs-lookup"><span data-stu-id="cdfdf-158">No</span></span> |
| <span data-ttu-id="cdfdf-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cdfdf-159">gatewayName</span></span> |<span data-ttu-id="cdfdf-160">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Sybase 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="cdfdf-161">예</span><span class="sxs-lookup"><span data-stu-id="cdfdf-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="cdfdf-162">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-162">Dataset properties</span></span>
<span data-ttu-id="cdfdf-163">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cdfdf-164">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="cdfdf-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cdfdf-165">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="cdfdf-166">hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **RelationalTable** hello 다음과 같은 속성에 (Sybase 데이터 집합 포함):</span><span class="sxs-lookup"><span data-stu-id="cdfdf-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="cdfdf-167">속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-167">Property</span></span> | <span data-ttu-id="cdfdf-168">설명</span><span class="sxs-lookup"><span data-stu-id="cdfdf-168">Description</span></span> | <span data-ttu-id="cdfdf-169">필수</span><span class="sxs-lookup"><span data-stu-id="cdfdf-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdfdf-170">tableName</span><span class="sxs-lookup"><span data-stu-id="cdfdf-170">tableName</span></span> |<span data-ttu-id="cdfdf-171">Sybase 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="cdfdf-172">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="cdfdf-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="cdfdf-173">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-173">Copy activity properties</span></span>
<span data-ttu-id="cdfdf-174">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cdfdf-175">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="cdfdf-176">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cdfdf-177">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="cdfdf-178">Hello 원본 유형의 경우 **RelationalSource** (Sybase 포함), hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="cdfdf-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="cdfdf-179">속성</span><span class="sxs-lookup"><span data-stu-id="cdfdf-179">Property</span></span> | <span data-ttu-id="cdfdf-180">설명</span><span class="sxs-lookup"><span data-stu-id="cdfdf-180">Description</span></span> | <span data-ttu-id="cdfdf-181">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="cdfdf-181">Allowed values</span></span> | <span data-ttu-id="cdfdf-182">필수</span><span class="sxs-lookup"><span data-stu-id="cdfdf-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cdfdf-183">쿼리</span><span class="sxs-lookup"><span data-stu-id="cdfdf-183">query</span></span> |<span data-ttu-id="cdfdf-184">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="cdfdf-185">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-185">SQL query string.</span></span> <span data-ttu-id="cdfdf-186">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="cdfdf-187">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="cdfdf-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="cdfdf-188">JSON의 예: Sybase tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="cdfdf-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="cdfdf-189">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cdfdf-190">Sybase에서 toocopy 데이터 tooAzure Blob Storage 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="cdfdf-191">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="cdfdf-192">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="cdfdf-193">[OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cdfdf-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cdfdf-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cdfdf-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cdfdf-195">[RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="cdfdf-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cdfdf-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="cdfdf-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cdfdf-197">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cdfdf-198">hello 샘플 데이터 복사 Sybase 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="cdfdf-199">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cdfdf-200">첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="cdfdf-201">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="cdfdf-202">**Sybase 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="cdfdf-203">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="cdfdf-204">**Sybase 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="cdfdf-205">hello 샘플 가정 테이블 "MyTable"에서 만든 Sybase 시계열 데이터에 대 한 "timestamp" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="cdfdf-206">"External" 설정: true hello 데이터 팩터리 서비스에 알리고이 데이터 집합은 외부 toohello 데이터 팩터리 hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="cdfdf-207">해당 hello 확인 **형식** hello로 연결 된 서비스 설정: **RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="cdfdf-208">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cdfdf-209">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="cdfdf-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cdfdf-210">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cdfdf-211">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="cdfdf-212">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="cdfdf-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="cdfdf-213">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="cdfdf-214">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="cdfdf-215">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello DBA에서에서 hello 데이터를 선택 합니다. Hello 데이터베이스의 orders 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="cdfdf-216">Sybase에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="cdfdf-216">Type mapping for Sybase</span></span>
<span data-ttu-id="cdfdf-217">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 hello 복사 활동 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="cdfdf-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="cdfdf-218">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="cdfdf-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="cdfdf-219">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="cdfdf-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="cdfdf-220">Sybase는 T-SQL 및 T-SQL 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="cdfdf-221">Sql 형식 too.NET 형식에서 매핑 테이블을 참조 하십시오. [Azure SQL 커넥터](data-factory-azure-sql-connector.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="cdfdf-222">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="cdfdf-222">Map source toosink columns</span></span>
<span data-ttu-id="cdfdf-223">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="cdfdf-224">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="cdfdf-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="cdfdf-225">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="cdfdf-226">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cdfdf-227">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cdfdf-228">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="cdfdf-229">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cdfdf-230">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="cdfdf-230">Performance and Tuning</span></span>
<span data-ttu-id="cdfdf-231">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdfdf-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
