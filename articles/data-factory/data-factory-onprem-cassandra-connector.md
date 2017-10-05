---
title: "Data Factory를 사용하여 Cassandra에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 온-프레미스 Cassandra 데이터베이스에서 데이터를 이동하는 방법을 알아봅니다."
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
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="95c71-103">Azure Data Factory를 사용하여 온-프레미스 Cassandra 데이터베이스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="95c71-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="95c71-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 Cassandra 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="95c71-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="95c71-106">온-프레미스 Cassandra 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="95c71-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="95c71-108">현재 데이터 팩터리는 다른 데이터 저장소에서 Cassandra 데이터 저장소로 데이터 이동이 아닌 Cassandra 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="95c71-109">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="95c71-109">Supported versions</span></span>
<span data-ttu-id="95c71-110">Cassandra 커넥터는 Cassandra 2.X 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95c71-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95c71-111">Prerequisites</span></span>
<span data-ttu-id="95c71-112">Azure Data Factory 서비스가 온-프레미스 Cassandra 데이터베이스에 연결할 수 있도록 하려면 데이터베이스와 리소스 경쟁을 피하려면 데이터 관리 게이트웨이를 데이터베이스를 호스트하는 컴퓨터와 동일한 컴퓨터 또는 별도의 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="95c71-113">데이터 관리 게이트웨이는 온-프레미스 데이터 원본을 클라우드 서비스에 안전하게 관리되는 방식으로 연결하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="95c71-114">데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="95c71-115">데이터 이동을 위한 데이터 파이프라인 및 게이트웨이 설정에 대한 단계별 지침은 [온-프레미스에서 클라우드로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="95c71-116">데이터베이스가 클라우드(예: Azure IaaS VM)에서 호스팅되는 경우에도 게이트웨이를 사용하여 Cassandra 데이터베이스에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="95c71-117">게이트웨이를 데이터베이스에 연결할 수 있는 한, 데이터베이스를 호스팅하는 동일한 VM 또는 별도의 VM에 게이트웨이를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="95c71-118">게이트웨이를 설치하면 Cassandra 데이터베이스에 연결하는 데 사용되는 Microsoft Cassandra ODBC 드라이버가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="95c71-119">따라서 Cassandra 데이터베이스에서 데이터를 복사할 때 게이트웨이 컴퓨터에 드라이버를 수동으로 설치하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="95c71-120">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="95c71-121">시작</span><span class="sxs-lookup"><span data-stu-id="95c71-121">Getting started</span></span>
<span data-ttu-id="95c71-122">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="95c71-123">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="95c71-124">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="95c71-125">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="95c71-126">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="95c71-127">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="95c71-128">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="95c71-129">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="95c71-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="95c71-131">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="95c71-132">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="95c71-133">온-프레미스 Cassandra 데이터 저장소의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: Cassandra에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-cassandra-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="95c71-134">다음 섹션에서는 Cassandra 데이터 저장소에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="95c71-135">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="95c71-135">Linked service properties</span></span>
<span data-ttu-id="95c71-136">다음 표에서는 Cassandra 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="95c71-137">속성</span><span class="sxs-lookup"><span data-stu-id="95c71-137">Property</span></span> | <span data-ttu-id="95c71-138">설명</span><span class="sxs-lookup"><span data-stu-id="95c71-138">Description</span></span> | <span data-ttu-id="95c71-139">필수</span><span class="sxs-lookup"><span data-stu-id="95c71-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95c71-140">type</span><span class="sxs-lookup"><span data-stu-id="95c71-140">type</span></span> |<span data-ttu-id="95c71-141">type 속성은 다음으로 설정해야 함: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="95c71-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="95c71-142">예</span><span class="sxs-lookup"><span data-stu-id="95c71-142">Yes</span></span> |
| <span data-ttu-id="95c71-143">host</span><span class="sxs-lookup"><span data-stu-id="95c71-143">host</span></span> |<span data-ttu-id="95c71-144">Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.</span><span class="sxs-lookup"><span data-stu-id="95c71-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="95c71-145">모든 서버에 동시에 연결하려면 쉼표로 구분된 IP 주소 또는 호스트 이름 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="95c71-146">예</span><span class="sxs-lookup"><span data-stu-id="95c71-146">Yes</span></span> |
| <span data-ttu-id="95c71-147">포트</span><span class="sxs-lookup"><span data-stu-id="95c71-147">port</span></span> |<span data-ttu-id="95c71-148">Cassandra 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="95c71-149">아니요. 기본값: 9042</span><span class="sxs-lookup"><span data-stu-id="95c71-149">No, default value: 9042</span></span> |
| <span data-ttu-id="95c71-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="95c71-150">authenticationType</span></span> |<span data-ttu-id="95c71-151">Basic 또는 Anonymous</span><span class="sxs-lookup"><span data-stu-id="95c71-151">Basic, or Anonymous</span></span> |<span data-ttu-id="95c71-152">예</span><span class="sxs-lookup"><span data-stu-id="95c71-152">Yes</span></span> |
| <span data-ttu-id="95c71-153">username</span><span class="sxs-lookup"><span data-stu-id="95c71-153">username</span></span> |<span data-ttu-id="95c71-154">사용자 계정의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-154">Specify user name for the user account.</span></span> |<span data-ttu-id="95c71-155">예. authenticationType은 Basic으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="95c71-156">password</span><span class="sxs-lookup"><span data-stu-id="95c71-156">password</span></span> |<span data-ttu-id="95c71-157">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-157">Specify password for the user account.</span></span> |<span data-ttu-id="95c71-158">예. authenticationType은 Basic으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="95c71-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="95c71-159">gatewayName</span></span> |<span data-ttu-id="95c71-160">온-프레미스 Cassandra 데이터베이스에 연결하는 데 사용되는 게이트웨이 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="95c71-161">예</span><span class="sxs-lookup"><span data-stu-id="95c71-161">Yes</span></span> |
| <span data-ttu-id="95c71-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="95c71-162">encryptedCredential</span></span> |<span data-ttu-id="95c71-163">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="95c71-164">아니요</span><span class="sxs-lookup"><span data-stu-id="95c71-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="95c71-165">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="95c71-165">Dataset properties</span></span>
<span data-ttu-id="95c71-166">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="95c71-167">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="95c71-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="95c71-168">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="95c71-169">**CassandraTable** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="95c71-170">속성</span><span class="sxs-lookup"><span data-stu-id="95c71-170">Property</span></span> | <span data-ttu-id="95c71-171">설명</span><span class="sxs-lookup"><span data-stu-id="95c71-171">Description</span></span> | <span data-ttu-id="95c71-172">필수</span><span class="sxs-lookup"><span data-stu-id="95c71-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95c71-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="95c71-173">keyspace</span></span> |<span data-ttu-id="95c71-174">Cassandra 데이터베이스의 키스페이스 또는 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="95c71-175">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="95c71-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="95c71-176">tableName</span><span class="sxs-lookup"><span data-stu-id="95c71-176">tableName</span></span> |<span data-ttu-id="95c71-177">Cassandra 데이터베이스에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="95c71-178">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="95c71-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="95c71-179">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="95c71-179">Copy activity properties</span></span>
<span data-ttu-id="95c71-180">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="95c71-181">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="95c71-182">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="95c71-183">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="95c71-184">원본이 **CassandraSource**형식인 경우 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="95c71-185">속성</span><span class="sxs-lookup"><span data-stu-id="95c71-185">Property</span></span> | <span data-ttu-id="95c71-186">설명</span><span class="sxs-lookup"><span data-stu-id="95c71-186">Description</span></span> | <span data-ttu-id="95c71-187">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="95c71-187">Allowed values</span></span> | <span data-ttu-id="95c71-188">필수</span><span class="sxs-lookup"><span data-stu-id="95c71-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="95c71-189">쿼리</span><span class="sxs-lookup"><span data-stu-id="95c71-189">query</span></span> |<span data-ttu-id="95c71-190">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-190">Use the custom query to read data.</span></span> |<span data-ttu-id="95c71-191">SQL-92 쿼리 또는 CQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="95c71-192">[CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="95c71-193">SQL 쿼리를 사용할 경우 **keyspace name.table name** 을 지정하여 쿼리하려는 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="95c71-194">아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우)</span><span class="sxs-lookup"><span data-stu-id="95c71-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="95c71-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="95c71-195">consistencyLevel</span></span> |<span data-ttu-id="95c71-196">일관성 수준은 클라이언트 응용 프로그램에 데이터를 반환하기 전에 읽기 요청에 응답해야 하는 복제본 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="95c71-197">Cassandra는 데이터의 지정된 수의 복제본이 읽기 요청을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="95c71-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="95c71-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="95c71-199">자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="95c71-200">아니요.</span><span class="sxs-lookup"><span data-stu-id="95c71-200">No.</span></span> <span data-ttu-id="95c71-201">기본값은 ONE입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="95c71-202">JSON 예: Cassandra에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="95c71-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="95c71-203">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="95c71-204">온-프레미스 Cassandra 데이터베이스에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="95c71-205">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95c71-206">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="95c71-207">데이터 팩터리를 만들기 위한 단계별 지침은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="95c71-208">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="95c71-209">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="95c71-210">[OnPremisesCassandra](#linked-service-properties)형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="95c71-211">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="95c71-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="95c71-212">[CassandraTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="95c71-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="95c71-213">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="95c71-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="95c71-214">[CassandraSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="95c71-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="95c71-215">**Cassandra 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="95c71-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="95c71-216">이 예제에서는 **Cassandra** 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="95c71-217">이 연결된 서비스에서 지원하는 속성 목록은 [Cassandra 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

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

<span data-ttu-id="95c71-218">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="95c71-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="95c71-219">**Cassandra 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="95c71-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="95c71-220">**external**을 **true**로 설정하면 데이터 집합이 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="95c71-221">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="95c71-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="95c71-222">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="95c71-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="95c71-223">**Cassandra 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="95c71-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="95c71-224">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="95c71-225">파이프라인 JSON 정의에서 **source** 형식은 **CassandraSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="95c71-226">RelationalSource에서 지원하는 속성 목록은 [RelationalSource 형식 속성](#copy-activity-properties) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

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
            "description": "Copy from Cassandra to an Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="95c71-227">Cassandra에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="95c71-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="95c71-228">Cassandra 형식</span><span class="sxs-lookup"><span data-stu-id="95c71-228">Cassandra Type</span></span> | <span data-ttu-id="95c71-229">.NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="95c71-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="95c71-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="95c71-230">ASCII</span></span> |<span data-ttu-id="95c71-231">문자열</span><span class="sxs-lookup"><span data-stu-id="95c71-231">String</span></span> |
| <span data-ttu-id="95c71-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="95c71-232">BIGINT</span></span> |<span data-ttu-id="95c71-233">Int64</span><span class="sxs-lookup"><span data-stu-id="95c71-233">Int64</span></span> |
| <span data-ttu-id="95c71-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="95c71-234">BLOB</span></span> |<span data-ttu-id="95c71-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="95c71-235">Byte[]</span></span> |
| <span data-ttu-id="95c71-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="95c71-236">BOOLEAN</span></span> |<span data-ttu-id="95c71-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="95c71-237">Boolean</span></span> |
| <span data-ttu-id="95c71-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="95c71-238">DECIMAL</span></span> |<span data-ttu-id="95c71-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="95c71-239">Decimal</span></span> |
| <span data-ttu-id="95c71-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="95c71-240">DOUBLE</span></span> |<span data-ttu-id="95c71-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="95c71-241">Double</span></span> |
| <span data-ttu-id="95c71-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="95c71-242">FLOAT</span></span> |<span data-ttu-id="95c71-243">단일</span><span class="sxs-lookup"><span data-stu-id="95c71-243">Single</span></span> |
| <span data-ttu-id="95c71-244">INET</span><span class="sxs-lookup"><span data-stu-id="95c71-244">INET</span></span> |<span data-ttu-id="95c71-245">문자열</span><span class="sxs-lookup"><span data-stu-id="95c71-245">String</span></span> |
| <span data-ttu-id="95c71-246">INT</span><span class="sxs-lookup"><span data-stu-id="95c71-246">INT</span></span> |<span data-ttu-id="95c71-247">Int32</span><span class="sxs-lookup"><span data-stu-id="95c71-247">Int32</span></span> |
| <span data-ttu-id="95c71-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="95c71-248">TEXT</span></span> |<span data-ttu-id="95c71-249">문자열</span><span class="sxs-lookup"><span data-stu-id="95c71-249">String</span></span> |
| <span data-ttu-id="95c71-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="95c71-250">TIMESTAMP</span></span> |<span data-ttu-id="95c71-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="95c71-251">DateTime</span></span> |
| <span data-ttu-id="95c71-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="95c71-252">TIMEUUID</span></span> |<span data-ttu-id="95c71-253">Guid</span><span class="sxs-lookup"><span data-stu-id="95c71-253">Guid</span></span> |
| <span data-ttu-id="95c71-254">UUID</span><span class="sxs-lookup"><span data-stu-id="95c71-254">UUID</span></span> |<span data-ttu-id="95c71-255">Guid</span><span class="sxs-lookup"><span data-stu-id="95c71-255">Guid</span></span> |
| <span data-ttu-id="95c71-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="95c71-256">VARCHAR</span></span> |<span data-ttu-id="95c71-257">문자열</span><span class="sxs-lookup"><span data-stu-id="95c71-257">String</span></span> |
| <span data-ttu-id="95c71-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="95c71-258">VARINT</span></span> |<span data-ttu-id="95c71-259">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="95c71-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="95c71-260">컬렉션 형식(맵, 집합, 목록 등)에 대해서는 [가상 테이블을 사용하여 Cassandra 컬렉션 형식으로 작업](#work-with-collections-using-virtual-table) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="95c71-261">사용자 정의 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="95c71-262">이진 열의 길이와 문자열 열 길이는 4000보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="95c71-263">가상 테이블을 사용하여 컬렉션으로 작업</span><span class="sxs-lookup"><span data-stu-id="95c71-263">Work with collections using virtual table</span></span>
<span data-ttu-id="95c71-264">Azure Data Factory는 기본 제공 ODBC 드라이버를 사용하여 Cassandra 데이터베이스에 연결하고 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="95c71-265">맵, 집합 및 목록을 포함하는 컬렉션 형식의 경우 드라이버는 데이터를 해당 가상 테이블로 다시 정규화합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="95c71-266">특히, 테이블에 컬렉션 열이 포함되어 있으면 드라이버는 다음 가상 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="95c71-267">**기본 테이블**: 컬렉션 열을 제외하고 실제 테이블과 동일한 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="95c71-268">기본 테이블은 나타내는 실제 테이블과 동일한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="95c71-269">**가상 테이블** : 컬렉션 열에 대해 생성되며, 중첩된 데이터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="95c71-270">컬렉션을 나타내는 가상 테이블 이름은 실제 테이블의 이름, 구분 기호 "*vt*" 및 열 이름을 사용하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="95c71-271">가상 테이블은 실제 테이블의 데이터를 나타내며, 드라이버가 정규화되지 않은 데이터에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="95c71-272">자세한 내용은 예제 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-272">See Example section for details.</span></span> <span data-ttu-id="95c71-273">가상 테이블을 쿼리 및 조인하여 Cassandra 컬렉션의 콘텐츠에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="95c71-274">[복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity)를 사용하여 가상 테이블을 비롯한 Cassandra 데이터베이스의 테이블 목록을 표시하고 내부의 데이터를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="95c71-275">또한 복사 마법사에서 쿼리를 생성하고 결과가 유효한지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="95c71-276">예</span><span class="sxs-lookup"><span data-stu-id="95c71-276">Example</span></span>
<span data-ttu-id="95c71-277">예를 들어 다음 "ExampleTable"은 "pk_int"라는 정수 기본 키 열, value라는 텍스트 열, 목록 열, 맵 열, 집합 열("StringSet")을 포함하는 Cassandra 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="95c71-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="95c71-278">pk_int</span></span> | <span data-ttu-id="95c71-279">값</span><span class="sxs-lookup"><span data-stu-id="95c71-279">Value</span></span> | <span data-ttu-id="95c71-280">나열</span><span class="sxs-lookup"><span data-stu-id="95c71-280">List</span></span> | <span data-ttu-id="95c71-281">Map</span><span class="sxs-lookup"><span data-stu-id="95c71-281">Map</span></span> | <span data-ttu-id="95c71-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="95c71-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="95c71-283">1</span><span class="sxs-lookup"><span data-stu-id="95c71-283">1</span></span> |<span data-ttu-id="95c71-284">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="95c71-284">"sample value 1"</span></span> |<span data-ttu-id="95c71-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="95c71-285">["1", "2", "3"]</span></span> |<span data-ttu-id="95c71-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="95c71-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="95c71-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="95c71-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="95c71-288">3</span><span class="sxs-lookup"><span data-stu-id="95c71-288">3</span></span> |<span data-ttu-id="95c71-289">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="95c71-289">"sample value 3"</span></span> |<span data-ttu-id="95c71-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="95c71-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="95c71-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="95c71-291">{"S1": "t"}</span></span> |<span data-ttu-id="95c71-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="95c71-292">{"A", "E"}</span></span> |

<span data-ttu-id="95c71-293">드라이버는 이 단일 테이블을 나타내는 여러 개의 가상 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="95c71-294">가상 테이블의 외래 키 열은 실제 테이블의 기본 키 열을 참조하고, 가상 테이블 행에 해당하는 실제 테이블 행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="95c71-295">첫 번째 가상 테이블은 다음 테이블에 표시된 "ExampleTable"이라는 기본 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="95c71-296">기본 테이블에는 컬렉션을 제외하고 원래 데이터베이스 테이블과 동일한 데이터가 포함됩니다. 컬렉션은 테이블에서 생략된 후 다른 가상 테이블에서 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="95c71-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="95c71-297">pk_int</span></span> | <span data-ttu-id="95c71-298">값</span><span class="sxs-lookup"><span data-stu-id="95c71-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="95c71-299">1</span><span class="sxs-lookup"><span data-stu-id="95c71-299">1</span></span> |<span data-ttu-id="95c71-300">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="95c71-300">"sample value 1"</span></span> |
| <span data-ttu-id="95c71-301">3</span><span class="sxs-lookup"><span data-stu-id="95c71-301">3</span></span> |<span data-ttu-id="95c71-302">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="95c71-302">"sample value 3"</span></span> |

<span data-ttu-id="95c71-303">다음 표에서는 List, Map 및 StringSet 열의 데이터를 다시 정규화하는 가상 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="95c71-304">이름이 “_index” 또는 “_key”로 끝나는 열은 원본 목록이나 맵 내의 데이터 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="95c71-305">이름이 "_value"로 끝나는 열에는 컬렉션에서 확장된 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="95c71-306">테이블 "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="95c71-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="95c71-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="95c71-307">pk_int</span></span> | <span data-ttu-id="95c71-308">List_index</span><span class="sxs-lookup"><span data-stu-id="95c71-308">List_index</span></span> | <span data-ttu-id="95c71-309">List_value</span><span class="sxs-lookup"><span data-stu-id="95c71-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95c71-310">1</span><span class="sxs-lookup"><span data-stu-id="95c71-310">1</span></span> |<span data-ttu-id="95c71-311">0</span><span class="sxs-lookup"><span data-stu-id="95c71-311">0</span></span> |<span data-ttu-id="95c71-312">1</span><span class="sxs-lookup"><span data-stu-id="95c71-312">1</span></span> |
| <span data-ttu-id="95c71-313">1</span><span class="sxs-lookup"><span data-stu-id="95c71-313">1</span></span> |<span data-ttu-id="95c71-314">1</span><span class="sxs-lookup"><span data-stu-id="95c71-314">1</span></span> |<span data-ttu-id="95c71-315">2</span><span class="sxs-lookup"><span data-stu-id="95c71-315">2</span></span> |
| <span data-ttu-id="95c71-316">1</span><span class="sxs-lookup"><span data-stu-id="95c71-316">1</span></span> |<span data-ttu-id="95c71-317">2</span><span class="sxs-lookup"><span data-stu-id="95c71-317">2</span></span> |<span data-ttu-id="95c71-318">3</span><span class="sxs-lookup"><span data-stu-id="95c71-318">3</span></span> |
| <span data-ttu-id="95c71-319">3</span><span class="sxs-lookup"><span data-stu-id="95c71-319">3</span></span> |<span data-ttu-id="95c71-320">0</span><span class="sxs-lookup"><span data-stu-id="95c71-320">0</span></span> |<span data-ttu-id="95c71-321">100</span><span class="sxs-lookup"><span data-stu-id="95c71-321">100</span></span> |
| <span data-ttu-id="95c71-322">3</span><span class="sxs-lookup"><span data-stu-id="95c71-322">3</span></span> |<span data-ttu-id="95c71-323">1</span><span class="sxs-lookup"><span data-stu-id="95c71-323">1</span></span> |<span data-ttu-id="95c71-324">101</span><span class="sxs-lookup"><span data-stu-id="95c71-324">101</span></span> |
| <span data-ttu-id="95c71-325">3</span><span class="sxs-lookup"><span data-stu-id="95c71-325">3</span></span> |<span data-ttu-id="95c71-326">2</span><span class="sxs-lookup"><span data-stu-id="95c71-326">2</span></span> |<span data-ttu-id="95c71-327">102</span><span class="sxs-lookup"><span data-stu-id="95c71-327">102</span></span> |
| <span data-ttu-id="95c71-328">3</span><span class="sxs-lookup"><span data-stu-id="95c71-328">3</span></span> |<span data-ttu-id="95c71-329">3</span><span class="sxs-lookup"><span data-stu-id="95c71-329">3</span></span> |<span data-ttu-id="95c71-330">103</span><span class="sxs-lookup"><span data-stu-id="95c71-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="95c71-331">테이블 “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="95c71-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="95c71-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="95c71-332">pk_int</span></span> | <span data-ttu-id="95c71-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="95c71-333">Map_key</span></span> | <span data-ttu-id="95c71-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="95c71-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95c71-335">1</span><span class="sxs-lookup"><span data-stu-id="95c71-335">1</span></span> |<span data-ttu-id="95c71-336">S1</span><span class="sxs-lookup"><span data-stu-id="95c71-336">S1</span></span> |<span data-ttu-id="95c71-337">A</span><span class="sxs-lookup"><span data-stu-id="95c71-337">A</span></span> |
| <span data-ttu-id="95c71-338">1</span><span class="sxs-lookup"><span data-stu-id="95c71-338">1</span></span> |<span data-ttu-id="95c71-339">S2</span><span class="sxs-lookup"><span data-stu-id="95c71-339">S2</span></span> |<span data-ttu-id="95c71-340">b</span><span class="sxs-lookup"><span data-stu-id="95c71-340">b</span></span> |
| <span data-ttu-id="95c71-341">3</span><span class="sxs-lookup"><span data-stu-id="95c71-341">3</span></span> |<span data-ttu-id="95c71-342">S1</span><span class="sxs-lookup"><span data-stu-id="95c71-342">S1</span></span> |<span data-ttu-id="95c71-343">t</span><span class="sxs-lookup"><span data-stu-id="95c71-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="95c71-344">테이블 “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="95c71-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="95c71-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="95c71-345">pk_int</span></span> | <span data-ttu-id="95c71-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="95c71-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="95c71-347">1</span><span class="sxs-lookup"><span data-stu-id="95c71-347">1</span></span> |<span data-ttu-id="95c71-348">A</span><span class="sxs-lookup"><span data-stu-id="95c71-348">A</span></span> |
| <span data-ttu-id="95c71-349">1</span><span class="sxs-lookup"><span data-stu-id="95c71-349">1</span></span> |<span data-ttu-id="95c71-350">b</span><span class="sxs-lookup"><span data-stu-id="95c71-350">B</span></span> |
| <span data-ttu-id="95c71-351">1</span><span class="sxs-lookup"><span data-stu-id="95c71-351">1</span></span> |<span data-ttu-id="95c71-352">C</span><span class="sxs-lookup"><span data-stu-id="95c71-352">C</span></span> |
| <span data-ttu-id="95c71-353">3</span><span class="sxs-lookup"><span data-stu-id="95c71-353">3</span></span> |<span data-ttu-id="95c71-354">A</span><span class="sxs-lookup"><span data-stu-id="95c71-354">A</span></span> |
| <span data-ttu-id="95c71-355">3</span><span class="sxs-lookup"><span data-stu-id="95c71-355">3</span></span> |<span data-ttu-id="95c71-356">E</span><span class="sxs-lookup"><span data-stu-id="95c71-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="95c71-357">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="95c71-357">Map source to sink columns</span></span>
<span data-ttu-id="95c71-358">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="95c71-359">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="95c71-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="95c71-360">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="95c71-361">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="95c71-362">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="95c71-363">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c71-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="95c71-364">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="95c71-365">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="95c71-365">Performance and Tuning</span></span>
<span data-ttu-id="95c71-366">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95c71-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
