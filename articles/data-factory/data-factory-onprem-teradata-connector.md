---
title: "Azure Data Factory를 사용하여 Teradata에서 데이터 이동 | Microsoft Docs"
description: "Teradata 데이터베이스에서 데이터를 이동시킬 수 있는 데이터 팩터리 서비스용 Teradata 커넥터에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="226a4-103">Azure 데이터 팩터리를 사용하여 Teradata에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="226a4-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="226a4-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 Teradata 데이터베이스에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="226a4-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="226a4-106">온-프레미스 Teradata 데이터 저장소의 데이터를 지원되는 싱크 데이터 저장소로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="226a4-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="226a4-108">현재 데이터 팩터리는 다른 데이터 저장소에서 Teradata 데이터 저장소로 데이터 이동이 아닌 Teradata 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="226a4-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="226a4-109">Prerequisites</span></span>
<span data-ttu-id="226a4-110">데이터 팩터리는 데이터 관리 게이트웨이를 통해 온-프레미스 Teradata 원본에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="226a4-111">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="226a4-112">게이트웨이는 Teradata가 Azure IaaS VM에 호스팅되더라도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="226a4-113">게이트웨이를 데이터베이스에 연결할 수 있는 한 데이터 저장소와 동일한 IaaS VM 또는 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="226a4-114">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="226a4-115">지원되는 버전 및 설치</span><span class="sxs-lookup"><span data-stu-id="226a4-115">Supported versions and installation</span></span>
<span data-ttu-id="226a4-116">Teradata 데이터베이스에 연결할 데이터 관리 게이트웨이의 경우 데이터 관리 게이트웨이와 동일한 시스템에 [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) 버전 14 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="226a4-117">Teradata 버전 12 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="226a4-118">시작</span><span class="sxs-lookup"><span data-stu-id="226a4-118">Getting started</span></span>
<span data-ttu-id="226a4-119">여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="226a4-120">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="226a4-121">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="226a4-122">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="226a4-123">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="226a4-124">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="226a4-125">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="226a4-126">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="226a4-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="226a4-128">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="226a4-129">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="226a4-130">온-프레미스 Teradata의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: Teradata에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-teradata-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="226a4-131">다음 섹션에서는 Teradata 데이터 저장소에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="226a4-132">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="226a4-132">Linked service properties</span></span>
<span data-ttu-id="226a4-133">다음 표에서는 Teradata 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="226a4-134">속성</span><span class="sxs-lookup"><span data-stu-id="226a4-134">Property</span></span> | <span data-ttu-id="226a4-135">설명</span><span class="sxs-lookup"><span data-stu-id="226a4-135">Description</span></span> | <span data-ttu-id="226a4-136">필수</span><span class="sxs-lookup"><span data-stu-id="226a4-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="226a4-137">type</span><span class="sxs-lookup"><span data-stu-id="226a4-137">type</span></span> |<span data-ttu-id="226a4-138">형식 속성은 **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="226a4-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="226a4-139">예</span><span class="sxs-lookup"><span data-stu-id="226a4-139">Yes</span></span> |
| <span data-ttu-id="226a4-140">server</span><span class="sxs-lookup"><span data-stu-id="226a4-140">server</span></span> |<span data-ttu-id="226a4-141">Teradata 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-141">Name of the Teradata server.</span></span> |<span data-ttu-id="226a4-142">예</span><span class="sxs-lookup"><span data-stu-id="226a4-142">Yes</span></span> |
| <span data-ttu-id="226a4-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="226a4-143">authenticationType</span></span> |<span data-ttu-id="226a4-144">Teradata 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="226a4-145">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="226a4-146">예</span><span class="sxs-lookup"><span data-stu-id="226a4-146">Yes</span></span> |
| <span data-ttu-id="226a4-147">username</span><span class="sxs-lookup"><span data-stu-id="226a4-147">username</span></span> |<span data-ttu-id="226a4-148">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="226a4-149">아니요</span><span class="sxs-lookup"><span data-stu-id="226a4-149">No</span></span> |
| <span data-ttu-id="226a4-150">password</span><span class="sxs-lookup"><span data-stu-id="226a4-150">password</span></span> |<span data-ttu-id="226a4-151">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="226a4-152">아니요</span><span class="sxs-lookup"><span data-stu-id="226a4-152">No</span></span> |
| <span data-ttu-id="226a4-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="226a4-153">gatewayName</span></span> |<span data-ttu-id="226a4-154">데이터 팩터리 서비스가 온-프레미스 Teradata 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="226a4-155">예</span><span class="sxs-lookup"><span data-stu-id="226a4-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="226a4-156">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="226a4-156">Dataset properties</span></span>
<span data-ttu-id="226a4-157">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="226a4-158">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="226a4-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="226a4-159">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="226a4-160">현재 Teradata 데이터 집합에 대해 지원되는 형식 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="226a4-161">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="226a4-161">Copy activity properties</span></span>
<span data-ttu-id="226a4-162">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="226a4-163">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="226a4-164">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="226a4-165">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="226a4-166">원본이 **RelationalSource**(Teradata 포함) 형식인 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="226a4-167">속성</span><span class="sxs-lookup"><span data-stu-id="226a4-167">Property</span></span> | <span data-ttu-id="226a4-168">설명</span><span class="sxs-lookup"><span data-stu-id="226a4-168">Description</span></span> | <span data-ttu-id="226a4-169">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="226a4-169">Allowed values</span></span> | <span data-ttu-id="226a4-170">필수</span><span class="sxs-lookup"><span data-stu-id="226a4-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="226a4-171">쿼리</span><span class="sxs-lookup"><span data-stu-id="226a4-171">query</span></span> |<span data-ttu-id="226a4-172">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-172">Use the custom query to read data.</span></span> |<span data-ttu-id="226a4-173">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="226a4-173">SQL query string.</span></span> <span data-ttu-id="226a4-174">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="226a4-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="226a4-175">예</span><span class="sxs-lookup"><span data-stu-id="226a4-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="226a4-176">JSON 예: Teradata에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="226a4-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="226a4-177">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="226a4-178">이 샘플은 Teradata에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="226a4-179">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="226a4-180">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="226a4-181">[OnPremisesTeradata](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="226a4-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="226a4-182">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="226a4-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="226a4-183">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="226a4-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="226a4-184">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="226a4-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="226a4-185">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="226a4-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="226a4-186">샘플은 Teradata 데이터베이스의 쿼리 결과에서 blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="226a4-187">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="226a4-188">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="226a4-189">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="226a4-190">**Teradata 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="226a4-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="226a4-191">**Azure Blob 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="226a4-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="226a4-192">**Teradata 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="226a4-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="226a4-193">샘플은 Teradata에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestamp"라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="226a4-194">"external": true를 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="226a4-195">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="226a4-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="226a4-196">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="226a4-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="226a4-197">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="226a4-198">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="226a4-199">**복사 작업을 포함하는 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="226a4-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="226a4-200">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="226a4-201">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="226a4-202">**query** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="226a4-203">Teradata에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="226a4-203">Type mapping for Teradata</span></span>
<span data-ttu-id="226a4-204">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼, 복사 활동은 다음과 같은 2단계 방식을 사용해 소스 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="226a4-205">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="226a4-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="226a4-206">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="226a4-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="226a4-207">Teradata로 데이터를 이동하는 경우 Teradata 형식에서 .NET 형식으로 이동에 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="226a4-208">Teradata 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="226a4-208">Teradata Database type</span></span> | <span data-ttu-id="226a4-209">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="226a4-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="226a4-210">Char</span><span class="sxs-lookup"><span data-stu-id="226a4-210">Char</span></span> |<span data-ttu-id="226a4-211">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-211">String</span></span> |
| <span data-ttu-id="226a4-212">Clob</span><span class="sxs-lookup"><span data-stu-id="226a4-212">Clob</span></span> |<span data-ttu-id="226a4-213">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-213">String</span></span> |
| <span data-ttu-id="226a4-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="226a4-214">Graphic</span></span> |<span data-ttu-id="226a4-215">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-215">String</span></span> |
| <span data-ttu-id="226a4-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="226a4-216">VarChar</span></span> |<span data-ttu-id="226a4-217">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-217">String</span></span> |
| <span data-ttu-id="226a4-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="226a4-218">VarGraphic</span></span> |<span data-ttu-id="226a4-219">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-219">String</span></span> |
| <span data-ttu-id="226a4-220">Blob</span><span class="sxs-lookup"><span data-stu-id="226a4-220">Blob</span></span> |<span data-ttu-id="226a4-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="226a4-221">Byte[]</span></span> |
| <span data-ttu-id="226a4-222">Byte</span><span class="sxs-lookup"><span data-stu-id="226a4-222">Byte</span></span> |<span data-ttu-id="226a4-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="226a4-223">Byte[]</span></span> |
| <span data-ttu-id="226a4-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="226a4-224">VarByte</span></span> |<span data-ttu-id="226a4-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="226a4-225">Byte[]</span></span> |
| <span data-ttu-id="226a4-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="226a4-226">BigInt</span></span> |<span data-ttu-id="226a4-227">Int64</span><span class="sxs-lookup"><span data-stu-id="226a4-227">Int64</span></span> |
| <span data-ttu-id="226a4-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="226a4-228">ByteInt</span></span> |<span data-ttu-id="226a4-229">Int16</span><span class="sxs-lookup"><span data-stu-id="226a4-229">Int16</span></span> |
| <span data-ttu-id="226a4-230">10진수</span><span class="sxs-lookup"><span data-stu-id="226a4-230">Decimal</span></span> |<span data-ttu-id="226a4-231">10진수</span><span class="sxs-lookup"><span data-stu-id="226a4-231">Decimal</span></span> |
| <span data-ttu-id="226a4-232">Double</span><span class="sxs-lookup"><span data-stu-id="226a4-232">Double</span></span> |<span data-ttu-id="226a4-233">Double</span><span class="sxs-lookup"><span data-stu-id="226a4-233">Double</span></span> |
| <span data-ttu-id="226a4-234">Integer</span><span class="sxs-lookup"><span data-stu-id="226a4-234">Integer</span></span> |<span data-ttu-id="226a4-235">Int32</span><span class="sxs-lookup"><span data-stu-id="226a4-235">Int32</span></span> |
| <span data-ttu-id="226a4-236">Number</span><span class="sxs-lookup"><span data-stu-id="226a4-236">Number</span></span> |<span data-ttu-id="226a4-237">Double</span><span class="sxs-lookup"><span data-stu-id="226a4-237">Double</span></span> |
| <span data-ttu-id="226a4-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="226a4-238">SmallInt</span></span> |<span data-ttu-id="226a4-239">Int16</span><span class="sxs-lookup"><span data-stu-id="226a4-239">Int16</span></span> |
| <span data-ttu-id="226a4-240">Date</span><span class="sxs-lookup"><span data-stu-id="226a4-240">Date</span></span> |<span data-ttu-id="226a4-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="226a4-241">DateTime</span></span> |
| <span data-ttu-id="226a4-242">Time</span><span class="sxs-lookup"><span data-stu-id="226a4-242">Time</span></span> |<span data-ttu-id="226a4-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-243">TimeSpan</span></span> |
| <span data-ttu-id="226a4-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="226a4-244">Time With Time Zone</span></span> |<span data-ttu-id="226a4-245">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-245">String</span></span> |
| <span data-ttu-id="226a4-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="226a4-246">Timestamp</span></span> |<span data-ttu-id="226a4-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="226a4-247">DateTime</span></span> |
| <span data-ttu-id="226a4-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="226a4-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="226a4-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="226a4-249">DateTimeOffset</span></span> |
| <span data-ttu-id="226a4-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="226a4-250">Interval Day</span></span> |<span data-ttu-id="226a4-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-251">TimeSpan</span></span> |
| <span data-ttu-id="226a4-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="226a4-252">Interval Day To Hour</span></span> |<span data-ttu-id="226a4-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-253">TimeSpan</span></span> |
| <span data-ttu-id="226a4-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="226a4-254">Interval Day To Minute</span></span> |<span data-ttu-id="226a4-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-255">TimeSpan</span></span> |
| <span data-ttu-id="226a4-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="226a4-256">Interval Day To Second</span></span> |<span data-ttu-id="226a4-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-257">TimeSpan</span></span> |
| <span data-ttu-id="226a4-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="226a4-258">Interval Hour</span></span> |<span data-ttu-id="226a4-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-259">TimeSpan</span></span> |
| <span data-ttu-id="226a4-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="226a4-260">Interval Hour To Minute</span></span> |<span data-ttu-id="226a4-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-261">TimeSpan</span></span> |
| <span data-ttu-id="226a4-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="226a4-262">Interval Hour To Second</span></span> |<span data-ttu-id="226a4-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-263">TimeSpan</span></span> |
| <span data-ttu-id="226a4-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="226a4-264">Interval Minute</span></span> |<span data-ttu-id="226a4-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-265">TimeSpan</span></span> |
| <span data-ttu-id="226a4-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="226a4-266">Interval Minute To Second</span></span> |<span data-ttu-id="226a4-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-267">TimeSpan</span></span> |
| <span data-ttu-id="226a4-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="226a4-268">Interval Second</span></span> |<span data-ttu-id="226a4-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="226a4-269">TimeSpan</span></span> |
| <span data-ttu-id="226a4-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="226a4-270">Interval Year</span></span> |<span data-ttu-id="226a4-271">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-271">String</span></span> |
| <span data-ttu-id="226a4-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="226a4-272">Interval Year To Month</span></span> |<span data-ttu-id="226a4-273">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-273">String</span></span> |
| <span data-ttu-id="226a4-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="226a4-274">Interval Month</span></span> |<span data-ttu-id="226a4-275">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-275">String</span></span> |
| <span data-ttu-id="226a4-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="226a4-276">Period(Date)</span></span> |<span data-ttu-id="226a4-277">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-277">String</span></span> |
| <span data-ttu-id="226a4-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="226a4-278">Period(Time)</span></span> |<span data-ttu-id="226a4-279">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-279">String</span></span> |
| <span data-ttu-id="226a4-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="226a4-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="226a4-281">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-281">String</span></span> |
| <span data-ttu-id="226a4-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="226a4-282">Period(Timestamp)</span></span> |<span data-ttu-id="226a4-283">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-283">String</span></span> |
| <span data-ttu-id="226a4-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="226a4-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="226a4-285">문자열</span><span class="sxs-lookup"><span data-stu-id="226a4-285">String</span></span> |
| <span data-ttu-id="226a4-286">Xml</span><span class="sxs-lookup"><span data-stu-id="226a4-286">Xml</span></span> |<span data-ttu-id="226a4-287">String</span><span class="sxs-lookup"><span data-stu-id="226a4-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="226a4-288">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="226a4-288">Map source to sink columns</span></span>
<span data-ttu-id="226a4-289">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="226a4-290">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="226a4-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="226a4-291">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="226a4-292">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="226a4-293">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="226a4-294">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226a4-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="226a4-295">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="226a4-296">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="226a4-296">Performance and Tuning</span></span>
<span data-ttu-id="226a4-297">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226a4-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
