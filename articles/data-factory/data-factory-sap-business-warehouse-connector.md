---
title: "Azure Data Factory를 사용하여 SAP Business Warehouse에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 SAP Business Warehouse에서 데이터를 이동하는 방법을 알아봅니다."
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
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="663b6-103">Azure Data Factory를 사용하여 SAP Business Warehouse에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="663b6-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="663b6-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 SAP BW(Business Warehouse)에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="663b6-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="663b6-106">온-프레미스 SAP Business Warehouse 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="663b6-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="663b6-108">현재 데이터 팩터리는 다른 데이터 저장소에서 SAP Business Warehouse로 데이터를 이동하는 것은 지원하지 않고 SAP Business Warehouse에서 다른 데이터 저장소로 데이터를 이동하는 것만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="663b6-109">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="663b6-109">Supported versions and installation</span></span>
<span data-ttu-id="663b6-110">이 커넥터는 SAP Business Warehouse 버전 7.x를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="663b6-111">MDX 쿼리를 사용하여 InfoCubes 및 QueryCubes(BEx 쿼리 포함)에서 데이터를 복사하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="663b6-112">SAP BW 인스턴스에 대한 연결을 사용하도록 설정하려면 다음 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="663b6-113">**데이터 관리 게이트웨이**: Data Factory 서비스는 데이터 관리 게이트웨이라는 구성 요소를 사용하여 온-프레미스 데이터 저장소(SAP Business Warehouse 포함)에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="663b6-114">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="663b6-115">게이트웨이는 SAP Business Warehouse가 Azure IaaS 가상 컴퓨터(VM)에 호스팅되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="663b6-116">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="663b6-117">게이트웨이 컴퓨터의 **SAP NetWeaver 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="663b6-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="663b6-118">SAP Netweaver 라이브러리는 SAP 관리자를 통해 구하거나 [SAP 소프트웨어 다운로드 센터](https://support.sap.com/swdc)에서 바로 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="663b6-119">최신 버전에 대한 다운로드 위치를 찾으려면 **SAP Note #1025361**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="663b6-120">SAP NetWeaver 라이브러리(32비트 또는 64비트)의 아키텍처가 게이트웨이 설치와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="663b6-121">그런 다음 SAP Note에 따라 SAP NetWeaver RFC SDK에 포함된 모든 파일을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="663b6-122">SAP NetWeaver 라이브러리는 SAP Client Tools 설치에도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="663b6-123">NetWeaver RFC SDK에서 추출된 dll을 system32 폴더에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="663b6-124">시작</span><span class="sxs-lookup"><span data-stu-id="663b6-124">Getting started</span></span>
<span data-ttu-id="663b6-125">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="663b6-126">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="663b6-127">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="663b6-128">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="663b6-129">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="663b6-130">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="663b6-131">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="663b6-132">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="663b6-133">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="663b6-134">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="663b6-135">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="663b6-136">온-프레미스 SAP Business Warehouse의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: SAP Business Warehouse에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="663b6-137">다음 섹션에서는 SAP BW 데이터 저장소에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="663b6-138">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="663b6-138">Linked service properties</span></span>
<span data-ttu-id="663b6-139">다음 테이블은 SAP Business Warehouse(BW) 연결된 서비스에 특정의 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="663b6-140">속성</span><span class="sxs-lookup"><span data-stu-id="663b6-140">Property</span></span> | <span data-ttu-id="663b6-141">설명</span><span class="sxs-lookup"><span data-stu-id="663b6-141">Description</span></span> | <span data-ttu-id="663b6-142">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="663b6-142">Allowed values</span></span> | <span data-ttu-id="663b6-143">필수</span><span class="sxs-lookup"><span data-stu-id="663b6-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="663b6-144">server</span><span class="sxs-lookup"><span data-stu-id="663b6-144">server</span></span> | <span data-ttu-id="663b6-145">SAP BW 인스턴스가 상주하는 서버의 이름.</span><span class="sxs-lookup"><span data-stu-id="663b6-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="663b6-146">string</span><span class="sxs-lookup"><span data-stu-id="663b6-146">string</span></span> | <span data-ttu-id="663b6-147">예</span><span class="sxs-lookup"><span data-stu-id="663b6-147">Yes</span></span>
<span data-ttu-id="663b6-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="663b6-148">systemNumber</span></span> | <span data-ttu-id="663b6-149">SAP BW 시스템의 시스템 번호.</span><span class="sxs-lookup"><span data-stu-id="663b6-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="663b6-150">문자열로 표현되는 두 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="663b6-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="663b6-151">예</span><span class="sxs-lookup"><span data-stu-id="663b6-151">Yes</span></span>
<span data-ttu-id="663b6-152">clientId</span><span class="sxs-lookup"><span data-stu-id="663b6-152">clientId</span></span> | <span data-ttu-id="663b6-153">SAP W 시스템에 있는 클라이언트의 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="663b6-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="663b6-154">문자열로 표현되는 세 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="663b6-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="663b6-155">예</span><span class="sxs-lookup"><span data-stu-id="663b6-155">Yes</span></span>
<span data-ttu-id="663b6-156">username</span><span class="sxs-lookup"><span data-stu-id="663b6-156">username</span></span> | <span data-ttu-id="663b6-157">SAP 서버에 대한 액세스 권한이 있는 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="663b6-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="663b6-158">string</span><span class="sxs-lookup"><span data-stu-id="663b6-158">string</span></span> | <span data-ttu-id="663b6-159">예</span><span class="sxs-lookup"><span data-stu-id="663b6-159">Yes</span></span>
<span data-ttu-id="663b6-160">password</span><span class="sxs-lookup"><span data-stu-id="663b6-160">password</span></span> | <span data-ttu-id="663b6-161">사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-161">Password for the user.</span></span> | <span data-ttu-id="663b6-162">string</span><span class="sxs-lookup"><span data-stu-id="663b6-162">string</span></span> | <span data-ttu-id="663b6-163">예</span><span class="sxs-lookup"><span data-stu-id="663b6-163">Yes</span></span>
<span data-ttu-id="663b6-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="663b6-164">gatewayName</span></span> | <span data-ttu-id="663b6-165">Data Factory 서비스가 온-프레미스 SAP BW 인스턴스에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="663b6-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="663b6-166">string</span><span class="sxs-lookup"><span data-stu-id="663b6-166">string</span></span> | <span data-ttu-id="663b6-167">예</span><span class="sxs-lookup"><span data-stu-id="663b6-167">Yes</span></span>
<span data-ttu-id="663b6-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="663b6-168">encryptedCredential</span></span> | <span data-ttu-id="663b6-169">암호화된 자격 증명 문자열.</span><span class="sxs-lookup"><span data-stu-id="663b6-169">The encrypted credential string.</span></span> | <span data-ttu-id="663b6-170">string</span><span class="sxs-lookup"><span data-stu-id="663b6-170">string</span></span> | <span data-ttu-id="663b6-171">아니요</span><span class="sxs-lookup"><span data-stu-id="663b6-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="663b6-172">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="663b6-172">Dataset properties</span></span>
<span data-ttu-id="663b6-173">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="663b6-174">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="663b6-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="663b6-175">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="663b6-176">**RelationalTable** 형식의 SAP BW 데이터 집합에 대해 지원되는 type별 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="663b6-177">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="663b6-177">Copy activity properties</span></span>
<span data-ttu-id="663b6-178">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="663b6-179">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="663b6-180">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="663b6-181">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="663b6-182">활동 복사의 원본이 **RelationalSource**(SAP BW 포함) 형식인 경우 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="663b6-183">속성</span><span class="sxs-lookup"><span data-stu-id="663b6-183">Property</span></span> | <span data-ttu-id="663b6-184">설명</span><span class="sxs-lookup"><span data-stu-id="663b6-184">Description</span></span> | <span data-ttu-id="663b6-185">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="663b6-185">Allowed values</span></span> | <span data-ttu-id="663b6-186">필수</span><span class="sxs-lookup"><span data-stu-id="663b6-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="663b6-187">쿼리</span><span class="sxs-lookup"><span data-stu-id="663b6-187">query</span></span> | <span data-ttu-id="663b6-188">SAP BW 인스턴스에서 데이터를 읽을 MDX 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="663b6-189">MDX 쿼리.</span><span class="sxs-lookup"><span data-stu-id="663b6-189">MDX query.</span></span> | <span data-ttu-id="663b6-190">예</span><span class="sxs-lookup"><span data-stu-id="663b6-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="663b6-191">JSON 샘플: SAP Business Warehouse에서 Azure Blob에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="663b6-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="663b6-192">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="663b6-193">이 샘플은 온-프레미스 SAP Business Warehouse에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="663b6-194">그러나 Azure Data Factory의 복사 작업을 사용하여 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="663b6-195">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="663b6-196">데이터 팩터리를 만들기 위한 단계별 지침은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="663b6-197">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="663b6-198">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="663b6-199">[SapBw](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="663b6-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="663b6-200">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="663b6-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="663b6-201">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="663b6-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="663b6-202">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="663b6-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="663b6-203">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="663b6-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="663b6-204">샘플은 SAP Business Warehouse 인스턴스에서 Azure Blob으로 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="663b6-205">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="663b6-206">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="663b6-207">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="663b6-208">SAP Business Warehouse 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="663b6-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="663b6-209">이 연결된 서비스는 SAP BW 인스턴스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="663b6-210">type 속성은 **SapBw**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="663b6-211">typeProperties 섹션은 SAP BW 인스턴스에 대한 연결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="663b6-212">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="663b6-212">Azure Storage linked service</span></span>
<span data-ttu-id="663b6-213">이 연결된 서비스는 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="663b6-214">type 속성은 **AzureStorage**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="663b6-215">typeProperties 섹션은 Azure Storage 계정에 대한 연결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="663b6-216">SAP BW 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="663b6-216">SAP BW input dataset</span></span>
<span data-ttu-id="663b6-217">이 데이터 집합은 SAP Business Warehouse 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="663b6-218">Data Factory 데이터 집합의 type은 **RelationalTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="663b6-219">현재 SAP BW 데이터 집합에 대한 type별 속성은 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="663b6-220">활동 복사 정의의 쿼리는 SAP BW 인스턴스에서 읽을 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="663b6-221">external 속성을 true로 설정하면 테이블이 데이터 팩터리의 외부에 있으며 데이터 팩터리의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="663b6-222">frequency 및 interval 속성은 일정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="663b6-223">이런 경우 SAP BW 인스턴스에서 매시간 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="663b6-224">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="663b6-224">Azure Blob output dataset</span></span>
<span data-ttu-id="663b6-225">이 데이터 집합은 출력 Azure Blob 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="663b6-226">type 속성은 AzureBlob으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="663b6-227">typeProperties 섹션은 SAP BW 인스턴스에서 복사한 데이터가 저장되는 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="663b6-228">데이터는 매시간 새 Blob에 기록됩니다(빈도: 1시간, 간격:1회).</span><span class="sxs-lookup"><span data-stu-id="663b6-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="663b6-229">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="663b6-230">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="663b6-231">복사 작업을 포함하는 파이프라인</span><span class="sxs-lookup"><span data-stu-id="663b6-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="663b6-232">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="663b6-233">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고(SAP BW 원본의 경우) **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="663b6-234">**query** 속성에 지정된 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="663b6-235">SAP BW에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="663b6-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="663b6-236">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="663b6-237">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="663b6-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="663b6-238">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="663b6-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="663b6-239">SAP BW의 데이터를 이동하는 경우 SAP BW 형식에서 .NET 형식으로 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="663b6-240">ABAP 사전의 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="663b6-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="663b6-241">.Net 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="663b6-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="663b6-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="663b6-242">ACCP</span></span> |  <span data-ttu-id="663b6-243">int</span><span class="sxs-lookup"><span data-stu-id="663b6-243">Int</span></span>
<span data-ttu-id="663b6-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="663b6-244">CHAR</span></span> | <span data-ttu-id="663b6-245">string</span><span class="sxs-lookup"><span data-stu-id="663b6-245">String</span></span>
<span data-ttu-id="663b6-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="663b6-246">CLNT</span></span> | <span data-ttu-id="663b6-247">string</span><span class="sxs-lookup"><span data-stu-id="663b6-247">String</span></span>
<span data-ttu-id="663b6-248">CURR</span><span class="sxs-lookup"><span data-stu-id="663b6-248">CURR</span></span> | <span data-ttu-id="663b6-249">10진수</span><span class="sxs-lookup"><span data-stu-id="663b6-249">Decimal</span></span>
<span data-ttu-id="663b6-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="663b6-250">CUKY</span></span> | <span data-ttu-id="663b6-251">string</span><span class="sxs-lookup"><span data-stu-id="663b6-251">String</span></span>
<span data-ttu-id="663b6-252">DEC</span><span class="sxs-lookup"><span data-stu-id="663b6-252">DEC</span></span> | <span data-ttu-id="663b6-253">10진수</span><span class="sxs-lookup"><span data-stu-id="663b6-253">Decimal</span></span>
<span data-ttu-id="663b6-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="663b6-254">FLTP</span></span> | <span data-ttu-id="663b6-255">Double</span><span class="sxs-lookup"><span data-stu-id="663b6-255">Double</span></span>
<span data-ttu-id="663b6-256">INT1</span><span class="sxs-lookup"><span data-stu-id="663b6-256">INT1</span></span> | <span data-ttu-id="663b6-257">Byte</span><span class="sxs-lookup"><span data-stu-id="663b6-257">Byte</span></span>
<span data-ttu-id="663b6-258">INT2</span><span class="sxs-lookup"><span data-stu-id="663b6-258">INT2</span></span> | <span data-ttu-id="663b6-259">Int16</span><span class="sxs-lookup"><span data-stu-id="663b6-259">Int16</span></span>
<span data-ttu-id="663b6-260">INT4</span><span class="sxs-lookup"><span data-stu-id="663b6-260">INT4</span></span> | <span data-ttu-id="663b6-261">int</span><span class="sxs-lookup"><span data-stu-id="663b6-261">Int</span></span>
<span data-ttu-id="663b6-262">LANG</span><span class="sxs-lookup"><span data-stu-id="663b6-262">LANG</span></span> | <span data-ttu-id="663b6-263">String</span><span class="sxs-lookup"><span data-stu-id="663b6-263">String</span></span>
<span data-ttu-id="663b6-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="663b6-264">LCHR</span></span> | <span data-ttu-id="663b6-265">String</span><span class="sxs-lookup"><span data-stu-id="663b6-265">String</span></span>
<span data-ttu-id="663b6-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="663b6-266">LRAW</span></span> | <span data-ttu-id="663b6-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="663b6-267">Byte[]</span></span>
<span data-ttu-id="663b6-268">PREC</span><span class="sxs-lookup"><span data-stu-id="663b6-268">PREC</span></span> | <span data-ttu-id="663b6-269">Int16</span><span class="sxs-lookup"><span data-stu-id="663b6-269">Int16</span></span>
<span data-ttu-id="663b6-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="663b6-270">QUAN</span></span> | <span data-ttu-id="663b6-271">10진수</span><span class="sxs-lookup"><span data-stu-id="663b6-271">Decimal</span></span>
<span data-ttu-id="663b6-272">RAW</span><span class="sxs-lookup"><span data-stu-id="663b6-272">RAW</span></span> | <span data-ttu-id="663b6-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="663b6-273">Byte[]</span></span>
<span data-ttu-id="663b6-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="663b6-274">RAWSTRING</span></span> | <span data-ttu-id="663b6-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="663b6-275">Byte[]</span></span>
<span data-ttu-id="663b6-276">STRING</span><span class="sxs-lookup"><span data-stu-id="663b6-276">STRING</span></span> | <span data-ttu-id="663b6-277">String</span><span class="sxs-lookup"><span data-stu-id="663b6-277">String</span></span>
<span data-ttu-id="663b6-278">단위</span><span class="sxs-lookup"><span data-stu-id="663b6-278">UNIT</span></span> | <span data-ttu-id="663b6-279">string</span><span class="sxs-lookup"><span data-stu-id="663b6-279">String</span></span>
<span data-ttu-id="663b6-280">DATS</span><span class="sxs-lookup"><span data-stu-id="663b6-280">DATS</span></span> | <span data-ttu-id="663b6-281">string</span><span class="sxs-lookup"><span data-stu-id="663b6-281">String</span></span>
<span data-ttu-id="663b6-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="663b6-282">NUMC</span></span> | <span data-ttu-id="663b6-283">string</span><span class="sxs-lookup"><span data-stu-id="663b6-283">String</span></span>
<span data-ttu-id="663b6-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="663b6-284">TIMS</span></span> | <span data-ttu-id="663b6-285">string</span><span class="sxs-lookup"><span data-stu-id="663b6-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="663b6-286">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="663b6-287">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="663b6-287">Map source to sink columns</span></span>
<span data-ttu-id="663b6-288">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="663b6-289">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="663b6-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="663b6-290">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="663b6-291">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="663b6-292">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="663b6-293">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="663b6-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="663b6-294">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="663b6-295">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="663b6-295">Performance and Tuning</span></span>
<span data-ttu-id="663b6-296">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="663b6-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
