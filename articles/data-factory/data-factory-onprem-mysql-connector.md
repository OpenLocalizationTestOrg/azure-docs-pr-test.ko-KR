---
title: "Azure Data Factory를 사용하여 MySQL에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 MySQL 데이터베이스에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="86baa-103">Azure 데이터 팩터리를 사용하여 MySQL에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="86baa-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="86baa-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 MySQL 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="86baa-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="86baa-106">온-프레미스 MySQL 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="86baa-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="86baa-108">현재 데이터 팩터리는 다른 데이터 저장소에서 MySQL 데이터 저장소로 데이터 이동이 아닌 MySQL 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="86baa-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="86baa-109">Prerequisites</span></span>
<span data-ttu-id="86baa-110">데이터 팩터리 서비스는 데이터 관리 게이트웨이를 사용하여 온-프레미스 MySQL 원본에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="86baa-111">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="86baa-112">게이트웨이는 MySQL 데이터베이스가 Azure IaaS 가상 컴퓨터 (VM)에 호스팅되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="86baa-113">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="86baa-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="86baa-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="86baa-115">Supported versions and installation</span></span>
<span data-ttu-id="86baa-116">MySQL 데이터베이스에 연결할 데이터 관리 게이트웨이의 경우 데이터 관리 게이트웨이와 동일한 시스템에 [MySQL 커넥터/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/)(버전 6.6.5 이상)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="86baa-117">MySQL 버전 5.1 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="86baa-118">"원격측에서 전송 스트림을 닫았으므로 인증에 실패했습니다." 오류가 발생할 경우 MySQL 커넥터/Net을 더 높은 버전으로 업그레이드하는 방안을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="86baa-119">시작</span><span class="sxs-lookup"><span data-stu-id="86baa-119">Getting started</span></span>
<span data-ttu-id="86baa-120">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="86baa-121">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="86baa-122">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="86baa-123">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="86baa-124">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="86baa-125">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="86baa-126">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="86baa-127">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="86baa-128">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="86baa-129">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="86baa-130">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="86baa-131">온-프레미스 MySQL의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: MySQL에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-mysql-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="86baa-132">다음 섹션에서는 MySQL 데이터 저장소에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="86baa-133">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="86baa-133">Linked service properties</span></span>
<span data-ttu-id="86baa-134">다음 테이블은 MySQL 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="86baa-135">속성</span><span class="sxs-lookup"><span data-stu-id="86baa-135">Property</span></span> | <span data-ttu-id="86baa-136">설명</span><span class="sxs-lookup"><span data-stu-id="86baa-136">Description</span></span> | <span data-ttu-id="86baa-137">필수</span><span class="sxs-lookup"><span data-stu-id="86baa-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86baa-138">type</span><span class="sxs-lookup"><span data-stu-id="86baa-138">type</span></span> |<span data-ttu-id="86baa-139">형식 속성은 **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="86baa-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="86baa-140">예</span><span class="sxs-lookup"><span data-stu-id="86baa-140">Yes</span></span> |
| <span data-ttu-id="86baa-141">server</span><span class="sxs-lookup"><span data-stu-id="86baa-141">server</span></span> |<span data-ttu-id="86baa-142">MySQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-142">Name of the MySQL server.</span></span> |<span data-ttu-id="86baa-143">예</span><span class="sxs-lookup"><span data-stu-id="86baa-143">Yes</span></span> |
| <span data-ttu-id="86baa-144">database</span><span class="sxs-lookup"><span data-stu-id="86baa-144">database</span></span> |<span data-ttu-id="86baa-145">MySQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-145">Name of the MySQL database.</span></span> |<span data-ttu-id="86baa-146">예</span><span class="sxs-lookup"><span data-stu-id="86baa-146">Yes</span></span> |
| <span data-ttu-id="86baa-147">schema</span><span class="sxs-lookup"><span data-stu-id="86baa-147">schema</span></span> |<span data-ttu-id="86baa-148">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-148">Name of the schema in the database.</span></span> |<span data-ttu-id="86baa-149">아니요</span><span class="sxs-lookup"><span data-stu-id="86baa-149">No</span></span> |
| <span data-ttu-id="86baa-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="86baa-150">authenticationType</span></span> |<span data-ttu-id="86baa-151">MySQL 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="86baa-152">가능한 값은 `Basic`입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="86baa-153">예</span><span class="sxs-lookup"><span data-stu-id="86baa-153">Yes</span></span> |
| <span data-ttu-id="86baa-154">username</span><span class="sxs-lookup"><span data-stu-id="86baa-154">username</span></span> |<span data-ttu-id="86baa-155">MySQL 데이터베이스에 연결할 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="86baa-156">예</span><span class="sxs-lookup"><span data-stu-id="86baa-156">Yes</span></span> |
| <span data-ttu-id="86baa-157">password</span><span class="sxs-lookup"><span data-stu-id="86baa-157">password</span></span> |<span data-ttu-id="86baa-158">지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="86baa-159">예</span><span class="sxs-lookup"><span data-stu-id="86baa-159">Yes</span></span> |
| <span data-ttu-id="86baa-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="86baa-160">gatewayName</span></span> |<span data-ttu-id="86baa-161">데이터 팩터리 서비스가 온-프레미스 MySQL 데이터 베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="86baa-162">예</span><span class="sxs-lookup"><span data-stu-id="86baa-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="86baa-163">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="86baa-163">Dataset properties</span></span>
<span data-ttu-id="86baa-164">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="86baa-165">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="86baa-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="86baa-166">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="86baa-167">**RelationalTable** 형식의 데이터 집합(MySQL 데이터 집합을 포함)에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="86baa-168">속성</span><span class="sxs-lookup"><span data-stu-id="86baa-168">Property</span></span> | <span data-ttu-id="86baa-169">설명</span><span class="sxs-lookup"><span data-stu-id="86baa-169">Description</span></span> | <span data-ttu-id="86baa-170">필수</span><span class="sxs-lookup"><span data-stu-id="86baa-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86baa-171">tableName</span><span class="sxs-lookup"><span data-stu-id="86baa-171">tableName</span></span> |<span data-ttu-id="86baa-172">연결된 서비스가 참조하는 MySQL 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="86baa-173">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="86baa-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="86baa-174">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="86baa-174">Copy activity properties</span></span>
<span data-ttu-id="86baa-175">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="86baa-176">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="86baa-177">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="86baa-178">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="86baa-179">복사 작업의 원본이 **RelationalSource**(MySQL 포함) 형식인 경우 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="86baa-180">속성</span><span class="sxs-lookup"><span data-stu-id="86baa-180">Property</span></span> | <span data-ttu-id="86baa-181">설명</span><span class="sxs-lookup"><span data-stu-id="86baa-181">Description</span></span> | <span data-ttu-id="86baa-182">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="86baa-182">Allowed values</span></span> | <span data-ttu-id="86baa-183">필수</span><span class="sxs-lookup"><span data-stu-id="86baa-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="86baa-184">쿼리</span><span class="sxs-lookup"><span data-stu-id="86baa-184">query</span></span> |<span data-ttu-id="86baa-185">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-185">Use the custom query to read data.</span></span> |<span data-ttu-id="86baa-186">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="86baa-186">SQL query string.</span></span> <span data-ttu-id="86baa-187">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="86baa-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="86baa-188">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="86baa-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="86baa-189">JSON 예: MySQL에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="86baa-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="86baa-190">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="86baa-191">온-프레미스 MySQL 데이터베이스에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="86baa-192">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86baa-193">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="86baa-194">데이터 팩터리를 만들기 위한 단계별 지침은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="86baa-195">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="86baa-196">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="86baa-197">[OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="86baa-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="86baa-198">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="86baa-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="86baa-199">[RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="86baa-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="86baa-200">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="86baa-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="86baa-201">[RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="86baa-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="86baa-202">샘플은 MySQL 데이터베이스의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="86baa-203">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="86baa-204">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="86baa-205">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="86baa-206">**MySQL 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="86baa-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="86baa-207">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="86baa-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="86baa-208">**MySQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="86baa-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="86baa-209">샘플은 MySQL에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn"이라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="86baa-210">"external": true를 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="86baa-211">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="86baa-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="86baa-212">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="86baa-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="86baa-213">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="86baa-214">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="86baa-215">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="86baa-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="86baa-216">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="86baa-217">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="86baa-218">**query** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="86baa-219">MySQL에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="86baa-219">Type mapping for MySQL</span></span>
<span data-ttu-id="86baa-220">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법을 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="86baa-221">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="86baa-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="86baa-222">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="86baa-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="86baa-223">MySQL에 데이터를 이동하는 경우 MySQL 형식에서 .NET 형식으로 이동에 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="86baa-224">MySQL 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="86baa-224">MySQL Database type</span></span> | <span data-ttu-id="86baa-225">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="86baa-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="86baa-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-226">bigint unsigned</span></span> |<span data-ttu-id="86baa-227">10진수</span><span class="sxs-lookup"><span data-stu-id="86baa-227">Decimal</span></span> |
| <span data-ttu-id="86baa-228">bigint</span><span class="sxs-lookup"><span data-stu-id="86baa-228">bigint</span></span> |<span data-ttu-id="86baa-229">Int64</span><span class="sxs-lookup"><span data-stu-id="86baa-229">Int64</span></span> |
| <span data-ttu-id="86baa-230">bit</span><span class="sxs-lookup"><span data-stu-id="86baa-230">bit</span></span> |<span data-ttu-id="86baa-231">10진수</span><span class="sxs-lookup"><span data-stu-id="86baa-231">Decimal</span></span> |
| <span data-ttu-id="86baa-232">Blob</span><span class="sxs-lookup"><span data-stu-id="86baa-232">blob</span></span> |<span data-ttu-id="86baa-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86baa-233">Byte[]</span></span> |
| <span data-ttu-id="86baa-234">bool</span><span class="sxs-lookup"><span data-stu-id="86baa-234">bool</span></span> |<span data-ttu-id="86baa-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="86baa-235">Boolean</span></span> |
| <span data-ttu-id="86baa-236">char</span><span class="sxs-lookup"><span data-stu-id="86baa-236">char</span></span> |<span data-ttu-id="86baa-237">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-237">String</span></span> |
| <span data-ttu-id="86baa-238">date</span><span class="sxs-lookup"><span data-stu-id="86baa-238">date</span></span> |<span data-ttu-id="86baa-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="86baa-239">Datetime</span></span> |
| <span data-ttu-id="86baa-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="86baa-240">datetime</span></span> |<span data-ttu-id="86baa-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="86baa-241">Datetime</span></span> |
| <span data-ttu-id="86baa-242">10진수</span><span class="sxs-lookup"><span data-stu-id="86baa-242">decimal</span></span> |<span data-ttu-id="86baa-243">10진수</span><span class="sxs-lookup"><span data-stu-id="86baa-243">Decimal</span></span> |
| <span data-ttu-id="86baa-244">double precision</span><span class="sxs-lookup"><span data-stu-id="86baa-244">double precision</span></span> |<span data-ttu-id="86baa-245">Double</span><span class="sxs-lookup"><span data-stu-id="86baa-245">Double</span></span> |
| <span data-ttu-id="86baa-246">Double</span><span class="sxs-lookup"><span data-stu-id="86baa-246">double</span></span> |<span data-ttu-id="86baa-247">Double</span><span class="sxs-lookup"><span data-stu-id="86baa-247">Double</span></span> |
| <span data-ttu-id="86baa-248">enum</span><span class="sxs-lookup"><span data-stu-id="86baa-248">enum</span></span> |<span data-ttu-id="86baa-249">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-249">String</span></span> |
| <span data-ttu-id="86baa-250">float</span><span class="sxs-lookup"><span data-stu-id="86baa-250">float</span></span> |<span data-ttu-id="86baa-251">Single</span><span class="sxs-lookup"><span data-stu-id="86baa-251">Single</span></span> |
| <span data-ttu-id="86baa-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-252">int unsigned</span></span> |<span data-ttu-id="86baa-253">Int64</span><span class="sxs-lookup"><span data-stu-id="86baa-253">Int64</span></span> |
| <span data-ttu-id="86baa-254">int</span><span class="sxs-lookup"><span data-stu-id="86baa-254">int</span></span> |<span data-ttu-id="86baa-255">Int32</span><span class="sxs-lookup"><span data-stu-id="86baa-255">Int32</span></span> |
| <span data-ttu-id="86baa-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-256">integer unsigned</span></span> |<span data-ttu-id="86baa-257">Int64</span><span class="sxs-lookup"><span data-stu-id="86baa-257">Int64</span></span> |
| <span data-ttu-id="86baa-258">정수</span><span class="sxs-lookup"><span data-stu-id="86baa-258">integer</span></span> |<span data-ttu-id="86baa-259">Int32</span><span class="sxs-lookup"><span data-stu-id="86baa-259">Int32</span></span> |
| <span data-ttu-id="86baa-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="86baa-260">long varbinary</span></span> |<span data-ttu-id="86baa-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86baa-261">Byte[]</span></span> |
| <span data-ttu-id="86baa-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="86baa-262">long varchar</span></span> |<span data-ttu-id="86baa-263">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-263">String</span></span> |
| <span data-ttu-id="86baa-264">longblob</span><span class="sxs-lookup"><span data-stu-id="86baa-264">longblob</span></span> |<span data-ttu-id="86baa-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86baa-265">Byte[]</span></span> |
| <span data-ttu-id="86baa-266">longtext</span><span class="sxs-lookup"><span data-stu-id="86baa-266">longtext</span></span> |<span data-ttu-id="86baa-267">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-267">String</span></span> |
| <span data-ttu-id="86baa-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="86baa-268">mediumblob</span></span> |<span data-ttu-id="86baa-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86baa-269">Byte[]</span></span> |
| <span data-ttu-id="86baa-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-270">mediumint unsigned</span></span> |<span data-ttu-id="86baa-271">Int64</span><span class="sxs-lookup"><span data-stu-id="86baa-271">Int64</span></span> |
| <span data-ttu-id="86baa-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="86baa-272">mediumint</span></span> |<span data-ttu-id="86baa-273">Int32</span><span class="sxs-lookup"><span data-stu-id="86baa-273">Int32</span></span> |
| <span data-ttu-id="86baa-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="86baa-274">mediumtext</span></span> |<span data-ttu-id="86baa-275">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-275">String</span></span> |
| <span data-ttu-id="86baa-276">numeric</span><span class="sxs-lookup"><span data-stu-id="86baa-276">numeric</span></span> |<span data-ttu-id="86baa-277">10진수</span><span class="sxs-lookup"><span data-stu-id="86baa-277">Decimal</span></span> |
| <span data-ttu-id="86baa-278">real</span><span class="sxs-lookup"><span data-stu-id="86baa-278">real</span></span> |<span data-ttu-id="86baa-279">Double</span><span class="sxs-lookup"><span data-stu-id="86baa-279">Double</span></span> |
| <span data-ttu-id="86baa-280">set</span><span class="sxs-lookup"><span data-stu-id="86baa-280">set</span></span> |<span data-ttu-id="86baa-281">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-281">String</span></span> |
| <span data-ttu-id="86baa-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-282">smallint unsigned</span></span> |<span data-ttu-id="86baa-283">Int32</span><span class="sxs-lookup"><span data-stu-id="86baa-283">Int32</span></span> |
| <span data-ttu-id="86baa-284">smallint</span><span class="sxs-lookup"><span data-stu-id="86baa-284">smallint</span></span> |<span data-ttu-id="86baa-285">Int16</span><span class="sxs-lookup"><span data-stu-id="86baa-285">Int16</span></span> |
| <span data-ttu-id="86baa-286">텍스트</span><span class="sxs-lookup"><span data-stu-id="86baa-286">text</span></span> |<span data-ttu-id="86baa-287">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-287">String</span></span> |
| <span data-ttu-id="86baa-288">실시간</span><span class="sxs-lookup"><span data-stu-id="86baa-288">time</span></span> |<span data-ttu-id="86baa-289">timespan</span><span class="sxs-lookup"><span data-stu-id="86baa-289">TimeSpan</span></span> |
| <span data-ttu-id="86baa-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="86baa-290">timestamp</span></span> |<span data-ttu-id="86baa-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="86baa-291">Datetime</span></span> |
| <span data-ttu-id="86baa-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="86baa-292">tinyblob</span></span> |<span data-ttu-id="86baa-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86baa-293">Byte[]</span></span> |
| <span data-ttu-id="86baa-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="86baa-294">tinyint unsigned</span></span> |<span data-ttu-id="86baa-295">Int16</span><span class="sxs-lookup"><span data-stu-id="86baa-295">Int16</span></span> |
| <span data-ttu-id="86baa-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="86baa-296">tinyint</span></span> |<span data-ttu-id="86baa-297">Int16</span><span class="sxs-lookup"><span data-stu-id="86baa-297">Int16</span></span> |
| <span data-ttu-id="86baa-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="86baa-298">tinytext</span></span> |<span data-ttu-id="86baa-299">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-299">String</span></span> |
| <span data-ttu-id="86baa-300">varchar</span><span class="sxs-lookup"><span data-stu-id="86baa-300">varchar</span></span> |<span data-ttu-id="86baa-301">문자열</span><span class="sxs-lookup"><span data-stu-id="86baa-301">String</span></span> |
| <span data-ttu-id="86baa-302">year</span><span class="sxs-lookup"><span data-stu-id="86baa-302">year</span></span> |<span data-ttu-id="86baa-303">int</span><span class="sxs-lookup"><span data-stu-id="86baa-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="86baa-304">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="86baa-304">Map source to sink columns</span></span>
<span data-ttu-id="86baa-305">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="86baa-306">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="86baa-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="86baa-307">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="86baa-308">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="86baa-309">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="86baa-310">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86baa-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="86baa-311">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="86baa-312">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="86baa-312">Performance and Tuning</span></span>
<span data-ttu-id="86baa-313">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86baa-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
