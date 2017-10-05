---
title: "데이터 팩터리를 사용하여 Oracle 간 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 온-프레미스 Oracle 데이터베이스 간 데이터를 복사하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="6a25b-103">Azure Data Factory를 사용하여 온-프레미스 Oracle 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6a25b-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="6a25b-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 Oracle 데이터베이스의 데이터를 다른 곳으로 이동하는 방법 또는 그 반대로 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="6a25b-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="6a25b-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="6a25b-106">Supported scenarios</span></span>
<span data-ttu-id="6a25b-107">**Oracle 데이터베이스에서** 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6a25b-108">다음 데이터 저장소에서 **Oracle 데이터베이스로** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="6a25b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6a25b-109">Prerequisites</span></span>
<span data-ttu-id="6a25b-110">Data Factory는 데이터 관리 게이트웨이를 사용하여 온-프레미스 Oracle 원본에 연결하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="6a25b-111">[데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하여 데이터 관리 게이트웨이에 대해 알아보고 [온-프레미스에서 클라우드로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하여 데이터를 이동하는 데이터 파이프라인의 게이트웨이 설정에 대 한 단계별 지침에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="6a25b-112">게이트웨이는 Oracle이 Azure IaaS VM에 호스트되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="6a25b-113">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 IaaS VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="6a25b-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6a25b-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="6a25b-115">Supported versions and installation</span></span>
<span data-ttu-id="6a25b-116">이 Oracle 커넥터는 다음 두 가지 버전의 드라이버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="6a25b-117">**Microsoft Driver for Oracle(권장)**: 데이터 관리 게이트웨이 버전 2.7부터 Microsoft Driver for Oracle은 게이트웨이와 함께 자동으로 설치되므로 Oracle에 대한 연결을 설정하기 위해 해당 드라이버를 추가로 처리할 필요가 없으며 이 드라이버를 사용하여 더 나은 복사 성능을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="6a25b-118">아래 Oracle 데이터베이스 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="6a25b-119">Oracle 12c R1(12.1)</span><span class="sxs-lookup"><span data-stu-id="6a25b-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="6a25b-120">Oracle 11g R1, R2(11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="6a25b-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="6a25b-121">Oracle 10g R1, R2(10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="6a25b-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="6a25b-122">Oracle 9i R1, R2(9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="6a25b-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="6a25b-123">Oracle 8i R3(8.1.7)</span><span class="sxs-lookup"><span data-stu-id="6a25b-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a25b-124">현재 Oracle용 Microsoft 드라이버는 Oracle에서 데이터를 복사하는 것만 지원하고 Oracle로 쓰는 것은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="6a25b-125">데이터 관리 게이트웨이 진단 탭의 연결 테스트 기능은 이 드라이버를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="6a25b-126">또는 복사 마법사를 사용하여 연결의 유효성을 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="6a25b-127">**.NET용 Oracle Data Provider:**  Oracle Data Provider를 사용하여 Oracle로 데이터를 복사하거나 Oracle에서 데이터를 복사하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="6a25b-128">이 구성 요소는 [Windows용 Oracle Data Access Components](http://www.oracle.com/technetwork/topics/dotnet/downloads/)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="6a25b-129">게이트웨이가 설치되어 있는 컴퓨터에 해당 버전(32/64비트)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="6a25b-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) 은 Oracle Database 10g 릴리스 2 이상에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="6a25b-131">"XCopy 설치"를 선택하는 경우 readme.htm의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="6a25b-132">UI(XCopy UI가 아닌 UI)가 포함된 설치 관리자를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="6a25b-133">공급자를 설치한 후 서비스 애플릿 또는 데이터 관리 게이트웨이 구성 관리자를 사용하여 컴퓨터에서 데이터 관리 게이트웨이 호스트 서비스를 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="6a25b-134">복사 마법사를 사용하여 복사 파이프라인을 작성하는 경우 드라이버 형식은 자동으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="6a25b-135">게이트웨이 버전이 2.7보다 낮거나 싱크로 Oracle을 선택한 경우가 아니면 기본적으로 Microsoft 드라이버가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6a25b-136">시작</span><span class="sxs-lookup"><span data-stu-id="6a25b-136">Getting started</span></span>
<span data-ttu-id="6a25b-137">다른 도구/API를 사용하여 온-프레미스 Oracle 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="6a25b-138">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6a25b-139">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="6a25b-140">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6a25b-141">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="6a25b-142">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6a25b-143">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-143">Create a **data factory**.</span></span> <span data-ttu-id="6a25b-144">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6a25b-145">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="6a25b-146">예를 들어 Oracle 데이터베이스에서 Azure Blob Storage로 복사하는 경우 Oracle 데이터베이스 및 Azure 저장소 계정을 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="6a25b-147">Oracle과 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="6a25b-148">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="6a25b-149">마지막 단계에서 설명한 예에서는 입력 데이터가 포함된 Oracle 데이터베이스의 테이블을 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="6a25b-150">그리고 Blob 컨테이너와 Oracle 데이터베이스에서 복사된 데이터가 저장되는 폴더를 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="6a25b-151">Oracle과 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6a25b-152">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6a25b-153">앞에서 언급한 예에서는 OracleSource를 원본으로, BlobSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="6a25b-154">마찬가지로, Azure Blob Storage에서 Oracle 데이터베이스로 복사하는 경우 복사 작업에 BlobSource 및 OracleSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="6a25b-155">Oracle 데이터베이스와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6a25b-156">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대 한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="6a25b-157">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6a25b-158">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6a25b-159">다른 곳에서 온-프레미스 Oracle 데이터베이스로 또는 그 반대로 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-oracle-database) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="6a25b-160">다음 섹션에서는 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6a25b-161">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-161">Linked service properties</span></span>
<span data-ttu-id="6a25b-162">다음 표에서는 Oracle 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="6a25b-163">속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-163">Property</span></span> | <span data-ttu-id="6a25b-164">설명</span><span class="sxs-lookup"><span data-stu-id="6a25b-164">Description</span></span> | <span data-ttu-id="6a25b-165">필수</span><span class="sxs-lookup"><span data-stu-id="6a25b-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a25b-166">type</span><span class="sxs-lookup"><span data-stu-id="6a25b-166">type</span></span> |<span data-ttu-id="6a25b-167">type 속성은 **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="6a25b-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="6a25b-168">예</span><span class="sxs-lookup"><span data-stu-id="6a25b-168">Yes</span></span> |
| <span data-ttu-id="6a25b-169">driverType</span><span class="sxs-lookup"><span data-stu-id="6a25b-169">driverType</span></span> | <span data-ttu-id="6a25b-170">Oracle Database로 데이터를 복사하거나 Oracle Database에서 데이터를 복사하는 데 사용할 드라이버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="6a25b-171">허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="6a25b-172">드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="6a25b-173">아니요</span><span class="sxs-lookup"><span data-stu-id="6a25b-173">No</span></span> |
| <span data-ttu-id="6a25b-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="6a25b-174">connectionString</span></span> | <span data-ttu-id="6a25b-175">connectionString 속성에 대한 Oracle 데이터베이스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="6a25b-176">예</span><span class="sxs-lookup"><span data-stu-id="6a25b-176">Yes</span></span> |
| <span data-ttu-id="6a25b-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6a25b-177">gatewayName</span></span> | <span data-ttu-id="6a25b-178">온-프레미스 Oracle 서버에 연결하는 데 사용할 게이트웨이 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="6a25b-179">예</span><span class="sxs-lookup"><span data-stu-id="6a25b-179">Yes</span></span> |

<span data-ttu-id="6a25b-180">**예제: Microsoft 드라이버 사용:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="6a25b-181">**예제: ODP 드라이버 사용**</span><span class="sxs-lookup"><span data-stu-id="6a25b-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="6a25b-182">허용되는 형식에 대한 내용은 [이 사이트](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="6a25b-183">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-183">Dataset properties</span></span>
<span data-ttu-id="6a25b-184">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6a25b-185">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Oracle, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="6a25b-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6a25b-186">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6a25b-187">OracleTable 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="6a25b-188">속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-188">Property</span></span> | <span data-ttu-id="6a25b-189">설명</span><span class="sxs-lookup"><span data-stu-id="6a25b-189">Description</span></span> | <span data-ttu-id="6a25b-190">필수</span><span class="sxs-lookup"><span data-stu-id="6a25b-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a25b-191">tableName</span><span class="sxs-lookup"><span data-stu-id="6a25b-191">tableName</span></span> |<span data-ttu-id="6a25b-192">연결된 서비스가 참조하는 Oracle 데이터베이스에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="6a25b-193">아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="6a25b-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6a25b-194">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-194">Copy activity properties</span></span>
<span data-ttu-id="6a25b-195">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6a25b-196">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6a25b-197">복사 작업은 하나의 입력을 가지고 하나의 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="6a25b-198">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="6a25b-199">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="6a25b-200">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6a25b-200">OracleSource</span></span>
<span data-ttu-id="6a25b-201">원본이 **OracleSource** 형식인 복사 작업의 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6a25b-202">속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-202">Property</span></span> | <span data-ttu-id="6a25b-203">설명</span><span class="sxs-lookup"><span data-stu-id="6a25b-203">Description</span></span> | <span data-ttu-id="6a25b-204">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="6a25b-204">Allowed values</span></span> | <span data-ttu-id="6a25b-205">필수</span><span class="sxs-lookup"><span data-stu-id="6a25b-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6a25b-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6a25b-206">oracleReaderQuery</span></span> |<span data-ttu-id="6a25b-207">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-207">Use the custom query to read data.</span></span> |<span data-ttu-id="6a25b-208">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="6a25b-208">SQL query string.</span></span> <span data-ttu-id="6a25b-209">예: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="6a25b-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="6a25b-210">지정하지 않는 경우 실행되는 SQL 문: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="6a25b-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="6a25b-211">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="6a25b-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="6a25b-212">파이프라인</span><span class="sxs-lookup"><span data-stu-id="6a25b-212">OracleSink</span></span>
<span data-ttu-id="6a25b-213">**OracleSink** 는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="6a25b-214">속성</span><span class="sxs-lookup"><span data-stu-id="6a25b-214">Property</span></span> | <span data-ttu-id="6a25b-215">설명</span><span class="sxs-lookup"><span data-stu-id="6a25b-215">Description</span></span> | <span data-ttu-id="6a25b-216">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="6a25b-216">Allowed values</span></span> | <span data-ttu-id="6a25b-217">필수</span><span class="sxs-lookup"><span data-stu-id="6a25b-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6a25b-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6a25b-218">writeBatchTimeout</span></span> |<span data-ttu-id="6a25b-219">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="6a25b-220">timespan</span><span class="sxs-lookup"><span data-stu-id="6a25b-220">timespan</span></span><br/><br/> <span data-ttu-id="6a25b-221">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="6a25b-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="6a25b-222">아니요</span><span class="sxs-lookup"><span data-stu-id="6a25b-222">No</span></span> |
| <span data-ttu-id="6a25b-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6a25b-223">writeBatchSize</span></span> |<span data-ttu-id="6a25b-224">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="6a25b-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6a25b-225">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="6a25b-225">Integer (number of rows)</span></span> |<span data-ttu-id="6a25b-226">아니요(기본값: 100)</span><span class="sxs-lookup"><span data-stu-id="6a25b-226">No (default: 100)</span></span> |
| <span data-ttu-id="6a25b-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6a25b-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6a25b-228">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="6a25b-229">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-229">A query statement.</span></span> |<span data-ttu-id="6a25b-230">아니요</span><span class="sxs-lookup"><span data-stu-id="6a25b-230">No</span></span> |
| <span data-ttu-id="6a25b-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6a25b-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6a25b-232">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="6a25b-233">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6a25b-234">아니요</span><span class="sxs-lookup"><span data-stu-id="6a25b-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="6a25b-235">Oracle 데이터베이스로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="6a25b-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="6a25b-236">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6a25b-237">이 샘플은 Oracle 데이터베이스와 Azure Blob 저장소 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="6a25b-238">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="6a25b-239">예: Oracle에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6a25b-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="6a25b-240">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6a25b-241">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="6a25b-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6a25b-242">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="6a25b-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6a25b-243">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="6a25b-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6a25b-244">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="6a25b-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6a25b-245">[OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 소스로, [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="6a25b-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="6a25b-246">샘플은 온-프레미스 Oracle 데이터베이스의 테이블에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="6a25b-247">샘플에 사용되는 다양한 속성에 대한 자세한 내용은 샘플 다음에 나오는 섹션의 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="6a25b-248">**Oracle 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="6a25b-249">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="6a25b-250">**Oracle 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="6a25b-251">샘플은 Oracle에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn"이라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6a25b-252">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="6a25b-253">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6a25b-254">데이터는 매시간 새 blob에 기록됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6a25b-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6a25b-255">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6a25b-256">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="6a25b-257">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6a25b-258">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="6a25b-259">파이프라인 JSON 정의에서 **원본** 형식은 **OracleSource**로 설정되고 **싱크** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="6a25b-260">**oracleReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="6a25b-261">예: Azure Blob에서 Oracle로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6a25b-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="6a25b-262">이 샘플은 Azure Blob 저장소에서 온-프레미스 Oracle 데이터베이스로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="6a25b-263">그러나 Azure Data Factory의 복사 작업을 사용하여 **여기** 에 설명한 원본에서 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="6a25b-264">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6a25b-265">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="6a25b-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6a25b-266">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="6a25b-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6a25b-267">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6a25b-268">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6a25b-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6a25b-269">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)를 소스로, [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="6a25b-270">샘플은 Blob에서 온-프레미스 Oracle 데이터베이스의 테이블로 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="6a25b-271">샘플에 사용되는 다양한 속성에 대한 자세한 내용은 샘플 다음에 나오는 섹션의 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="6a25b-272">**Oracle 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="6a25b-273">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="6a25b-274">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="6a25b-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="6a25b-275">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6a25b-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6a25b-276">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6a25b-277">폴더 경로는 연도, 월 및 일 일부 시작 시간을 사용하고 파일 이름은 시작 시간의 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="6a25b-278">"external": "true" 설정은 데이터 팩터리 서비스에 이 테이블이 데이터 팩터리의 외부에 있으며 데이터 팩터리의 작업에 의해 생성되지 않는다는 점을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="6a25b-279">**Oracle 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="6a25b-280">샘플은 Oracle에 "MyTable" 테이블을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="6a25b-281">Blob CSV 파일을 포함하려 하면 같은 수의 열을 사용하여 Oracle에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="6a25b-282">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-282">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="6a25b-283">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6a25b-284">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6a25b-285">파이프라인 JSON 정의에서 **원본** 형식은 **BlobSource**로 설정되고 **싱크** 형식은 **OracleSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="6a25b-286">문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="6a25b-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="6a25b-287">문제 1: .NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="6a25b-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="6a25b-288">다음 **오류 메시지**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="6a25b-289">**가능한 원인:**</span><span class="sxs-lookup"><span data-stu-id="6a25b-289">**Possible causes:**</span></span>

1. <span data-ttu-id="6a25b-290">.NET Framework Data Provider for Oracle이 설치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="6a25b-291">.NET Framework Data Provider for Oracle이 .NET Framework 2.0에 설치되었고 .NET Framework 4.0 폴더에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="6a25b-292">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="6a25b-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="6a25b-293">.NET Provider for Oracle을 설치하지 않았으면 [해당 항목을 설치](http://www.oracle.com/technetwork/topics/dotnet/downloads/) 한 후 시나리오를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="6a25b-294">Provider를 설치한 후에도 오류 메시지가 표시되면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="6a25b-295"><system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config 폴더에서 .NET 2.0 machine config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="6a25b-296">**Oracle Data Provider for .NET**을 검색하면 **system.data** -> **DbProviderFactories**에서 “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET과 같은 항목을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="6a25b-297">”이라는 제목의 방법 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-297">”</span></span>
3. <span data-ttu-id="6a25b-298">이 항목을 v4.0 폴더 즉, <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config의 machine.config 파일에 복사하고 버전을 4.xxx.x.x으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="6a25b-299">`gacutil /i [provider path]`를 실행하여 전역 어셈블리 캐시(GAC)에 “<ODP.NET 설치된 경로>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll”을 설치합니다.## 문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="6a25b-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="6a25b-300">문제 2: 날짜/시간 서식</span><span class="sxs-lookup"><span data-stu-id="6a25b-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="6a25b-301">다음 **오류 메시지**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="6a25b-302">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="6a25b-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="6a25b-303">다음 샘플에서처럼 Oracle Database에 날짜가 구성되는 방법에 따라 복사 작업에서 쿼리 문자열을 조정해야 할 수 있습니다(To_date 함수 사용).</span><span class="sxs-lookup"><span data-stu-id="6a25b-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="6a25b-304">Oracle에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="6a25b-304">Type mapping for Oracle</span></span>
<span data-ttu-id="6a25b-305">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="6a25b-306">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="6a25b-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6a25b-307">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="6a25b-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6a25b-308">Oracle에서 데이터를 이동하는 경우 Oracle 데이터 형식에서 .NET 형식에 그리고 그 반대로 다음 매핑을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="6a25b-309">Oracle 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="6a25b-309">Oracle data type</span></span> | <span data-ttu-id="6a25b-310">.NET Framework 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="6a25b-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="6a25b-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="6a25b-311">BFILE</span></span> |<span data-ttu-id="6a25b-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a25b-312">Byte[]</span></span> |
| <span data-ttu-id="6a25b-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="6a25b-313">BLOB</span></span> |<span data-ttu-id="6a25b-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a25b-314">Byte[]</span></span> |
| <span data-ttu-id="6a25b-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="6a25b-315">CHAR</span></span> |<span data-ttu-id="6a25b-316">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-316">String</span></span> |
| <span data-ttu-id="6a25b-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="6a25b-317">CLOB</span></span> |<span data-ttu-id="6a25b-318">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-318">String</span></span> |
| <span data-ttu-id="6a25b-319">DATE</span><span class="sxs-lookup"><span data-stu-id="6a25b-319">DATE</span></span> |<span data-ttu-id="6a25b-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a25b-320">DateTime</span></span> |
| <span data-ttu-id="6a25b-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="6a25b-321">FLOAT</span></span> |<span data-ttu-id="6a25b-322">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="6a25b-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6a25b-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="6a25b-323">INTEGER</span></span> |<span data-ttu-id="6a25b-324">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="6a25b-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6a25b-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="6a25b-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="6a25b-326">Int32</span><span class="sxs-lookup"><span data-stu-id="6a25b-326">Int32</span></span> |
| <span data-ttu-id="6a25b-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="6a25b-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="6a25b-328">timespan</span><span class="sxs-lookup"><span data-stu-id="6a25b-328">TimeSpan</span></span> |
| <span data-ttu-id="6a25b-329">LONG</span><span class="sxs-lookup"><span data-stu-id="6a25b-329">LONG</span></span> |<span data-ttu-id="6a25b-330">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-330">String</span></span> |
| <span data-ttu-id="6a25b-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="6a25b-331">LONG RAW</span></span> |<span data-ttu-id="6a25b-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a25b-332">Byte[]</span></span> |
| <span data-ttu-id="6a25b-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="6a25b-333">NCHAR</span></span> |<span data-ttu-id="6a25b-334">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-334">String</span></span> |
| <span data-ttu-id="6a25b-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="6a25b-335">NCLOB</span></span> |<span data-ttu-id="6a25b-336">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-336">String</span></span> |
| <span data-ttu-id="6a25b-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="6a25b-337">NUMBER</span></span> |<span data-ttu-id="6a25b-338">Decimal, 문자열(전체 자릿수의 경우 > 28)</span><span class="sxs-lookup"><span data-stu-id="6a25b-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6a25b-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="6a25b-339">NVARCHAR2</span></span> |<span data-ttu-id="6a25b-340">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-340">String</span></span> |
| <span data-ttu-id="6a25b-341">RAW</span><span class="sxs-lookup"><span data-stu-id="6a25b-341">RAW</span></span> |<span data-ttu-id="6a25b-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6a25b-342">Byte[]</span></span> |
| <span data-ttu-id="6a25b-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="6a25b-343">ROWID</span></span> |<span data-ttu-id="6a25b-344">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-344">String</span></span> |
| <span data-ttu-id="6a25b-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="6a25b-345">TIMESTAMP</span></span> |<span data-ttu-id="6a25b-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a25b-346">DateTime</span></span> |
| <span data-ttu-id="6a25b-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="6a25b-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="6a25b-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a25b-348">DateTime</span></span> |
| <span data-ttu-id="6a25b-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="6a25b-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="6a25b-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="6a25b-350">DateTime</span></span> |
| <span data-ttu-id="6a25b-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="6a25b-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="6a25b-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="6a25b-352">Number</span></span> |
| <span data-ttu-id="6a25b-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="6a25b-353">VARCHAR2</span></span> |<span data-ttu-id="6a25b-354">문자열</span><span class="sxs-lookup"><span data-stu-id="6a25b-354">String</span></span> |
| <span data-ttu-id="6a25b-355">XML</span><span class="sxs-lookup"><span data-stu-id="6a25b-355">XML</span></span> |<span data-ttu-id="6a25b-356">String</span><span class="sxs-lookup"><span data-stu-id="6a25b-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="6a25b-357">데이터 형식 **INTERVAL YEAR TO MONTH** 및 **INTERVAL DAY TO SECOND**는 Microsoft 드라이버를 사용할 때 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6a25b-358">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="6a25b-358">Map source to sink columns</span></span>
<span data-ttu-id="6a25b-359">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6a25b-360">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="6a25b-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="6a25b-361">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6a25b-362">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6a25b-363">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6a25b-364">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a25b-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6a25b-365">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6a25b-366">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="6a25b-366">Performance and Tuning</span></span>
<span data-ttu-id="6a25b-367">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a25b-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
