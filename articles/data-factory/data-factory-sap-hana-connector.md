---
title: "aaaMove 데이터를 Azure 데이터 팩터리를 사용 하 여 SAP HANA | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 SAP HANA의 toomove 데이터입니다."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="a908e-103">Azure Data Factory를 사용하여 SAP HANA에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="a908e-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="a908e-104">이 문서에서는 Azure Data Factory toomove 데이터는 온-프레미스 SAP HANA에 있는 toouse 복사 작업 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="a908e-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a908e-106">온-프레미스 SAP HANA 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="a908e-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a908e-108">데이터 팩터리의 현재만 지 원하는 데이터를 SAP HANA tooother 데이터에서에서 저장 하지 않은 이동 tooan SAP HANA 저장소 다른 데이터에서 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="a908e-109">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="a908e-109">Supported versions and installation</span></span>
<span data-ttu-id="a908e-110">이 커넥터는 모든 버전의 SAP HANA 데이터베이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="a908e-111">SQL 쿼리를 사용한 행/열 테이블 및 HANA 정보 모델(예: 분석 및 계산 보기)의 데이터 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="a908e-112">tooenable hello 연결 toohello SAP HANA 인스턴스는 다음과 같은 구성 요소가 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="a908e-113">**데이터 관리 게이트웨이**: Data Factory 서비스가 지 원하는 tooon 온-프레미스 데이터 연결 (포함 하 여 SAP HANA) 저장소 데이터 관리 게이트웨이 라는 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="a908e-114">데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 toolearn 참조 [toocloud 데이터 저장소를 저장 하는 온-프레미스 데이터 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a908e-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="a908e-115">게이트웨이 SAP HANA hello Azure IaaS 가상 컴퓨터 (VM)에서 호스팅되는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="a908e-116">동일한 VM hello 데이터로 저장 하거나 hello 게이트웨이 다른 VM에 연결할 수 toohello 데이터베이스 hello에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="a908e-117">**SAP HANA ODBC 드라이버** hello 게이트웨이 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="a908e-118">Hello에서 hello SAP HANA ODBC 드라이버를 다운로드할 수 있습니다 [SAP 소프트웨어 다운로드 센터](https://support.sap.com/swdc)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="a908e-119">Hello 키워드를 사용 하 여 검색 **SAP HANA CLIENT for Windows**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="a908e-120">시작</span><span class="sxs-lookup"><span data-stu-id="a908e-120">Getting started</span></span>
<span data-ttu-id="a908e-121">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a908e-122">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a908e-123">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="a908e-124">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a908e-125">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a908e-126">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a908e-127">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a908e-128">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a908e-129">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a908e-130">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a908e-131">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a908e-132">Data Factory 된 엔터티를 사용 하는 toocopy 데이터를 온-프레미스 SAP HANA에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: SAP HANA tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-sap-hana-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a908e-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a908e-133">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooan SAP HANA 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a908e-134">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="a908e-134">Linked service properties</span></span>
<span data-ttu-id="a908e-135">다음 표에서 hello JSON 요소 특정 tooSAP HANA에 대 한 연결 된 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="a908e-136">속성</span><span class="sxs-lookup"><span data-stu-id="a908e-136">Property</span></span> | <span data-ttu-id="a908e-137">설명</span><span class="sxs-lookup"><span data-stu-id="a908e-137">Description</span></span> | <span data-ttu-id="a908e-138">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="a908e-138">Allowed values</span></span> | <span data-ttu-id="a908e-139">필수</span><span class="sxs-lookup"><span data-stu-id="a908e-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="a908e-140">server</span><span class="sxs-lookup"><span data-stu-id="a908e-140">server</span></span> | <span data-ttu-id="a908e-141">SAP HANA는 hello에 인스턴스가 있는 hello 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="a908e-142">서버에서 사용자 지정된 포트를 사용하는 경우 `server:port`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="a908e-143">string</span><span class="sxs-lookup"><span data-stu-id="a908e-143">string</span></span> | <span data-ttu-id="a908e-144">예</span><span class="sxs-lookup"><span data-stu-id="a908e-144">Yes</span></span>
<span data-ttu-id="a908e-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a908e-145">authenticationType</span></span> | <span data-ttu-id="a908e-146">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-146">Type of authentication.</span></span> | <span data-ttu-id="a908e-147">string.</span><span class="sxs-lookup"><span data-stu-id="a908e-147">string.</span></span> <span data-ttu-id="a908e-148">"Basic" 또는 "Windows"</span><span class="sxs-lookup"><span data-stu-id="a908e-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="a908e-149">예</span><span class="sxs-lookup"><span data-stu-id="a908e-149">Yes</span></span> 
<span data-ttu-id="a908e-150">username</span><span class="sxs-lookup"><span data-stu-id="a908e-150">username</span></span> | <span data-ttu-id="a908e-151">Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="a908e-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="a908e-152">string</span><span class="sxs-lookup"><span data-stu-id="a908e-152">string</span></span> | <span data-ttu-id="a908e-153">예</span><span class="sxs-lookup"><span data-stu-id="a908e-153">Yes</span></span>
<span data-ttu-id="a908e-154">암호</span><span class="sxs-lookup"><span data-stu-id="a908e-154">password</span></span> | <span data-ttu-id="a908e-155">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-155">Password for hello user.</span></span> | <span data-ttu-id="a908e-156">string</span><span class="sxs-lookup"><span data-stu-id="a908e-156">string</span></span> | <span data-ttu-id="a908e-157">예</span><span class="sxs-lookup"><span data-stu-id="a908e-157">Yes</span></span>
<span data-ttu-id="a908e-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a908e-158">gatewayName</span></span> | <span data-ttu-id="a908e-159">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP HANA 인스턴스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="a908e-160">string</span><span class="sxs-lookup"><span data-stu-id="a908e-160">string</span></span> | <span data-ttu-id="a908e-161">예</span><span class="sxs-lookup"><span data-stu-id="a908e-161">Yes</span></span>
<span data-ttu-id="a908e-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a908e-162">encryptedCredential</span></span> | <span data-ttu-id="a908e-163">hello 암호화 된 자격 증명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-163">hello encrypted credential string.</span></span> | <span data-ttu-id="a908e-164">string</span><span class="sxs-lookup"><span data-stu-id="a908e-164">string</span></span> | <span data-ttu-id="a908e-165">아니요</span><span class="sxs-lookup"><span data-stu-id="a908e-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="a908e-166">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="a908e-166">Dataset properties</span></span>
<span data-ttu-id="a908e-167">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a908e-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a908e-168">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="a908e-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a908e-169">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a908e-170">형식의 hello SAP HANA 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="a908e-171">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="a908e-171">Copy activity properties</span></span>
<span data-ttu-id="a908e-172">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a908e-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a908e-173">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="a908e-174">반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a908e-175">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a908e-176">복사 작업의 원본 유형의 경우 **RelationalSource** (SAP HANA 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="a908e-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a908e-177">속성</span><span class="sxs-lookup"><span data-stu-id="a908e-177">Property</span></span> | <span data-ttu-id="a908e-178">설명</span><span class="sxs-lookup"><span data-stu-id="a908e-178">Description</span></span> | <span data-ttu-id="a908e-179">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="a908e-179">Allowed values</span></span> | <span data-ttu-id="a908e-180">필수</span><span class="sxs-lookup"><span data-stu-id="a908e-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a908e-181">쿼리</span><span class="sxs-lookup"><span data-stu-id="a908e-181">query</span></span> | <span data-ttu-id="a908e-182">Hello SAP HANA 인스턴스에서 hello SQL 쿼리 tooread 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="a908e-183">SQL 쿼리.</span><span class="sxs-lookup"><span data-stu-id="a908e-183">SQL query.</span></span> | <span data-ttu-id="a908e-184">예</span><span class="sxs-lookup"><span data-stu-id="a908e-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="a908e-185">JSON의 예: SAP HANA tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="a908e-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="a908e-186">hello 다음 예제에서는 제공 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a908e-187">이 샘플은 어떻게 온-프레미스 SAP HANA tooan Azure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="a908e-188">그러나 데이터를 복사할 수 있습니다 **직접** 나열 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a908e-189">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="a908e-190">Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="a908e-191">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a908e-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="a908e-192">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="a908e-193">[SapHana](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a908e-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="a908e-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a908e-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a908e-195">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="a908e-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a908e-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="a908e-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a908e-197">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="a908e-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a908e-198">hello 샘플에 1 시간 마다 SAP HANA 인스턴스 tooan Azure blob에서에서 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="a908e-199">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a908e-200">첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="a908e-201">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a908e-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="a908e-202">SAP HANA 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a908e-202">SAP HANA linked service</span></span>
<span data-ttu-id="a908e-203">SAP HANA 인스턴스 toohello 데이터 팩터리 서비스 링크 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="a908e-204">hello type 속성이 너무 설정 되어**SapHana**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="a908e-205">hello typeProperties 섹션 hello SAP HANA 인스턴스에 대 한 연결 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="a908e-206">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a908e-206">Azure Storage linked service</span></span>
<span data-ttu-id="a908e-207">Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="a908e-208">hello type 속성이 너무 설정 되어**AzureStorage**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="a908e-209">hello typeProperties 섹션 hello Azure 저장소 계정에 대 한 연결 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="a908e-210">SAP HANA 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="a908e-210">SAP HANA input dataset</span></span>

<span data-ttu-id="a908e-211">이 데이터 집합 hello SAP HANA 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="a908e-212">Hello Data Factory 데이터 집합의 hello 유형을 너무 설정**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="a908e-213">현재 SAP HANA 데이터 집합에 대한 type별 속성은 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="a908e-214">hello 쿼리 hello 복사 활동 정의에서 어떤 데이터 tooread hello SAP HANA 인스턴스에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="a908e-215">외부 속성 tootrue 설정 알리고 hello 데이터 팩터리 서비스 hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="a908e-216">빈도 간격 속성은 hello 일정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="a908e-217">이 경우 hello 데이터를 읽을 hello SAP HANA 인스턴스에서 1 시간 마다.</span><span class="sxs-lookup"><span data-stu-id="a908e-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a908e-218">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="a908e-218">Azure Blob output dataset</span></span>
<span data-ttu-id="a908e-219">이 데이터 집합 hello 출력 Azure Blob 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="a908e-220">hello type 속성이 tooAzureBlob 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="a908e-221">hello typeProperties 섹션 hello SAP HANA 인스턴스에서 복사한 hello 데이터 저장 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="a908e-222">hello 데이터 tooa 새 blob 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="a908e-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a908e-223">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a908e-224">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="a908e-225">복사 작업을 포함하는 파이프라인</span><span class="sxs-lookup"><span data-stu-id="a908e-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="a908e-226">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a908e-227">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** (SAP HANA 소스)에 대 한 및 **싱크** 형식이 너무 설정**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a908e-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a908e-228">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="a908e-229">SAP HANA에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="a908e-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="a908e-230">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="a908e-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="a908e-231">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="a908e-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a908e-232">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="a908e-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a908e-233">SAP HANA에서 데이터를 이동할 때는 다음 매핑을 hello SAP HANA 형식 too.NET 형식에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="a908e-234">SAP HANA 형식</span><span class="sxs-lookup"><span data-stu-id="a908e-234">SAP HANA Type</span></span> | <span data-ttu-id="a908e-235">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="a908e-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="a908e-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="a908e-236">TINYINT</span></span> | <span data-ttu-id="a908e-237">Byte</span><span class="sxs-lookup"><span data-stu-id="a908e-237">Byte</span></span>
<span data-ttu-id="a908e-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a908e-238">SMALLINT</span></span> | <span data-ttu-id="a908e-239">Int16</span><span class="sxs-lookup"><span data-stu-id="a908e-239">Int16</span></span>
<span data-ttu-id="a908e-240">INT</span><span class="sxs-lookup"><span data-stu-id="a908e-240">INT</span></span> | <span data-ttu-id="a908e-241">Int32</span><span class="sxs-lookup"><span data-stu-id="a908e-241">Int32</span></span>
<span data-ttu-id="a908e-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="a908e-242">BIGINT</span></span> | <span data-ttu-id="a908e-243">Int64</span><span class="sxs-lookup"><span data-stu-id="a908e-243">Int64</span></span>
<span data-ttu-id="a908e-244">Real</span><span class="sxs-lookup"><span data-stu-id="a908e-244">REAL</span></span> | <span data-ttu-id="a908e-245">단일</span><span class="sxs-lookup"><span data-stu-id="a908e-245">Single</span></span>
<span data-ttu-id="a908e-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="a908e-246">DOUBLE</span></span> | <span data-ttu-id="a908e-247">단일</span><span class="sxs-lookup"><span data-stu-id="a908e-247">Single</span></span>
<span data-ttu-id="a908e-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="a908e-248">DECIMAL</span></span> | <span data-ttu-id="a908e-249">10진수</span><span class="sxs-lookup"><span data-stu-id="a908e-249">Decimal</span></span>
<span data-ttu-id="a908e-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="a908e-250">BOOLEAN</span></span> | <span data-ttu-id="a908e-251">Byte</span><span class="sxs-lookup"><span data-stu-id="a908e-251">Byte</span></span>
<span data-ttu-id="a908e-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="a908e-252">VARCHAR</span></span> | <span data-ttu-id="a908e-253">문자열</span><span class="sxs-lookup"><span data-stu-id="a908e-253">String</span></span>
<span data-ttu-id="a908e-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="a908e-254">NVARCHAR</span></span> | <span data-ttu-id="a908e-255">string</span><span class="sxs-lookup"><span data-stu-id="a908e-255">String</span></span>
<span data-ttu-id="a908e-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="a908e-256">CLOB</span></span> | <span data-ttu-id="a908e-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a908e-257">Byte[]</span></span>
<span data-ttu-id="a908e-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="a908e-258">ALPHANUM</span></span> | <span data-ttu-id="a908e-259">문자열</span><span class="sxs-lookup"><span data-stu-id="a908e-259">String</span></span>
<span data-ttu-id="a908e-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="a908e-260">BLOB</span></span> | <span data-ttu-id="a908e-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a908e-261">Byte[]</span></span>
<span data-ttu-id="a908e-262">DATE</span><span class="sxs-lookup"><span data-stu-id="a908e-262">DATE</span></span> | <span data-ttu-id="a908e-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="a908e-263">DateTime</span></span>
<span data-ttu-id="a908e-264">TIME</span><span class="sxs-lookup"><span data-stu-id="a908e-264">TIME</span></span> | <span data-ttu-id="a908e-265">timespan</span><span class="sxs-lookup"><span data-stu-id="a908e-265">TimeSpan</span></span>
<span data-ttu-id="a908e-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="a908e-266">TIMESTAMP</span></span> | <span data-ttu-id="a908e-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="a908e-267">DateTime</span></span>
<span data-ttu-id="a908e-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="a908e-268">SECONDDATE</span></span> | <span data-ttu-id="a908e-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="a908e-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="a908e-270">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="a908e-270">Known limitations</span></span>
<span data-ttu-id="a908e-271">SAP HANA에서 데이터를 복사하는 경우 몇 가지 알려진 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="a908e-272">NVARCHAR 문자열은 잘림된 toomaximum 길이 4000 유니코드 문자</span><span class="sxs-lookup"><span data-stu-id="a908e-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="a908e-273">SMALLDECIMAL은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="a908e-274">VARBINARY는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="a908e-275">유효한 날짜는 1899/12/30 ~ 9999/12/31입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="a908e-276">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="a908e-276">Map source toosink columns</span></span>
<span data-ttu-id="a908e-277">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a908e-278">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="a908e-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="a908e-279">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="a908e-280">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a908e-281">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a908e-282">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a908e-283">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a908e-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a908e-284">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="a908e-284">Performance and Tuning</span></span>
<span data-ttu-id="a908e-285">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a908e-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
