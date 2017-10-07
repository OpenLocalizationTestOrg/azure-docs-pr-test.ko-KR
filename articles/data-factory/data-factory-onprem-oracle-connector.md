---
title: "데이터 팩터리를 사용 하 여 Oracle에서 데이터를 aaaCopy | Microsoft Docs"
description: "어떻게 toocopy 있는 Oracle 데이터베이스에서 온-프레미스 데이터 Azure 데이터 팩터리를 사용 하 여에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="0cf3b-103">Azure Data Factory를 사용하여 온-프레미스 Oracle 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="0cf3b-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="0cf3b-104">이 문서에서는 toouse 온-프레미스 Oracle 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="0cf3b-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="0cf3b-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="0cf3b-106">Supported scenarios</span></span>
<span data-ttu-id="0cf3b-107">데이터를 복사할 수 **Oracle 데이터베이스에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="0cf3b-108">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooan Oracle 데이터베이스**:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="0cf3b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0cf3b-109">Prerequisites</span></span>
<span data-ttu-id="0cf3b-110">데이터 팩터리 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 Oracle 원본을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="0cf3b-111">참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 데이터 관리 게이트웨이에 대 한 문서 toolearn 및 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 설정 toomove 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="0cf3b-112">게이트웨이 hello Oracle에서에서 호스팅되는 Azure IaaS VM 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="0cf3b-113">Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="0cf3b-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0cf3b-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="0cf3b-115">Supported versions and installation</span></span>
<span data-ttu-id="0cf3b-116">이 Oracle 커넥터는 다음 두 가지 버전의 드라이버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="0cf3b-117">**Oracle (권장)에 대 한 Microsoft 드라이버**: 부터는 데이터 관리 게이트웨이 버전 2.7에서 Microsoft 드라이버 Oracle는 hello 게이트웨이 함께 자동으로 설치 됩니다. 따라서 필요 하지 않습니다 순서로 tooadditionally 핸들 hello 드라이버 tooestablish 연결 tooOracle 하 고이 드라이버를 사용 하 여 더 나은 복사 성능을 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="0cf3b-118">아래 Oracle 데이터베이스 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="0cf3b-119">Oracle 12c R1(12.1)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="0cf3b-120">Oracle 11g R1, R2(11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="0cf3b-121">Oracle 10g R1, R2(10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="0cf3b-122">Oracle 9i R1, R2(9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="0cf3b-123">Oracle 8i R3(8.1.7)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cf3b-124">현재 Microsoft driver for Oracle tooOracle를 작성 하지 않고 Oracle에서 데이터를 복사만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="0cf3b-125">및 데이터 관리 게이트웨이 진단 탭에서 hello 테스트 연결 기능에서는이 드라이버를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="0cf3b-126">또는 hello 복사 마법사 toovalidate hello 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="0cf3b-127">**Oracle Data Provider for.NET:** toouse Oracle 데이터 공급자 toocopy 데이터를 선택할 수도 있습니다 / tooOracle 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="0cf3b-128">이 구성 요소는 [Windows용 Oracle Data Access Components](http://www.oracle.com/technetwork/topics/dotnet/downloads/)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="0cf3b-129">Hello 게이트웨이가 설치 된 hello 컴퓨터에 hello 적절 한 버전 (32/64 비트)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="0cf3b-130">[Oracle 데이터 공급자.NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) tooOracle 데이터베이스 10g 릴리스 2 이상에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="0cf3b-131">"XCopy 설치"를 선택한 경우 hello readme.htm의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="0cf3b-132">UI (비-XCopy 하나)가 포함 된 hello 설치 관리자를 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="0cf3b-133">Hello 공급자를 설치한 후 **다시 시작** hello 서비스 애플릿을 (또는) 데이터 관리 게이트웨이 구성 관리자를 사용 하 여 컴퓨터에서 데이터 관리 게이트웨이 호스트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="0cf3b-134">복사 마법사 tooauthor hello 복사본 파이프라인을 사용 하는 경우 hello 드라이버 종류 자동 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="0cf3b-135">게이트웨이 버전이 2.7보다 낮거나 싱크로 Oracle을 선택한 경우가 아니면 기본적으로 Microsoft 드라이버가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0cf3b-136">시작</span><span class="sxs-lookup"><span data-stu-id="0cf3b-136">Getting started</span></span>
<span data-ttu-id="0cf3b-137">다른 도구/API를 사용하여 온-프레미스 Oracle 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="0cf3b-138">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0cf3b-139">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="0cf3b-140">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0cf3b-141">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="0cf3b-142">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="0cf3b-143">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-143">Create a **data factory**.</span></span> <span data-ttu-id="0cf3b-144">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="0cf3b-145">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="0cf3b-146">예를 들어 Oralce 데이터베이스 tooan Azure blob 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Oracle 데이터베이스와 Azure 저장소 계정 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="0cf3b-147">특정 tooOracle 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="0cf3b-148">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="0cf3b-149">예에서 hello hello 마지막 단계에서 언급 한 hello 입력된 데이터를 포함 하 여 Oracle 데이터베이스에서 데이터 집합 toospecify hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="0cf3b-150">And, 다른 데이터 집합 toospecify hello blob 컨테이너 만들기 및 Oracle 데이터베이스 hello에서 복사 된 hello 데이터를 보유 하는 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="0cf3b-151">참조 데이터 집합 속성을 특정 tooOracle [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="0cf3b-152">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="0cf3b-153">앞에서 언급 한 hello 예제를 사용 하 여 OracleSource 소스 및 BlobSink로는 싱크도 hello 복사 작업에 대 한.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="0cf3b-154">마찬가지로, Azure Blob 저장소 tooOracle 데이터베이스에서에서 복사 하는 경우 BlobSource 및 사용 OracleSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="0cf3b-155">복사 활동 속성을 특정 tooOracle 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="0cf3b-156">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="0cf3b-157">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0cf3b-158">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0cf3b-159">샘플 은/온-프레미스 Oracle 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-oracle-database) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="0cf3b-160">사용 되는 toodefine Data Factory 엔터티에 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0cf3b-161">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-161">Linked service properties</span></span>
<span data-ttu-id="0cf3b-162">다음 표에서 hello JSON 요소 특정 tooOracle 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="0cf3b-163">속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-163">Property</span></span> | <span data-ttu-id="0cf3b-164">설명</span><span class="sxs-lookup"><span data-stu-id="0cf3b-164">Description</span></span> | <span data-ttu-id="0cf3b-165">필수</span><span class="sxs-lookup"><span data-stu-id="0cf3b-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cf3b-166">type</span><span class="sxs-lookup"><span data-stu-id="0cf3b-166">type</span></span> |<span data-ttu-id="0cf3b-167">hello type 속성 설정 해야 합니다: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="0cf3b-168">예</span><span class="sxs-lookup"><span data-stu-id="0cf3b-168">Yes</span></span> |
| <span data-ttu-id="0cf3b-169">driverType</span><span class="sxs-lookup"><span data-stu-id="0cf3b-169">driverType</span></span> | <span data-ttu-id="0cf3b-170">드라이버 toouse toocopy 데이터 지정 / tooOracle 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="0cf3b-171">허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="0cf3b-172">드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="0cf3b-173">아니요</span><span class="sxs-lookup"><span data-stu-id="0cf3b-173">No</span></span> |
| <span data-ttu-id="0cf3b-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="0cf3b-174">connectionString</span></span> | <span data-ttu-id="0cf3b-175">Hello connectionString 속성에 대 한 tooconnect toohello Oracle 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="0cf3b-176">예</span><span class="sxs-lookup"><span data-stu-id="0cf3b-176">Yes</span></span> |
| <span data-ttu-id="0cf3b-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0cf3b-177">gatewayName</span></span> | <span data-ttu-id="0cf3b-178">사용 하는 tooconnect toohello 온-프레미스 Oracle 서버 hello 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="0cf3b-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="0cf3b-179">예</span><span class="sxs-lookup"><span data-stu-id="0cf3b-179">Yes</span></span> |

<span data-ttu-id="0cf3b-180">**예제: Microsoft 드라이버 사용:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="0cf3b-181">**예제: ODP 드라이버 사용**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="0cf3b-182">너무 참조[이 사이트](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) hello 허용 된 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="0cf3b-183">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-183">Dataset properties</span></span>
<span data-ttu-id="0cf3b-184">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0cf3b-185">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Oracle, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0cf3b-186">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0cf3b-187">OracleTable 형식의 hello 데이터 집합에 대 한 hello typeProperties 섹션에는 다음과 같은 속성 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="0cf3b-188">속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-188">Property</span></span> | <span data-ttu-id="0cf3b-189">설명</span><span class="sxs-lookup"><span data-stu-id="0cf3b-189">Description</span></span> | <span data-ttu-id="0cf3b-190">필수</span><span class="sxs-lookup"><span data-stu-id="0cf3b-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cf3b-191">tableName</span><span class="sxs-lookup"><span data-stu-id="0cf3b-191">tableName</span></span> |<span data-ttu-id="0cf3b-192">Oracle 데이터베이스를 연결 된 서비스 hello hello에 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="0cf3b-193">아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="0cf3b-194">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-194">Copy activity properties</span></span>
<span data-ttu-id="0cf3b-195">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0cf3b-196">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="0cf3b-197">복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="0cf3b-198">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0cf3b-199">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="0cf3b-200">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0cf3b-200">OracleSource</span></span>
<span data-ttu-id="0cf3b-201">Hello 원본 유형인 경우 복사 활동에서 **OracleSource** hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="0cf3b-202">속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-202">Property</span></span> | <span data-ttu-id="0cf3b-203">설명</span><span class="sxs-lookup"><span data-stu-id="0cf3b-203">Description</span></span> | <span data-ttu-id="0cf3b-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="0cf3b-204">Allowed values</span></span> | <span data-ttu-id="0cf3b-205">필수</span><span class="sxs-lookup"><span data-stu-id="0cf3b-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cf3b-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="0cf3b-206">oracleReaderQuery</span></span> |<span data-ttu-id="0cf3b-207">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0cf3b-208">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-208">SQL query string.</span></span> <span data-ttu-id="0cf3b-209">예: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="0cf3b-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="0cf3b-210">지정 하지 않으면 실행 되는 SQL 문을 hello: 선택 * from MyTable</span><span class="sxs-lookup"><span data-stu-id="0cf3b-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="0cf3b-211">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="0cf3b-212">파이프라인</span><span class="sxs-lookup"><span data-stu-id="0cf3b-212">OracleSink</span></span>
<span data-ttu-id="0cf3b-213">**OracleSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="0cf3b-214">속성</span><span class="sxs-lookup"><span data-stu-id="0cf3b-214">Property</span></span> | <span data-ttu-id="0cf3b-215">설명</span><span class="sxs-lookup"><span data-stu-id="0cf3b-215">Description</span></span> | <span data-ttu-id="0cf3b-216">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="0cf3b-216">Allowed values</span></span> | <span data-ttu-id="0cf3b-217">필수</span><span class="sxs-lookup"><span data-stu-id="0cf3b-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cf3b-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0cf3b-218">writeBatchTimeout</span></span> |<span data-ttu-id="0cf3b-219">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="0cf3b-220">timespan</span><span class="sxs-lookup"><span data-stu-id="0cf3b-220">timespan</span></span><br/><br/> <span data-ttu-id="0cf3b-221">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="0cf3b-222">아니요</span><span class="sxs-lookup"><span data-stu-id="0cf3b-222">No</span></span> |
| <span data-ttu-id="0cf3b-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0cf3b-223">writeBatchSize</span></span> |<span data-ttu-id="0cf3b-224">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="0cf3b-225">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-225">Integer (number of rows)</span></span> |<span data-ttu-id="0cf3b-226">아니요(기본값: 100)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-226">No (default: 100)</span></span> |
| <span data-ttu-id="0cf3b-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="0cf3b-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="0cf3b-228">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="0cf3b-229">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-229">A query statement.</span></span> |<span data-ttu-id="0cf3b-230">아니요</span><span class="sxs-lookup"><span data-stu-id="0cf3b-230">No</span></span> |
| <span data-ttu-id="0cf3b-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="0cf3b-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="0cf3b-232">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="0cf3b-233">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="0cf3b-234">아니요</span><span class="sxs-lookup"><span data-stu-id="0cf3b-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="0cf3b-235">Oracle 데이터베이스에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="0cf3b-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="0cf3b-236">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0cf3b-237">보여 줍니다 어떻게 toocopy 데이터로 / 하/Azure Blob 저장소에서 tooan Oracle 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="0cf3b-238">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="0cf3b-239">예: Oracle tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="0cf3b-240">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="0cf3b-241">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="0cf3b-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="0cf3b-242">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="0cf3b-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0cf3b-243">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="0cf3b-244">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0cf3b-245">[OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 소스로, [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="0cf3b-246">hello 샘플에 1 시간 마다는 온-프레미스 Oracle 데이터베이스 tooa blob의 테이블에서 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="0cf3b-247">Hello 샘플에 사용 되는 다양 한 속성에 대 한 자세한 내용은 hello 샘플 다음 섹션의 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="0cf3b-248">**Oracle 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="0cf3b-249">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="0cf3b-250">**Oracle 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="0cf3b-251">hello 샘플 테이블 "MyTable"에서 만든 Oracle 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="0cf3b-252">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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

<span data-ttu-id="0cf3b-253">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0cf3b-254">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0cf3b-255">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0cf3b-256">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="0cf3b-257">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="0cf3b-258">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="0cf3b-259">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**OracleSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="0cf3b-260">지정 된 hello SQL 쿼리 **oracleReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="0cf3b-261">예: Azure Blob tooOracle에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="0cf3b-262">이 샘플에서는 어떻게 toocopy 데이터를 Azure Blob 저장소 tooan 온-프레미스 Oracle 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="0cf3b-263">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 소스 중 하나에서 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="0cf3b-264">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="0cf3b-265">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="0cf3b-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="0cf3b-266">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="0cf3b-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0cf3b-267">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="0cf3b-268">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0cf3b-269">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)를 소스로, [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="0cf3b-270">hello 샘플 데이터 복사 온-프레미스 Oracle 데이터베이스에 있는 blob tooa 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="0cf3b-271">Hello 샘플에 사용 되는 다양 한 속성에 대 한 자세한 내용은 hello 샘플 다음 섹션의 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="0cf3b-272">**Oracle 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="0cf3b-273">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="0cf3b-274">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="0cf3b-275">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0cf3b-276">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0cf3b-277">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="0cf3b-278">"external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

<span data-ttu-id="0cf3b-279">**Oracle 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="0cf3b-280">hello 샘플 Oracle에 "MyTable" 테이블을 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="0cf3b-281">사용 하 여 Oracle에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="0cf3b-282">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-282">New rows are added toohello table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="0cf3b-283">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="0cf3b-284">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0cf3b-285">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 hello **싱크** 형식이 너무 설정**OracleSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="0cf3b-286">문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="0cf3b-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="0cf3b-287">문제 1: .NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="0cf3b-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="0cf3b-288">Hello 다음을 참조 **오류 메시지가**:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="0cf3b-289">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-289">**Possible causes:**</span></span>

1. <span data-ttu-id="0cf3b-290">.NET Framework Data Provider for Oracle hello 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="0cf3b-291">.NET Framework Data Provider for Oracle hello 설치 too.NET Framework 2.0 였으며 hello.NET Framework 4.0 폴더에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="0cf3b-292">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="0cf3b-293">Hello.NET Provider for Oracle 설치 하지 않은 경우 [설치](http://www.oracle.com/technetwork/topics/dotnet/downloads/) hello 시나리오를 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="0cf3b-294">Hello 공급자를 설치한 후에 hello 오류 메시지를 가져오는 경우 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="0cf3b-295">Hello 폴더에서 컴퓨터 구성의.NET 2.0을 열어: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="0cf3b-296">검색할 **Oracle Data Provider for.NET**, 샘플의 다음 hello에 표시 된 대로 수 toofind 항목 수 있어야 **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for.NET</span><span class="sxs-lookup"><span data-stu-id="0cf3b-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="0cf3b-297">”이라는 제목의 방법 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-297">”</span></span>
3. <span data-ttu-id="0cf3b-298">Hello v4.0 폴더를 다음에이 항목 toohello machine.config 파일을 복사: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, 및 hello 버전 too4.xxx.x.x 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="0cf3b-299">"< ODP.NET 설치 경로 > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll"를 실행 하 여 hello 전역 어셈블리 캐시 (GAC)에 설치 `gacutil /i [provider path]`. # # 문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="0cf3b-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="0cf3b-300">문제 2: 날짜/시간 서식</span><span class="sxs-lookup"><span data-stu-id="0cf3b-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="0cf3b-301">Hello 다음을 참조 **오류 메시지가**:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="0cf3b-302">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="0cf3b-303">Hello 다음과 같이 날짜는 Oracle 데이터베이스에서 구성 하는 방법에 따라 복사 작업에서 tooadjust hello 쿼리 문자열을 할 수 있습니다 (사용 하 여 hello to_date 함수가) 샘플:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="0cf3b-304">Oracle에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="0cf3b-304">Type mapping for Oracle</span></span>
<span data-ttu-id="0cf3b-305">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="0cf3b-306">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="0cf3b-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="0cf3b-307">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="0cf3b-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="0cf3b-308">Oracle에서 데이터를 이동할 때는 hello 매핑은 다음 Oracle 데이터 형식 too.NET 형식에서 그 반대의 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="0cf3b-309">Oracle 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="0cf3b-309">Oracle data type</span></span> | <span data-ttu-id="0cf3b-310">.NET Framework 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="0cf3b-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="0cf3b-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="0cf3b-311">BFILE</span></span> |<span data-ttu-id="0cf3b-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0cf3b-312">Byte[]</span></span> |
| <span data-ttu-id="0cf3b-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-313">BLOB</span></span> |<span data-ttu-id="0cf3b-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0cf3b-314">Byte[]</span></span> |
| <span data-ttu-id="0cf3b-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="0cf3b-315">CHAR</span></span> |<span data-ttu-id="0cf3b-316">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-316">String</span></span> |
| <span data-ttu-id="0cf3b-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-317">CLOB</span></span> |<span data-ttu-id="0cf3b-318">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-318">String</span></span> |
| <span data-ttu-id="0cf3b-319">DATE</span><span class="sxs-lookup"><span data-stu-id="0cf3b-319">DATE</span></span> |<span data-ttu-id="0cf3b-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cf3b-320">DateTime</span></span> |
| <span data-ttu-id="0cf3b-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="0cf3b-321">FLOAT</span></span> |<span data-ttu-id="0cf3b-322">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="0cf3b-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="0cf3b-323">INTEGER</span></span> |<span data-ttu-id="0cf3b-324">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="0cf3b-325">간격 연도 tooMONTH</span><span class="sxs-lookup"><span data-stu-id="0cf3b-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="0cf3b-326">Int32</span><span class="sxs-lookup"><span data-stu-id="0cf3b-326">Int32</span></span> |
| <span data-ttu-id="0cf3b-327">간격 날짜 tooSECOND</span><span class="sxs-lookup"><span data-stu-id="0cf3b-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="0cf3b-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0cf3b-328">TimeSpan</span></span> |
| <span data-ttu-id="0cf3b-329">LONG</span><span class="sxs-lookup"><span data-stu-id="0cf3b-329">LONG</span></span> |<span data-ttu-id="0cf3b-330">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-330">String</span></span> |
| <span data-ttu-id="0cf3b-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="0cf3b-331">LONG RAW</span></span> |<span data-ttu-id="0cf3b-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0cf3b-332">Byte[]</span></span> |
| <span data-ttu-id="0cf3b-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="0cf3b-333">NCHAR</span></span> |<span data-ttu-id="0cf3b-334">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-334">String</span></span> |
| <span data-ttu-id="0cf3b-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-335">NCLOB</span></span> |<span data-ttu-id="0cf3b-336">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-336">String</span></span> |
| <span data-ttu-id="0cf3b-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="0cf3b-337">NUMBER</span></span> |<span data-ttu-id="0cf3b-338">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="0cf3b-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="0cf3b-339">NVARCHAR2</span></span> |<span data-ttu-id="0cf3b-340">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-340">String</span></span> |
| <span data-ttu-id="0cf3b-341">RAW</span><span class="sxs-lookup"><span data-stu-id="0cf3b-341">RAW</span></span> |<span data-ttu-id="0cf3b-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0cf3b-342">Byte[]</span></span> |
| <span data-ttu-id="0cf3b-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="0cf3b-343">ROWID</span></span> |<span data-ttu-id="0cf3b-344">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-344">String</span></span> |
| <span data-ttu-id="0cf3b-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="0cf3b-345">TIMESTAMP</span></span> |<span data-ttu-id="0cf3b-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cf3b-346">DateTime</span></span> |
| <span data-ttu-id="0cf3b-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="0cf3b-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="0cf3b-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cf3b-348">DateTime</span></span> |
| <span data-ttu-id="0cf3b-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="0cf3b-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="0cf3b-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="0cf3b-350">DateTime</span></span> |
| <span data-ttu-id="0cf3b-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="0cf3b-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="0cf3b-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="0cf3b-352">Number</span></span> |
| <span data-ttu-id="0cf3b-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="0cf3b-353">VARCHAR2</span></span> |<span data-ttu-id="0cf3b-354">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-354">String</span></span> |
| <span data-ttu-id="0cf3b-355">XML</span><span class="sxs-lookup"><span data-stu-id="0cf3b-355">XML</span></span> |<span data-ttu-id="0cf3b-356">문자열</span><span class="sxs-lookup"><span data-stu-id="0cf3b-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="0cf3b-357">데이터 형식 **간격 연도 tooMONTH** 및 **간격 일 tooSECOND** Microsoft 드라이버를 사용 하는 경우 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="0cf3b-358">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="0cf3b-358">Map source toosink columns</span></span>
<span data-ttu-id="0cf3b-359">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0cf3b-360">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="0cf3b-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="0cf3b-361">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="0cf3b-362">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0cf3b-363">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0cf3b-364">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0cf3b-365">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0cf3b-366">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="0cf3b-366">Performance and Tuning</span></span>
<span data-ttu-id="0cf3b-367">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
