---
title: "Azure Data Factory를 사용하여 Sybase에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 Sybase 데이터베이스에서 데이터를 이동하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="d6f3d-103">Azure 데이터 팩터리를 사용하여 Sybase에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="d6f3d-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="d6f3d-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 Sybase 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="d6f3d-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d6f3d-106">온-프레미스 Sybase 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="d6f3d-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d6f3d-108">현재 데이터 팩터리는 다른 데이터 저장소에서 Sybase 데이터 저장소로 데이터 이동이 아닌 Sybase 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d6f3d-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6f3d-109">Prerequisites</span></span>
<span data-ttu-id="d6f3d-110">데이터 팩터리 서비스는 데이터 관리 게이트웨이를 사용하여 온-프레미스 Sybase 원본에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="d6f3d-111">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="d6f3d-112">게이트웨이는 Sybase 데이터베이스가 Azure IaaS VM에 호스팅되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="d6f3d-113">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 IaaS VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="d6f3d-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="d6f3d-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="d6f3d-115">Supported versions and installation</span></span>
<span data-ttu-id="d6f3d-116">Sybase 데이터베이스에 연결할 데이터 관리 게이트웨이의 경우 데이터 관리 게이트웨이와 동일한 시스템에 [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="d6f3d-117">Sybase 버전 16 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d6f3d-118">시작</span><span class="sxs-lookup"><span data-stu-id="d6f3d-118">Getting started</span></span>
<span data-ttu-id="d6f3d-119">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="d6f3d-120">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d6f3d-121">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="d6f3d-122">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d6f3d-123">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d6f3d-124">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d6f3d-125">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d6f3d-126">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d6f3d-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d6f3d-128">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d6f3d-129">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d6f3d-130">온-프레미스 Sybase의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: Sybase에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-sybase-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d6f3d-131">다음 섹션에서는 Sybase 데이터 저장소에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d6f3d-132">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-132">Linked service properties</span></span>
<span data-ttu-id="d6f3d-133">다음 표에서는 Sybase 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="d6f3d-134">속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-134">Property</span></span> | <span data-ttu-id="d6f3d-135">설명</span><span class="sxs-lookup"><span data-stu-id="d6f3d-135">Description</span></span> | <span data-ttu-id="d6f3d-136">필수</span><span class="sxs-lookup"><span data-stu-id="d6f3d-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6f3d-137">type</span><span class="sxs-lookup"><span data-stu-id="d6f3d-137">type</span></span> |<span data-ttu-id="d6f3d-138">형식 속성은 **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="d6f3d-139">예</span><span class="sxs-lookup"><span data-stu-id="d6f3d-139">Yes</span></span> |
| <span data-ttu-id="d6f3d-140">server</span><span class="sxs-lookup"><span data-stu-id="d6f3d-140">server</span></span> |<span data-ttu-id="d6f3d-141">Sybase 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-141">Name of the Sybase server.</span></span> |<span data-ttu-id="d6f3d-142">예</span><span class="sxs-lookup"><span data-stu-id="d6f3d-142">Yes</span></span> |
| <span data-ttu-id="d6f3d-143">database</span><span class="sxs-lookup"><span data-stu-id="d6f3d-143">database</span></span> |<span data-ttu-id="d6f3d-144">Sybase 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-144">Name of the Sybase database.</span></span> |<span data-ttu-id="d6f3d-145">예</span><span class="sxs-lookup"><span data-stu-id="d6f3d-145">Yes</span></span> |
| <span data-ttu-id="d6f3d-146">schema</span><span class="sxs-lookup"><span data-stu-id="d6f3d-146">schema</span></span> |<span data-ttu-id="d6f3d-147">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-147">Name of the schema in the database.</span></span> |<span data-ttu-id="d6f3d-148">아니요</span><span class="sxs-lookup"><span data-stu-id="d6f3d-148">No</span></span> |
| <span data-ttu-id="d6f3d-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6f3d-149">authenticationType</span></span> |<span data-ttu-id="d6f3d-150">Sybase 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="d6f3d-151">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6f3d-152">예</span><span class="sxs-lookup"><span data-stu-id="d6f3d-152">Yes</span></span> |
| <span data-ttu-id="d6f3d-153">username</span><span class="sxs-lookup"><span data-stu-id="d6f3d-153">username</span></span> |<span data-ttu-id="d6f3d-154">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="d6f3d-155">아니요</span><span class="sxs-lookup"><span data-stu-id="d6f3d-155">No</span></span> |
| <span data-ttu-id="d6f3d-156">password</span><span class="sxs-lookup"><span data-stu-id="d6f3d-156">password</span></span> |<span data-ttu-id="d6f3d-157">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="d6f3d-158">아니요</span><span class="sxs-lookup"><span data-stu-id="d6f3d-158">No</span></span> |
| <span data-ttu-id="d6f3d-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6f3d-159">gatewayName</span></span> |<span data-ttu-id="d6f3d-160">데이터 팩터리 서비스가 온-프레미스 Sybase 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="d6f3d-161">예</span><span class="sxs-lookup"><span data-stu-id="d6f3d-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d6f3d-162">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-162">Dataset properties</span></span>
<span data-ttu-id="d6f3d-163">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d6f3d-164">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="d6f3d-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d6f3d-165">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d6f3d-166">**RelationalTable** 형식의 데이터 집합(Sybase 데이터 집합을 포함)에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="d6f3d-167">속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-167">Property</span></span> | <span data-ttu-id="d6f3d-168">설명</span><span class="sxs-lookup"><span data-stu-id="d6f3d-168">Description</span></span> | <span data-ttu-id="d6f3d-169">필수</span><span class="sxs-lookup"><span data-stu-id="d6f3d-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6f3d-170">tableName</span><span class="sxs-lookup"><span data-stu-id="d6f3d-170">tableName</span></span> |<span data-ttu-id="d6f3d-171">연결된 서비스가 참조하는 Sybase 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6f3d-172">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d6f3d-173">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-173">Copy activity properties</span></span>
<span data-ttu-id="d6f3d-174">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d6f3d-175">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="d6f3d-176">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="d6f3d-177">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d6f3d-178">원본이 **RelationalSource**(Sybase 포함) 형식인 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d6f3d-179">속성</span><span class="sxs-lookup"><span data-stu-id="d6f3d-179">Property</span></span> | <span data-ttu-id="d6f3d-180">설명</span><span class="sxs-lookup"><span data-stu-id="d6f3d-180">Description</span></span> | <span data-ttu-id="d6f3d-181">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="d6f3d-181">Allowed values</span></span> | <span data-ttu-id="d6f3d-182">필수</span><span class="sxs-lookup"><span data-stu-id="d6f3d-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6f3d-183">쿼리</span><span class="sxs-lookup"><span data-stu-id="d6f3d-183">query</span></span> |<span data-ttu-id="d6f3d-184">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-184">Use the custom query to read data.</span></span> |<span data-ttu-id="d6f3d-185">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-185">SQL query string.</span></span> <span data-ttu-id="d6f3d-186">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="d6f3d-187">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="d6f3d-188">JSON 예: Sybase에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="d6f3d-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="d6f3d-189">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d6f3d-190">이 샘플은 Sybase 데이터베이스에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="d6f3d-191">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="d6f3d-192">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d6f3d-193">[OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d6f3d-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="d6f3d-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d6f3d-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d6f3d-195">[RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d6f3d-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d6f3d-197">[RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d6f3d-198">샘플은 Sybase 데이터베이스의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="d6f3d-199">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d6f3d-200">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="d6f3d-201">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="d6f3d-202">**Sybase 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="d6f3d-203">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="d6f3d-204">**Sybase 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="d6f3d-205">샘플은 Sybase에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestamp" 라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="d6f3d-206">"external": true를 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="d6f3d-207">연결된 서비스의 **type**을 **RelationalTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="d6f3d-208">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d6f3d-209">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="d6f3d-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d6f3d-210">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d6f3d-211">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="d6f3d-212">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="d6f3d-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="d6f3d-213">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="d6f3d-214">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d6f3d-215">**query** 속성에 지정된 SQL 쿼리는 데이터베이스의 DBA.Orders 테이블에서 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="d6f3d-216">Sybase에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="d6f3d-216">Type mapping for Sybase</span></span>
<span data-ttu-id="d6f3d-217">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼, 복사 활동은 다음과 같은 2단계 방식을 사용해 소스 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d6f3d-218">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="d6f3d-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d6f3d-219">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="d6f3d-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d6f3d-220">Sybase는 T-SQL 및 T-SQL 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="d6f3d-221">sql 형식에서 .NET 형식으로의 매핑 테이블은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d6f3d-222">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="d6f3d-222">Map source to sink columns</span></span>
<span data-ttu-id="d6f3d-223">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d6f3d-224">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="d6f3d-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="d6f3d-225">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d6f3d-226">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d6f3d-227">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d6f3d-228">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d6f3d-229">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d6f3d-230">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="d6f3d-230">Performance and Tuning</span></span>
<span data-ttu-id="d6f3d-231">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6f3d-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
