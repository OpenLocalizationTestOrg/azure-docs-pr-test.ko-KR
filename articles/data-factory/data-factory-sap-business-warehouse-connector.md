---
title: "Azure 데이터 팩터리를 사용 하 여 SAP Business Warehouse aaaMove 데이터로 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 SAP Business Warehouse에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="cd499-103">Azure Data Factory를 사용하여 SAP Business Warehouse에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="cd499-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="cd499-104">이 문서에서는 toouse Azure Data Factory toomove 데이터에서는 온-프레미스 SAP 비즈니스 웨어하우스 (BW)의 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="cd499-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="cd499-106">온-프레미스 SAP Business Warehouse 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="cd499-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="cd499-108">데이터 팩터리의 현재만 지 원하는 데이터를 SAP Business Warehouse tooother 데이터에서에서 저장 하지 않은 이동 tooan SAP Business Warehouse 저장소 다른 데이터에서 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="cd499-109">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="cd499-109">Supported versions and installation</span></span>
<span data-ttu-id="cd499-110">이 커넥터는 SAP Business Warehouse 버전 7.x를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="cd499-111">MDX 쿼리를 사용하여 InfoCubes 및 QueryCubes(BEx 쿼리 포함)에서 데이터를 복사하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="cd499-112">tooenable hello 연결 toohello SAP BW 인스턴스는 다음과 같은 구성 요소가 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="cd499-113">**데이터 관리 게이트웨이**: Data Factory 서비스가 지 원하는 tooon 온-프레미스 데이터 연결 (포함 하 여 SAP Business Warehouse) 저장소 데이터 관리 게이트웨이 라는 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="cd499-114">데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 toolearn 참조 [toocloud 데이터 저장소를 저장 하는 온-프레미스 데이터 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd499-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="cd499-115">게이트웨이 SAP Business Warehouse hello Azure IaaS 가상 컴퓨터 (VM)에서 호스팅되는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="cd499-116">동일한 VM hello 데이터로 저장 하거나 hello 게이트웨이 다른 VM에 연결할 수 toohello 데이터베이스 hello에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="cd499-117">**SAP NetWeaver 라이브러리** hello 게이트웨이 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="cd499-118">SAP 관리자 또는 hello에서 직접 hello SAP Netweaver 라이브러리를 얻을 수 [SAP 소프트웨어 다운로드 센터](https://support.sap.com/swdc)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="cd499-119">Hello에 대 한 검색 **SAP 참고 #1025361** hello 가장 최신 버전에 대 한 tooget hello 다운로드 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="cd499-120">Hello 아키텍처 (32 비트 또는 64 비트) hello SAP NetWeaver 라이브러리에 대 한 게이트웨이 설치와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="cd499-121">Hello SAP NetWeaver RFC SDK에 따라 toohello SAP Note에에서 포함 된 모든 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="cd499-122">hello SAP NetWeaver 라이브러리 hello SAP 클라이언트 도구 설치에에서도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="cd499-123">NetWeaver RFC SDK system32 폴더에 hello에서 추출 된 hello dll을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cd499-124">시작</span><span class="sxs-lookup"><span data-stu-id="cd499-124">Getting started</span></span>
<span data-ttu-id="cd499-125">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="cd499-126">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cd499-127">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="cd499-128">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cd499-129">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cd499-130">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cd499-131">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="cd499-132">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="cd499-133">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="cd499-134">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cd499-135">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cd499-136">Data Factory 된 엔터티를 온-프레미스 SAP Business Warehouse에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: SAP Business Warehouse tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="cd499-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="cd499-137">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooan SAP BW 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cd499-138">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="cd499-138">Linked service properties</span></span>
<span data-ttu-id="cd499-139">다음 표에서 hello JSON 요소 특정 tooSAP 비즈니스 웨어하우스 (BW) 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="cd499-140">속성</span><span class="sxs-lookup"><span data-stu-id="cd499-140">Property</span></span> | <span data-ttu-id="cd499-141">설명</span><span class="sxs-lookup"><span data-stu-id="cd499-141">Description</span></span> | <span data-ttu-id="cd499-142">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="cd499-142">Allowed values</span></span> | <span data-ttu-id="cd499-143">필수</span><span class="sxs-lookup"><span data-stu-id="cd499-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="cd499-144">server</span><span class="sxs-lookup"><span data-stu-id="cd499-144">server</span></span> | <span data-ttu-id="cd499-145">SAP BW는 hello에 인스턴스가 있는 hello 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="cd499-146">string</span><span class="sxs-lookup"><span data-stu-id="cd499-146">string</span></span> | <span data-ttu-id="cd499-147">예</span><span class="sxs-lookup"><span data-stu-id="cd499-147">Yes</span></span>
<span data-ttu-id="cd499-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="cd499-148">systemNumber</span></span> | <span data-ttu-id="cd499-149">Hello SAP BW 시스템의 시스템 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="cd499-150">문자열로 표현되는 두 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="cd499-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="cd499-151">예</span><span class="sxs-lookup"><span data-stu-id="cd499-151">Yes</span></span>
<span data-ttu-id="cd499-152">clientId</span><span class="sxs-lookup"><span data-stu-id="cd499-152">clientId</span></span> | <span data-ttu-id="cd499-153">클라이언트 hello W SAP 시스템에서에서 hello 클라이언트의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="cd499-154">문자열로 표현되는 세 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="cd499-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="cd499-155">예</span><span class="sxs-lookup"><span data-stu-id="cd499-155">Yes</span></span>
<span data-ttu-id="cd499-156">username</span><span class="sxs-lookup"><span data-stu-id="cd499-156">username</span></span> | <span data-ttu-id="cd499-157">Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="cd499-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="cd499-158">string</span><span class="sxs-lookup"><span data-stu-id="cd499-158">string</span></span> | <span data-ttu-id="cd499-159">예</span><span class="sxs-lookup"><span data-stu-id="cd499-159">Yes</span></span>
<span data-ttu-id="cd499-160">암호</span><span class="sxs-lookup"><span data-stu-id="cd499-160">password</span></span> | <span data-ttu-id="cd499-161">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-161">Password for hello user.</span></span> | <span data-ttu-id="cd499-162">string</span><span class="sxs-lookup"><span data-stu-id="cd499-162">string</span></span> | <span data-ttu-id="cd499-163">예</span><span class="sxs-lookup"><span data-stu-id="cd499-163">Yes</span></span>
<span data-ttu-id="cd499-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cd499-164">gatewayName</span></span> | <span data-ttu-id="cd499-165">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP BW 인스턴스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="cd499-166">string</span><span class="sxs-lookup"><span data-stu-id="cd499-166">string</span></span> | <span data-ttu-id="cd499-167">예</span><span class="sxs-lookup"><span data-stu-id="cd499-167">Yes</span></span>
<span data-ttu-id="cd499-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="cd499-168">encryptedCredential</span></span> | <span data-ttu-id="cd499-169">hello 암호화 된 자격 증명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-169">hello encrypted credential string.</span></span> | <span data-ttu-id="cd499-170">string</span><span class="sxs-lookup"><span data-stu-id="cd499-170">string</span></span> | <span data-ttu-id="cd499-171">아니요</span><span class="sxs-lookup"><span data-stu-id="cd499-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="cd499-172">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="cd499-172">Dataset properties</span></span>
<span data-ttu-id="cd499-173">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd499-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cd499-174">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="cd499-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cd499-175">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="cd499-176">형식의 hello SAP BW 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="cd499-177">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="cd499-177">Copy activity properties</span></span>
<span data-ttu-id="cd499-178">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd499-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cd499-179">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="cd499-180">반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cd499-181">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="cd499-182">복사 작업의 원본 유형의 경우 **RelationalSource** (SAP BW 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="cd499-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="cd499-183">속성</span><span class="sxs-lookup"><span data-stu-id="cd499-183">Property</span></span> | <span data-ttu-id="cd499-184">설명</span><span class="sxs-lookup"><span data-stu-id="cd499-184">Description</span></span> | <span data-ttu-id="cd499-185">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="cd499-185">Allowed values</span></span> | <span data-ttu-id="cd499-186">필수</span><span class="sxs-lookup"><span data-stu-id="cd499-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd499-187">쿼리</span><span class="sxs-lookup"><span data-stu-id="cd499-187">query</span></span> | <span data-ttu-id="cd499-188">Hello hello SAP BW 인스턴스에서 MDX 쿼리 tooread 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="cd499-189">MDX 쿼리.</span><span class="sxs-lookup"><span data-stu-id="cd499-189">MDX query.</span></span> | <span data-ttu-id="cd499-190">예</span><span class="sxs-lookup"><span data-stu-id="cd499-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="cd499-191">JSON의 예: SAP Business Warehouse tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="cd499-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="cd499-192">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cd499-193">이 샘플은 어떻게 온-프레미스 SAP Business Warehouse tooan Azure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="cd499-194">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="cd499-195">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="cd499-196">Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="cd499-197">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd499-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="cd499-198">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="cd499-199">[SapBw](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cd499-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="cd499-200">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cd499-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cd499-201">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="cd499-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="cd499-202">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="cd499-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cd499-203">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="cd499-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cd499-204">hello 샘플에 1 시간 마다 SAP Business Warehouse 인스턴스에서 tooan Azure blob에서에서 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="cd499-205">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cd499-206">첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="cd499-207">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd499-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="cd499-208">SAP Business Warehouse 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cd499-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="cd499-209">SAP BW 인스턴스 toohello 데이터 팩터리 서비스 링크 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="cd499-210">hello type 속성이 너무 설정 되어**SapBw**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="cd499-211">hello typeProperties 섹션 hello SAP BW 인스턴스에 대 한 연결 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="cd499-212">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="cd499-212">Azure Storage linked service</span></span>
<span data-ttu-id="cd499-213">Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="cd499-214">hello type 속성이 너무 설정 되어**AzureStorage**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="cd499-215">hello typeProperties 섹션 hello Azure 저장소 계정에 대 한 연결 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="cd499-216">SAP BW 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="cd499-216">SAP BW input dataset</span></span>
<span data-ttu-id="cd499-217">이 데이터 집합 hello SAP Business Warehouse 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="cd499-218">Hello Data Factory 데이터 집합의 hello 유형을 너무 설정**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="cd499-219">현재 SAP BW 데이터 집합에 대한 type별 속성은 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="cd499-220">hello 쿼리 hello 복사 활동 정의에서 어떤 데이터 tooread hello SAP BW 인스턴스에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="cd499-221">외부 속성 tootrue 설정 알리고 hello 데이터 팩터리 서비스 hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="cd499-222">빈도 간격 속성은 hello 일정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="cd499-223">이 경우 hello 데이터를 읽을 hello SAP BW 인스턴스에서 1 시간 마다.</span><span class="sxs-lookup"><span data-stu-id="cd499-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="cd499-224">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="cd499-224">Azure Blob output dataset</span></span>
<span data-ttu-id="cd499-225">이 데이터 집합 hello 출력 Azure Blob 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="cd499-226">hello type 속성이 tooAzureBlob 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="cd499-227">hello typeProperties 섹션 hello SAP BW 인스턴스에서 복사한 hello 데이터 저장 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="cd499-228">hello 데이터 tooa 새 blob 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="cd499-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cd499-229">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cd499-230">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="cd499-231">복사 작업을 포함하는 파이프라인</span><span class="sxs-lookup"><span data-stu-id="cd499-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="cd499-232">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cd499-233">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** (SAP BW 원본)에 대 한 및 **싱크** 형식이 너무 설정**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cd499-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="cd499-234">hello에 대 한 지정 된 hello 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="cd499-235">SAP BW에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="cd499-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="cd499-236">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="cd499-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="cd499-237">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="cd499-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="cd499-238">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="cd499-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="cd499-239">SAP BW에서 데이터를 이동할 때는 다음 매핑을 hello SAP BW 형식 too.NET 형식에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="cd499-240">Hello ABAP 사전 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="cd499-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="cd499-241">.Net 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="cd499-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="cd499-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="cd499-242">ACCP</span></span> |  <span data-ttu-id="cd499-243">int</span><span class="sxs-lookup"><span data-stu-id="cd499-243">Int</span></span>
<span data-ttu-id="cd499-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="cd499-244">CHAR</span></span> | <span data-ttu-id="cd499-245">string</span><span class="sxs-lookup"><span data-stu-id="cd499-245">String</span></span>
<span data-ttu-id="cd499-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="cd499-246">CLNT</span></span> | <span data-ttu-id="cd499-247">string</span><span class="sxs-lookup"><span data-stu-id="cd499-247">String</span></span>
<span data-ttu-id="cd499-248">CURR</span><span class="sxs-lookup"><span data-stu-id="cd499-248">CURR</span></span> | <span data-ttu-id="cd499-249">10진수</span><span class="sxs-lookup"><span data-stu-id="cd499-249">Decimal</span></span>
<span data-ttu-id="cd499-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="cd499-250">CUKY</span></span> | <span data-ttu-id="cd499-251">string</span><span class="sxs-lookup"><span data-stu-id="cd499-251">String</span></span>
<span data-ttu-id="cd499-252">DEC</span><span class="sxs-lookup"><span data-stu-id="cd499-252">DEC</span></span> | <span data-ttu-id="cd499-253">10진수</span><span class="sxs-lookup"><span data-stu-id="cd499-253">Decimal</span></span>
<span data-ttu-id="cd499-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="cd499-254">FLTP</span></span> | <span data-ttu-id="cd499-255">Double</span><span class="sxs-lookup"><span data-stu-id="cd499-255">Double</span></span>
<span data-ttu-id="cd499-256">INT1</span><span class="sxs-lookup"><span data-stu-id="cd499-256">INT1</span></span> | <span data-ttu-id="cd499-257">Byte</span><span class="sxs-lookup"><span data-stu-id="cd499-257">Byte</span></span>
<span data-ttu-id="cd499-258">INT2</span><span class="sxs-lookup"><span data-stu-id="cd499-258">INT2</span></span> | <span data-ttu-id="cd499-259">Int16</span><span class="sxs-lookup"><span data-stu-id="cd499-259">Int16</span></span>
<span data-ttu-id="cd499-260">INT4</span><span class="sxs-lookup"><span data-stu-id="cd499-260">INT4</span></span> | <span data-ttu-id="cd499-261">int</span><span class="sxs-lookup"><span data-stu-id="cd499-261">Int</span></span>
<span data-ttu-id="cd499-262">LANG</span><span class="sxs-lookup"><span data-stu-id="cd499-262">LANG</span></span> | <span data-ttu-id="cd499-263">String</span><span class="sxs-lookup"><span data-stu-id="cd499-263">String</span></span>
<span data-ttu-id="cd499-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="cd499-264">LCHR</span></span> | <span data-ttu-id="cd499-265">String</span><span class="sxs-lookup"><span data-stu-id="cd499-265">String</span></span>
<span data-ttu-id="cd499-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="cd499-266">LRAW</span></span> | <span data-ttu-id="cd499-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cd499-267">Byte[]</span></span>
<span data-ttu-id="cd499-268">PREC</span><span class="sxs-lookup"><span data-stu-id="cd499-268">PREC</span></span> | <span data-ttu-id="cd499-269">Int16</span><span class="sxs-lookup"><span data-stu-id="cd499-269">Int16</span></span>
<span data-ttu-id="cd499-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="cd499-270">QUAN</span></span> | <span data-ttu-id="cd499-271">10진수</span><span class="sxs-lookup"><span data-stu-id="cd499-271">Decimal</span></span>
<span data-ttu-id="cd499-272">RAW</span><span class="sxs-lookup"><span data-stu-id="cd499-272">RAW</span></span> | <span data-ttu-id="cd499-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cd499-273">Byte[]</span></span>
<span data-ttu-id="cd499-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="cd499-274">RAWSTRING</span></span> | <span data-ttu-id="cd499-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cd499-275">Byte[]</span></span>
<span data-ttu-id="cd499-276">STRING</span><span class="sxs-lookup"><span data-stu-id="cd499-276">STRING</span></span> | <span data-ttu-id="cd499-277">String</span><span class="sxs-lookup"><span data-stu-id="cd499-277">String</span></span>
<span data-ttu-id="cd499-278">단위</span><span class="sxs-lookup"><span data-stu-id="cd499-278">UNIT</span></span> | <span data-ttu-id="cd499-279">string</span><span class="sxs-lookup"><span data-stu-id="cd499-279">String</span></span>
<span data-ttu-id="cd499-280">DATS</span><span class="sxs-lookup"><span data-stu-id="cd499-280">DATS</span></span> | <span data-ttu-id="cd499-281">string</span><span class="sxs-lookup"><span data-stu-id="cd499-281">String</span></span>
<span data-ttu-id="cd499-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="cd499-282">NUMC</span></span> | <span data-ttu-id="cd499-283">string</span><span class="sxs-lookup"><span data-stu-id="cd499-283">String</span></span>
<span data-ttu-id="cd499-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="cd499-284">TIMS</span></span> | <span data-ttu-id="cd499-285">문자열</span><span class="sxs-lookup"><span data-stu-id="cd499-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="cd499-286">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="cd499-287">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="cd499-287">Map source toosink columns</span></span>
<span data-ttu-id="cd499-288">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="cd499-289">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="cd499-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="cd499-290">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="cd499-291">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cd499-292">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cd499-293">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="cd499-294">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd499-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cd499-295">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="cd499-295">Performance and Tuning</span></span>
<span data-ttu-id="cd499-296">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cd499-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
