---
title: "데이터 팩터리를 사용 하 여 Cassandra aaaMove 데이터로 | Microsoft Docs"
description: "온-프레미스 Cassandra toomove 데이터로 데이터베이스 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="5c37d-103">Azure Data Factory를 사용하여 온-프레미스 Cassandra 데이터베이스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="5c37d-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="5c37d-104">이 문서에서는 Azure Data Factory toomove 데이터베이스의에서 데이터를 온-프레미스 Cassandra에서 toouse 복사 작업 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="5c37d-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="5c37d-106">온-프레미스 Cassandra 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="5c37d-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5c37d-108">데이터 팩터리는 현재 이동 Cassandra 데이터에서 데이터 저장 tooother 데이터 저장소 뿐만 아니라 다른 데이터 저장소 tooa Cassandra 데이터 저장소에서 데이터 이동에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="5c37d-109">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="5c37d-109">Supported versions</span></span>
<span data-ttu-id="5c37d-110">hello Cassandra 커넥터 버전 Cassandra의 다음 hello는 지원: 2.X 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c37d-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c37d-111">Prerequisites</span></span>
<span data-ttu-id="5c37d-112">Hello Azure Data Factory 서비스 toobe 수 tooconnect tooyour 온-프레미스 Cassandra 데이터베이스에서 데이터 관리 게이트웨이 설치 해야 동일한 컴퓨터 hello 데이터베이스를 호스팅 함 hello에 컴퓨터나 경쟁 hello 사용 하 여 리소스에 대 한 별도 컴퓨터 tooavoid 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="5c37d-113">데이터 관리 게이트웨이 안전 하 고 관리 되는 방식으로 온-프레미스 데이터 원본 toocloud 서비스를 연결 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="5c37d-114">데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="5c37d-115">참조 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 toomove 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="5c37d-116">Hello 데이터베이스가 호스팅되면 hello 클라우드의 예를 들어 Azure IaaS VM의 경우에 hello 게이트웨이 tooconnect tooa Cassandra 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="5c37d-117">Y hello 게이트웨이에 있을 수 있습니다 동일한 VM hello 데이터베이스를 호스팅 함 hello 또는 hello 게이트웨이 별도 VM toohello 데이터베이스 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="5c37d-118">Hello 게이트웨이 설치할 때 자동으로 Microsoft Cassandra ODBC 사용 되는 드라이버 tooconnect tooCassandra 데이터베이스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="5c37d-119">따라서 필요 하지 않습니다 toomanually hello Cassandra 데이터베이스에서 데이터를 복사할 때 hello 게이트웨이 컴퓨터에 모든 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c37d-120">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5c37d-121">시작</span><span class="sxs-lookup"><span data-stu-id="5c37d-121">Getting started</span></span>
<span data-ttu-id="5c37d-122">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5c37d-123">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5c37d-124">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="5c37d-125">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5c37d-126">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5c37d-127">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5c37d-128">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5c37d-129">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5c37d-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5c37d-131">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5c37d-132">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5c37d-133">Data Factory 된 엔터티를 온-프레미스 Cassandra 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: Cassandra tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-cassandra-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="5c37d-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5c37d-134">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa Cassandra 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5c37d-135">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-135">Linked service properties</span></span>
<span data-ttu-id="5c37d-136">다음 표에서 hello JSON 요소 특정 tooCassandra 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="5c37d-137">속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-137">Property</span></span> | <span data-ttu-id="5c37d-138">설명</span><span class="sxs-lookup"><span data-stu-id="5c37d-138">Description</span></span> | <span data-ttu-id="5c37d-139">필수</span><span class="sxs-lookup"><span data-stu-id="5c37d-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c37d-140">type</span><span class="sxs-lookup"><span data-stu-id="5c37d-140">type</span></span> |<span data-ttu-id="5c37d-141">hello type 속성 설정 해야 합니다: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="5c37d-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="5c37d-142">예</span><span class="sxs-lookup"><span data-stu-id="5c37d-142">Yes</span></span> |
| <span data-ttu-id="5c37d-143">host</span><span class="sxs-lookup"><span data-stu-id="5c37d-143">host</span></span> |<span data-ttu-id="5c37d-144">Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.</span><span class="sxs-lookup"><span data-stu-id="5c37d-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="5c37d-145">동시에 IP 주소 또는 호스트 이름 tooconnect tooall 서버의 쉼표로 구분 된 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="5c37d-146">예</span><span class="sxs-lookup"><span data-stu-id="5c37d-146">Yes</span></span> |
| <span data-ttu-id="5c37d-147">포트</span><span class="sxs-lookup"><span data-stu-id="5c37d-147">port</span></span> |<span data-ttu-id="5c37d-148">hello Cassandra 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="5c37d-149">아니요. 기본값: 9042</span><span class="sxs-lookup"><span data-stu-id="5c37d-149">No, default value: 9042</span></span> |
| <span data-ttu-id="5c37d-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5c37d-150">authenticationType</span></span> |<span data-ttu-id="5c37d-151">Basic 또는 Anonymous</span><span class="sxs-lookup"><span data-stu-id="5c37d-151">Basic, or Anonymous</span></span> |<span data-ttu-id="5c37d-152">예</span><span class="sxs-lookup"><span data-stu-id="5c37d-152">Yes</span></span> |
| <span data-ttu-id="5c37d-153">username</span><span class="sxs-lookup"><span data-stu-id="5c37d-153">username</span></span> |<span data-ttu-id="5c37d-154">Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="5c37d-155">예, authenticationType tooBasic 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="5c37d-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="5c37d-156">암호</span><span class="sxs-lookup"><span data-stu-id="5c37d-156">password</span></span> |<span data-ttu-id="5c37d-157">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-157">Specify password for hello user account.</span></span> |<span data-ttu-id="5c37d-158">예, authenticationType tooBasic 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="5c37d-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="5c37d-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5c37d-159">gatewayName</span></span> |<span data-ttu-id="5c37d-160">데이터베이스가 사용 되는 tooconnect toohello 온-프레미스 Cassandra hello 게이트웨이의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="5c37d-161">예</span><span class="sxs-lookup"><span data-stu-id="5c37d-161">Yes</span></span> |
| <span data-ttu-id="5c37d-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="5c37d-162">encryptedCredential</span></span> |<span data-ttu-id="5c37d-163">Hello 게이트웨이로 암호화 된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="5c37d-164">아니요</span><span class="sxs-lookup"><span data-stu-id="5c37d-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5c37d-165">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-165">Dataset properties</span></span>
<span data-ttu-id="5c37d-166">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5c37d-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5c37d-167">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="5c37d-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5c37d-168">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5c37d-169">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **CassandraTable** hello 다음과 같은 속성에</span><span class="sxs-lookup"><span data-stu-id="5c37d-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="5c37d-170">속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-170">Property</span></span> | <span data-ttu-id="5c37d-171">설명</span><span class="sxs-lookup"><span data-stu-id="5c37d-171">Description</span></span> | <span data-ttu-id="5c37d-172">필수</span><span class="sxs-lookup"><span data-stu-id="5c37d-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c37d-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="5c37d-173">keyspace</span></span> |<span data-ttu-id="5c37d-174">키 스페이스 hello 또는 Cassandra 데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="5c37d-175">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="5c37d-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="5c37d-176">tableName</span><span class="sxs-lookup"><span data-stu-id="5c37d-176">tableName</span></span> |<span data-ttu-id="5c37d-177">Hello Cassandra 데이터베이스 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="5c37d-178">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="5c37d-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5c37d-179">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-179">Copy activity properties</span></span>
<span data-ttu-id="5c37d-180">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5c37d-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5c37d-181">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5c37d-182">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="5c37d-183">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5c37d-184">원본 유형의 경우 **CassandraSource**, 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="5c37d-185">속성</span><span class="sxs-lookup"><span data-stu-id="5c37d-185">Property</span></span> | <span data-ttu-id="5c37d-186">설명</span><span class="sxs-lookup"><span data-stu-id="5c37d-186">Description</span></span> | <span data-ttu-id="5c37d-187">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="5c37d-187">Allowed values</span></span> | <span data-ttu-id="5c37d-188">필수</span><span class="sxs-lookup"><span data-stu-id="5c37d-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5c37d-189">쿼리</span><span class="sxs-lookup"><span data-stu-id="5c37d-189">query</span></span> |<span data-ttu-id="5c37d-190">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="5c37d-191">SQL-92 쿼리 또는 CQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="5c37d-192">[CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="5c37d-193">SQL 쿼리를 사용할 때 지정 **키 스페이스 name.table 이름** tooquery 원하는 toorepresent hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="5c37d-194">아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우)</span><span class="sxs-lookup"><span data-stu-id="5c37d-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="5c37d-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="5c37d-195">consistencyLevel</span></span> |<span data-ttu-id="5c37d-196">hello 일관성 수준이 지정 복제 개수 데이터 toohello 클라이언트 응용 프로그램을 반환 하기 전에 tooa 읽기 요청 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="5c37d-197">Cassandra 검사 읽기 요청을 데이터 toosatisfy hello에 대 한 복제본의 지정 된 수를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="5c37d-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="5c37d-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="5c37d-199">자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="5c37d-200">아니요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-200">No.</span></span> <span data-ttu-id="5c37d-201">기본값은 ONE입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="5c37d-202">JSON의 예: Cassandra tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="5c37d-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="5c37d-203">이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5c37d-204">온-프레미스 Cassandra toocopy 데이터로 데이터베이스 tooan Azure Blob 저장소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="5c37d-205">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c37d-206">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="5c37d-207">Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="5c37d-208">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="5c37d-209">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="5c37d-210">[OnPremisesCassandra](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="5c37d-211">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="5c37d-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5c37d-212">[CassandraTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="5c37d-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="5c37d-213">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="5c37d-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5c37d-214">[CassandraSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="5c37d-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5c37d-215">**Cassandra 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="5c37d-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="5c37d-216">이 예에서는 hello **Cassandra** 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="5c37d-217">참조 [Cassandra 연결 된 서비스](#linked-service-properties) 이 연결 된 서비스에서 지 원하는 hello 속성에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="5c37d-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="5c37d-218">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="5c37d-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="5c37d-219">**Cassandra 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="5c37d-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="5c37d-220">설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="5c37d-221">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="5c37d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5c37d-222">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="5c37d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="5c37d-223">**Cassandra 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="5c37d-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="5c37d-224">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="5c37d-225">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**CassandraSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="5c37d-226">참조 [RelationalSource 형식 속성](#copy-activity-properties) hello 목록이 hello RelationalSource에서 지 원하는 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="5c37d-227">Cassandra에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="5c37d-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="5c37d-228">Cassandra 형식</span><span class="sxs-lookup"><span data-stu-id="5c37d-228">Cassandra Type</span></span> | <span data-ttu-id="5c37d-229">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="5c37d-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="5c37d-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="5c37d-230">ASCII</span></span> |<span data-ttu-id="5c37d-231">문자열</span><span class="sxs-lookup"><span data-stu-id="5c37d-231">String</span></span> |
| <span data-ttu-id="5c37d-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="5c37d-232">BIGINT</span></span> |<span data-ttu-id="5c37d-233">Int64</span><span class="sxs-lookup"><span data-stu-id="5c37d-233">Int64</span></span> |
| <span data-ttu-id="5c37d-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="5c37d-234">BLOB</span></span> |<span data-ttu-id="5c37d-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5c37d-235">Byte[]</span></span> |
| <span data-ttu-id="5c37d-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="5c37d-236">BOOLEAN</span></span> |<span data-ttu-id="5c37d-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="5c37d-237">Boolean</span></span> |
| <span data-ttu-id="5c37d-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5c37d-238">DECIMAL</span></span> |<span data-ttu-id="5c37d-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5c37d-239">Decimal</span></span> |
| <span data-ttu-id="5c37d-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="5c37d-240">DOUBLE</span></span> |<span data-ttu-id="5c37d-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="5c37d-241">Double</span></span> |
| <span data-ttu-id="5c37d-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="5c37d-242">FLOAT</span></span> |<span data-ttu-id="5c37d-243">단일</span><span class="sxs-lookup"><span data-stu-id="5c37d-243">Single</span></span> |
| <span data-ttu-id="5c37d-244">INET</span><span class="sxs-lookup"><span data-stu-id="5c37d-244">INET</span></span> |<span data-ttu-id="5c37d-245">문자열</span><span class="sxs-lookup"><span data-stu-id="5c37d-245">String</span></span> |
| <span data-ttu-id="5c37d-246">INT</span><span class="sxs-lookup"><span data-stu-id="5c37d-246">INT</span></span> |<span data-ttu-id="5c37d-247">Int32</span><span class="sxs-lookup"><span data-stu-id="5c37d-247">Int32</span></span> |
| <span data-ttu-id="5c37d-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="5c37d-248">TEXT</span></span> |<span data-ttu-id="5c37d-249">문자열</span><span class="sxs-lookup"><span data-stu-id="5c37d-249">String</span></span> |
| <span data-ttu-id="5c37d-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="5c37d-250">TIMESTAMP</span></span> |<span data-ttu-id="5c37d-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="5c37d-251">DateTime</span></span> |
| <span data-ttu-id="5c37d-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="5c37d-252">TIMEUUID</span></span> |<span data-ttu-id="5c37d-253">Guid</span><span class="sxs-lookup"><span data-stu-id="5c37d-253">Guid</span></span> |
| <span data-ttu-id="5c37d-254">UUID</span><span class="sxs-lookup"><span data-stu-id="5c37d-254">UUID</span></span> |<span data-ttu-id="5c37d-255">Guid</span><span class="sxs-lookup"><span data-stu-id="5c37d-255">Guid</span></span> |
| <span data-ttu-id="5c37d-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="5c37d-256">VARCHAR</span></span> |<span data-ttu-id="5c37d-257">문자열</span><span class="sxs-lookup"><span data-stu-id="5c37d-257">String</span></span> |
| <span data-ttu-id="5c37d-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="5c37d-258">VARINT</span></span> |<span data-ttu-id="5c37d-259">10진수</span><span class="sxs-lookup"><span data-stu-id="5c37d-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="5c37d-260">컬렉션에 대 한 형식은 (지도, 집합, 목록, 등)를 참조 너무[가상 테이블을 사용 하 여 Cassandra 컬렉션 형식을 사용할](#work-with-collections-using-virtual-table) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5c37d-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="5c37d-261">사용자 정의 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="5c37d-262">hello 길이의 이진 열과 문자열 열 길이가 4000 보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="5c37d-263">가상 테이블을 사용하여 컬렉션으로 작업</span><span class="sxs-lookup"><span data-stu-id="5c37d-263">Work with collections using virtual table</span></span>
<span data-ttu-id="5c37d-264">Azure 데이터 팩터리는 기본 제공 ODBC 드라이버 tooconnect tooand에서에서 데이터 복사 Cassandra 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="5c37d-265">목록, 집합 및 맵을 포함 하는 컬렉션 형식에 대해 hello 드라이버를 해당 가상 테이블로 구하고 hello 데이터 다시 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="5c37d-266">특히, 컬렉션 열이 포함 된 테이블, hello 드라이버 hello 다음 가상 표를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="5c37d-267">A **기본 테이블**, 포함 된 hello hello 컬렉션 열 제외 하 고 실제 테이블 hello와 동일한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="5c37d-268">hello 기본 테이블 표시 되는 hello 실제 테이블 hello 이름과 같은 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="5c37d-269">A **가상 테이블** hello 중첩 된 데이터 확장 되는 각 컬렉션 열에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="5c37d-270">구분 기호, hello 실제 테이블의 hello 이름을 사용 하 여 컬렉션을 나타내는 hello 가상 테이블 이름의 "*vt*" 및 hello hello 열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="5c37d-271">가상 테이블 참조 toohello hello 실제 테이블에는 데이터, 사용할 수 있도록 hello 드라이버 tooaccess hello 비 정규화 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="5c37d-272">자세한 내용은 예제 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-272">See Example section for details.</span></span> <span data-ttu-id="5c37d-273">Cassandra 컬렉션의 내용을 hello 쿼리 한 hello 가상 테이블을 조인 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="5c37d-274">Hello를 사용할 수 있습니다 [복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively hello 가상 테이블을 포함 한 Cassandra 데이터베이스에서 테이블 목록을 hello 뷰와 내부 hello 데이터를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="5c37d-275">Hello 복사 마법사에서에서 쿼리를 작성 하 고 toosee hello 결과 유효성을 검사 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="5c37d-276">예제</span><span class="sxs-lookup"><span data-stu-id="5c37d-276">Example</span></span>
<span data-ttu-id="5c37d-277">예를 들어 hello ExampleTable"다음"은 정수 기본 키 열 이름은 "pk_int", value 라는 텍스트 열, 목록의 열, 열 매핑 ("StringSet" 라고 함) 집합 열이 포함 된 Cassandra 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="5c37d-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="5c37d-278">pk_int</span></span> | <span data-ttu-id="5c37d-279">값</span><span class="sxs-lookup"><span data-stu-id="5c37d-279">Value</span></span> | <span data-ttu-id="5c37d-280">나열</span><span class="sxs-lookup"><span data-stu-id="5c37d-280">List</span></span> | <span data-ttu-id="5c37d-281">Map</span><span class="sxs-lookup"><span data-stu-id="5c37d-281">Map</span></span> | <span data-ttu-id="5c37d-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="5c37d-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5c37d-283">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-283">1</span></span> |<span data-ttu-id="5c37d-284">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="5c37d-284">"sample value 1"</span></span> |<span data-ttu-id="5c37d-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="5c37d-285">["1", "2", "3"]</span></span> |<span data-ttu-id="5c37d-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="5c37d-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="5c37d-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="5c37d-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="5c37d-288">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-288">3</span></span> |<span data-ttu-id="5c37d-289">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="5c37d-289">"sample value 3"</span></span> |<span data-ttu-id="5c37d-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="5c37d-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="5c37d-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="5c37d-291">{"S1": "t"}</span></span> |<span data-ttu-id="5c37d-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="5c37d-292">{"A", "E"}</span></span> |

<span data-ttu-id="5c37d-293">hello 드라이버는이 단일 표에 여러 가상 테이블 toorepresent 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="5c37d-294">hello hello 가상 테이블의 외래 키 열 hello hello real 테이블의 기본 키 열을 참조 하 고는 실시간 표시 테이블 행 hello 가상 테이블 행에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="5c37d-295">hello 첫 번째 가상 테이블은 hello 라는 "ExampleTable"는 기본 테이블은 다음 표에 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="5c37d-296">hello hello 기본 테이블에 포함 되어이 테이블에서 생략 하 고 다른 가상 테이블에서 확장 되는 hello 컬렉션을 제외 하 고 원본 데이터베이스 테이블 hello와 동일한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="5c37d-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="5c37d-297">pk_int</span></span> | <span data-ttu-id="5c37d-298">값</span><span class="sxs-lookup"><span data-stu-id="5c37d-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5c37d-299">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-299">1</span></span> |<span data-ttu-id="5c37d-300">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="5c37d-300">"sample value 1"</span></span> |
| <span data-ttu-id="5c37d-301">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-301">3</span></span> |<span data-ttu-id="5c37d-302">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="5c37d-302">"sample value 3"</span></span> |

<span data-ttu-id="5c37d-303">hello 다음 표에서 보여 hello 열의 데이터를 hello 목록, 지도 및 StringSet renormalize hello 가상 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="5c37d-304">"_index" 또는 "(_k)"로 끝나는 이름의 hello 열 hello 원래 목록 또는 맵 내 hello 데이터 hello 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="5c37d-305">"_value"로 끝나는 이름의 hello 열 hello 컬렉션에서 hello 확장 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="5c37d-306">테이블 "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="5c37d-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="5c37d-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="5c37d-307">pk_int</span></span> | <span data-ttu-id="5c37d-308">List_index</span><span class="sxs-lookup"><span data-stu-id="5c37d-308">List_index</span></span> | <span data-ttu-id="5c37d-309">List_value</span><span class="sxs-lookup"><span data-stu-id="5c37d-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c37d-310">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-310">1</span></span> |<span data-ttu-id="5c37d-311">0</span><span class="sxs-lookup"><span data-stu-id="5c37d-311">0</span></span> |<span data-ttu-id="5c37d-312">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-312">1</span></span> |
| <span data-ttu-id="5c37d-313">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-313">1</span></span> |<span data-ttu-id="5c37d-314">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-314">1</span></span> |<span data-ttu-id="5c37d-315">2</span><span class="sxs-lookup"><span data-stu-id="5c37d-315">2</span></span> |
| <span data-ttu-id="5c37d-316">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-316">1</span></span> |<span data-ttu-id="5c37d-317">2</span><span class="sxs-lookup"><span data-stu-id="5c37d-317">2</span></span> |<span data-ttu-id="5c37d-318">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-318">3</span></span> |
| <span data-ttu-id="5c37d-319">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-319">3</span></span> |<span data-ttu-id="5c37d-320">0</span><span class="sxs-lookup"><span data-stu-id="5c37d-320">0</span></span> |<span data-ttu-id="5c37d-321">100</span><span class="sxs-lookup"><span data-stu-id="5c37d-321">100</span></span> |
| <span data-ttu-id="5c37d-322">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-322">3</span></span> |<span data-ttu-id="5c37d-323">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-323">1</span></span> |<span data-ttu-id="5c37d-324">101</span><span class="sxs-lookup"><span data-stu-id="5c37d-324">101</span></span> |
| <span data-ttu-id="5c37d-325">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-325">3</span></span> |<span data-ttu-id="5c37d-326">2</span><span class="sxs-lookup"><span data-stu-id="5c37d-326">2</span></span> |<span data-ttu-id="5c37d-327">102</span><span class="sxs-lookup"><span data-stu-id="5c37d-327">102</span></span> |
| <span data-ttu-id="5c37d-328">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-328">3</span></span> |<span data-ttu-id="5c37d-329">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-329">3</span></span> |<span data-ttu-id="5c37d-330">103</span><span class="sxs-lookup"><span data-stu-id="5c37d-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="5c37d-331">테이블 “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="5c37d-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="5c37d-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="5c37d-332">pk_int</span></span> | <span data-ttu-id="5c37d-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="5c37d-333">Map_key</span></span> | <span data-ttu-id="5c37d-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="5c37d-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c37d-335">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-335">1</span></span> |<span data-ttu-id="5c37d-336">S1</span><span class="sxs-lookup"><span data-stu-id="5c37d-336">S1</span></span> |<span data-ttu-id="5c37d-337">A</span><span class="sxs-lookup"><span data-stu-id="5c37d-337">A</span></span> |
| <span data-ttu-id="5c37d-338">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-338">1</span></span> |<span data-ttu-id="5c37d-339">S2</span><span class="sxs-lookup"><span data-stu-id="5c37d-339">S2</span></span> |<span data-ttu-id="5c37d-340">b</span><span class="sxs-lookup"><span data-stu-id="5c37d-340">b</span></span> |
| <span data-ttu-id="5c37d-341">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-341">3</span></span> |<span data-ttu-id="5c37d-342">S1</span><span class="sxs-lookup"><span data-stu-id="5c37d-342">S1</span></span> |<span data-ttu-id="5c37d-343">t</span><span class="sxs-lookup"><span data-stu-id="5c37d-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="5c37d-344">테이블 “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="5c37d-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="5c37d-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="5c37d-345">pk_int</span></span> | <span data-ttu-id="5c37d-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="5c37d-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="5c37d-347">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-347">1</span></span> |<span data-ttu-id="5c37d-348">A</span><span class="sxs-lookup"><span data-stu-id="5c37d-348">A</span></span> |
| <span data-ttu-id="5c37d-349">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-349">1</span></span> |<span data-ttu-id="5c37d-350">b</span><span class="sxs-lookup"><span data-stu-id="5c37d-350">B</span></span> |
| <span data-ttu-id="5c37d-351">1</span><span class="sxs-lookup"><span data-stu-id="5c37d-351">1</span></span> |<span data-ttu-id="5c37d-352">C</span><span class="sxs-lookup"><span data-stu-id="5c37d-352">C</span></span> |
| <span data-ttu-id="5c37d-353">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-353">3</span></span> |<span data-ttu-id="5c37d-354">A</span><span class="sxs-lookup"><span data-stu-id="5c37d-354">A</span></span> |
| <span data-ttu-id="5c37d-355">3</span><span class="sxs-lookup"><span data-stu-id="5c37d-355">3</span></span> |<span data-ttu-id="5c37d-356">E</span><span class="sxs-lookup"><span data-stu-id="5c37d-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="5c37d-357">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="5c37d-357">Map source toosink columns</span></span>
<span data-ttu-id="5c37d-358">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5c37d-359">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="5c37d-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="5c37d-360">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5c37d-361">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5c37d-362">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5c37d-363">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5c37d-364">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c37d-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5c37d-365">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="5c37d-365">Performance and Tuning</span></span>
<span data-ttu-id="5c37d-366">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5c37d-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
