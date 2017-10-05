---
title: "Azure Data Factory를 사용하여 DB2에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory 복사 활동을 사용하여 온-프레미스 DB2 데이터베이스에서 데이터를 이동하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="06276-103">Azure Data Factory 복사 활동을 사용하여 DB2에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="06276-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="06276-104">이 문서에서는 Azure Data Factory에서 복사 활동을 사용하여 온-프레미스 DB2 데이터베이스에서 데이터 저장소로 데이터를 복사하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="06276-105">[Data Factory 데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서에서 지원되는 싱크로 나열되는 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="06276-106">이 항목은 복사 활동을 사용한 데이터 이동에 대해 간략히 설명하고 지원되는 데이터 저장소 조합을 나열하는 Data Factory 문서를 기반으로 하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="06276-107">Data Factory는 현재 DB2 데이터베이스에서 [지원되는 싱크 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)로 데이터를 이동하는 작업만 지원하고,</span><span class="sxs-lookup"><span data-stu-id="06276-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="06276-108">다른 데이터 저장소에서 DB2 데이터베이스로 데이터를 이동하는 작업은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06276-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06276-109">Prerequisites</span></span>
<span data-ttu-id="06276-110">Data Factory는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 사용하여 온-프레미스 DB2 데이터베이스에 연결하는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="06276-111">데이터를 이동하기 위해 게이트웨이 데이터 파이프라인을 설정하는 단계별 지침은 [온-프레미스에서 클라우드로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="06276-112">DB2가 Azure IaaS VM에 호스팅되는 경우에도 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="06276-113">데이터 저장소와 동일한 IaaS VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="06276-114">게이트웨이에서 데이터베이스에 연결할 수 있으면 다른 VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="06276-115">데이터 관리 게이트웨이에서 기본 제공 DB2 드라이버를 제공하므로 DB2에서 데이터를 복사하기 위해 드라이버를 수동으로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="06276-116">연결 및 게이트웨이 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="06276-117">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="06276-117">Supported versions</span></span>
<span data-ttu-id="06276-118">Data Factory DB2 커넥터는 DRDA(Distributed Relational Database Architecture) SQL Access Manager 버전 9, 10 및 11과 함께 다음 IBM DB2 플랫폼 및 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="06276-119">z/OS용 IBM DB2 버전 11.1</span><span class="sxs-lookup"><span data-stu-id="06276-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="06276-120">z/OS용 IBM DB2 버전 10.1</span><span class="sxs-lookup"><span data-stu-id="06276-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="06276-121">i(AS400)용 IBM DB2 버전 7.2</span><span class="sxs-lookup"><span data-stu-id="06276-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="06276-122">i(AS400)용 IBM DB2 버전 7.1</span><span class="sxs-lookup"><span data-stu-id="06276-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="06276-123">LUW(Linux, UNIX, and Windows)용 IBM DB2 버전 11</span><span class="sxs-lookup"><span data-stu-id="06276-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="06276-124">LUW용 IBM DB2 버전 10.5</span><span class="sxs-lookup"><span data-stu-id="06276-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="06276-125">LUW용 IBM DB2 버전 10.1</span><span class="sxs-lookup"><span data-stu-id="06276-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="06276-126">"SQL 문 실행 요청에 해당하는 패키지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="06276-127">SQLSTATE=51002 SQLCODE=-805"라는 오류 메시지가 표시되면 OS에 일반 사용자에게 필요한 패키지가 만들어지지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="06276-128">이 문제를 해결하려면 DB2 서버 유형에 대한 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="06276-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="06276-129">i(AS400)용 DB2: 복사 활동을 실행하기 전에 고급 사용자가 일반 사용자에 대한 컬렉션을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="06276-130">컬렉션을 만들려면 `create collection <username>` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="06276-131">z/OS 또는 LUW용 DB2: 높은 권한 계정(패키지 권한 및 BIND, BINDADD, GRANT EXECUTE TO PUBLIC 권한이 있는 고급 사용자 또는 관리자)을 사용하여 복사를 한 번 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="06276-132">필요한 패키지는 복사 중에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="06276-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="06276-133">나중에 후속 복사 실행을 위해 일반 사용자로 다시 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="06276-134">시작</span><span class="sxs-lookup"><span data-stu-id="06276-134">Getting started</span></span>
<span data-ttu-id="06276-135">여러 도구/API를 사용하여 복사 활동이 포함된 파이프라인을 만들어 온-프레미스 DB2 데이터 저장소의 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="06276-136">파이프라인을 만드는 가장 쉬운 방법은 Azure Data Factory 복사 마법사를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="06276-137">복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="06276-138">또한 Azure Portal, Visual Studio, Azure PowerShell, Azure 리소스 관리자 템플릿, .NET API 및 REST API를 포함한 도구를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="06276-139">복사 활동이 포함된 파이프라인을 만드는 단계별 지침은 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="06276-140">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="06276-141">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06276-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="06276-142">복사 활동의 입력 및 출력 데이터를 나타내는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06276-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="06276-143">입력과 출력으로 각각의 데이터 집합을 사용하는 복사 활동이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06276-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="06276-144">복사 마법사를 사용하는 경우 Data Factory 연결된 서비스, 데이터 집합 및 파이프라인 엔터티에 대한 JSON 정의가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="06276-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="06276-145">도구 또는 API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="06276-146">[JSON 예제: DB2에서 Azure Blob 저장소로 데이터 복사](#json-example-copy-data-from-db2-to-azure-blob)에서는 온-프레미스 DB2 데이터 저장소에서 데이터를 복사하는 데 사용되는 Data Factory 엔터티에 대한 JSON 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06276-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="06276-147">다음 섹션에서는 DB2 데이터 저장소와 관련된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="06276-148">DB2 연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="06276-148">DB2 linked service properties</span></span>
<span data-ttu-id="06276-149">다음 표에는 DB2 연결된 서비스와 관련된 JSON 속성이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="06276-150">속성</span><span class="sxs-lookup"><span data-stu-id="06276-150">Property</span></span> | <span data-ttu-id="06276-151">설명</span><span class="sxs-lookup"><span data-stu-id="06276-151">Description</span></span> | <span data-ttu-id="06276-152">필수</span><span class="sxs-lookup"><span data-stu-id="06276-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06276-153">**type**</span><span class="sxs-lookup"><span data-stu-id="06276-153">**type**</span></span> |<span data-ttu-id="06276-154">**OnPremisesDB2**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="06276-155">예</span><span class="sxs-lookup"><span data-stu-id="06276-155">Yes</span></span> |
| <span data-ttu-id="06276-156">**server**</span><span class="sxs-lookup"><span data-stu-id="06276-156">**server**</span></span> |<span data-ttu-id="06276-157">DB2 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-157">The name of the DB2 server.</span></span> |<span data-ttu-id="06276-158">예</span><span class="sxs-lookup"><span data-stu-id="06276-158">Yes</span></span> |
| <span data-ttu-id="06276-159">**database**</span><span class="sxs-lookup"><span data-stu-id="06276-159">**database**</span></span> |<span data-ttu-id="06276-160">DB2 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-160">The name of the DB2 database.</span></span> |<span data-ttu-id="06276-161">예</span><span class="sxs-lookup"><span data-stu-id="06276-161">Yes</span></span> |
| <span data-ttu-id="06276-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="06276-162">**schema**</span></span> |<span data-ttu-id="06276-163">DB2 데이터베이스의 스키마 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="06276-164">대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-164">This property is case-sensitive.</span></span> |<span data-ttu-id="06276-165">아니요</span><span class="sxs-lookup"><span data-stu-id="06276-165">No</span></span> |
| <span data-ttu-id="06276-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="06276-166">**authenticationType**</span></span> |<span data-ttu-id="06276-167">DB2 데이터베이스에 연결하는 데 사용되는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="06276-168">가능한 값은 Anonymous, Basic 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="06276-169">예</span><span class="sxs-lookup"><span data-stu-id="06276-169">Yes</span></span> |
| <span data-ttu-id="06276-170">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="06276-170">**username**</span></span> |<span data-ttu-id="06276-171">Basic 또는 Windows 인증을 사용하는 경우 사용자 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="06276-172">아니요</span><span class="sxs-lookup"><span data-stu-id="06276-172">No</span></span> |
| <span data-ttu-id="06276-173">**암호**</span><span class="sxs-lookup"><span data-stu-id="06276-173">**password**</span></span> |<span data-ttu-id="06276-174">사용자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-174">The password for the user account.</span></span> |<span data-ttu-id="06276-175">아니요</span><span class="sxs-lookup"><span data-stu-id="06276-175">No</span></span> |
| <span data-ttu-id="06276-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="06276-176">**gatewayName**</span></span> |<span data-ttu-id="06276-177">Data Factory 서비스에서 온-프레미스 DB2 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="06276-178">예</span><span class="sxs-lookup"><span data-stu-id="06276-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="06276-179">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="06276-179">Dataset properties</span></span>
<span data-ttu-id="06276-180">데이터 집합을 정의하는 데 사용할 수 있는 섹션 및 속성 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="06276-181">JSON 데이터 집합에 대한 **structure**, **availability** 및 **policy**과 같은 섹션은 모든 데이터 집합 유형(Azure SQL, Azure Blob 저장소, Azure Table 저장소 등)에서 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="06276-182">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="06276-183">DB2 데이터 집합을 포함하는 **RelationalTable** 형식의 데이터 집합에 대한 **typeProperties** 섹션에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="06276-184">속성</span><span class="sxs-lookup"><span data-stu-id="06276-184">Property</span></span> | <span data-ttu-id="06276-185">설명</span><span class="sxs-lookup"><span data-stu-id="06276-185">Description</span></span> | <span data-ttu-id="06276-186">필수</span><span class="sxs-lookup"><span data-stu-id="06276-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06276-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="06276-187">**tableName**</span></span> |<span data-ttu-id="06276-188">연결된 서비스에서 참조하는 DB2 데이터베이스 인스턴스의 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="06276-189">대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-189">This property is case-sensitive.</span></span> |<span data-ttu-id="06276-190">아니요(**RelationalSource** 형식 복사 활동의 **query** 속성이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="06276-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="06276-191">복사 활동 속성</span><span class="sxs-lookup"><span data-stu-id="06276-191">Copy Activity properties</span></span>
<span data-ttu-id="06276-192">복사 활동을 정의하는 데 사용할 수 있는 섹션 및 속성 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="06276-193">**name**, **description**, **inputs** 테이블, **outputs** 테이블 및 **policy**와 같은 복사 활동 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="06276-194">각 활동 유형에 대한 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="06276-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="06276-195">복사 활동의 경우 속성은 데이터 원본 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="06276-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="06276-196">복사 활동의 경우 원본이 **RelationalSource** 형식인 경우(DB2 포함) **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="06276-197">속성</span><span class="sxs-lookup"><span data-stu-id="06276-197">Property</span></span> | <span data-ttu-id="06276-198">설명</span><span class="sxs-lookup"><span data-stu-id="06276-198">Description</span></span> | <span data-ttu-id="06276-199">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="06276-199">Allowed values</span></span> | <span data-ttu-id="06276-200">필수</span><span class="sxs-lookup"><span data-stu-id="06276-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06276-201">**query**</span><span class="sxs-lookup"><span data-stu-id="06276-201">**query**</span></span> |<span data-ttu-id="06276-202">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="06276-203">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="06276-203">SQL query string.</span></span> <span data-ttu-id="06276-204">예: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="06276-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="06276-205">아니요(데이터 집합의 **tableName** 속성이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="06276-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="06276-206">스키마 및 테이블 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="06276-207">쿼리 문에서 ""(큰 따옴표)를 사용하여 속성 이름을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="06276-208">예:</span><span class="sxs-lookup"><span data-stu-id="06276-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="06276-209">JSON 예제: DB2에서 Azure Blob 저장소로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="06276-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="06276-210">이 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="06276-211">DB2 데이터베이스에서 Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06276-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="06276-212">그러나 Azure Data Factory 복사 활동을 사용하여 [지원되는 데이터 저장소 싱크 형식](data-factory-data-movement-activities.md#supported-data-stores-and-formats)에 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="06276-213">샘플에 포함된 Data Factory 엔터티는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="06276-214">[OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties) 형식의 DB2 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="06276-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="06276-215">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 Azure Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="06276-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="06276-216">[RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="06276-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="06276-217">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="06276-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="06276-218">[RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 속성을 사용하는 복사 활동이 있는 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="06276-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="06276-219">샘플은 DB2 데이터베이스의 쿼리 결과에서 Azure Blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="06276-220">샘플에 사용된 JSON 속성은 엔터티 정의 뒤에 나오는 섹션에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="06276-221">첫 번째 단계로 데이터 관리 게이트웨이를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="06276-222">지침은 [온-프레미스 위치와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="06276-223">**DB2 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="06276-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="06276-224">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="06276-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="06276-225">**DB2 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="06276-225">**DB2 input dataset**</span></span>

<span data-ttu-id="06276-226">샘플에서는 시계열 데이터에 대한 "timestamp"라는 열이 있는 "MyTable"이라는 DB2 테이블을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="06276-227">**external** 속성이 "true"로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-227">The **external** property is set to "true."</span></span> <span data-ttu-id="06276-228">이 설정을 사용하는 경우 이 데이터 집합은 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory 서비스에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="06276-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="06276-229">**type** 속성은 **RelationalTable**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="06276-230">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="06276-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="06276-231">**frequency** 속성을 "Hour"로 설정하고 **interval** 속성을 1로 설정하여 매시간 새 Blob에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="06276-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="06276-232">Blob에 대한 **folderPath** 속성은 처리 중인 조각의 시작 시간에 따라 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="06276-233">폴더 경로는 시작 시간의 년, 월, 일 및 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="06276-234">**복사 활동에 대한 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="06276-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="06276-235">파이프라인에는 지정된 입력 및 출력 데이터 집합을 사용하도록 구성되고 매 시간마다 실행하도록 예약된 복사 활동이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="06276-236">파이프라인에 대한 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="06276-237">**query** 속성에 지정된 SQL 쿼리는 "Orders" 테이블에서 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="06276-238">DB2에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="06276-238">Type mapping for DB2</span></span>
<span data-ttu-id="06276-239">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 대로 복사 활동에서는 다음 2단계 접근 방법을 사용하여 source 형식에서 sink 형식으로의 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="06276-240">네이티브 소스 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="06276-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="06276-241">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="06276-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="06276-242">복사 활동에서 DB2 형식에서 .NET 형식으로 데이터를 변환할 때 다음 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06276-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="06276-243">DB2 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="06276-243">DB2 database type</span></span> | <span data-ttu-id="06276-244">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="06276-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="06276-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="06276-245">SmallInt</span></span> |<span data-ttu-id="06276-246">Int16</span><span class="sxs-lookup"><span data-stu-id="06276-246">Int16</span></span> |
| <span data-ttu-id="06276-247">Integer</span><span class="sxs-lookup"><span data-stu-id="06276-247">Integer</span></span> |<span data-ttu-id="06276-248">Int32</span><span class="sxs-lookup"><span data-stu-id="06276-248">Int32</span></span> |
| <span data-ttu-id="06276-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="06276-249">BigInt</span></span> |<span data-ttu-id="06276-250">Int64</span><span class="sxs-lookup"><span data-stu-id="06276-250">Int64</span></span> |
| <span data-ttu-id="06276-251">Real</span><span class="sxs-lookup"><span data-stu-id="06276-251">Real</span></span> |<span data-ttu-id="06276-252">단일</span><span class="sxs-lookup"><span data-stu-id="06276-252">Single</span></span> |
| <span data-ttu-id="06276-253">Double</span><span class="sxs-lookup"><span data-stu-id="06276-253">Double</span></span> |<span data-ttu-id="06276-254">Double</span><span class="sxs-lookup"><span data-stu-id="06276-254">Double</span></span> |
| <span data-ttu-id="06276-255">Float</span><span class="sxs-lookup"><span data-stu-id="06276-255">Float</span></span> |<span data-ttu-id="06276-256">Double</span><span class="sxs-lookup"><span data-stu-id="06276-256">Double</span></span> |
| <span data-ttu-id="06276-257">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-257">Decimal</span></span> |<span data-ttu-id="06276-258">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-258">Decimal</span></span> |
| <span data-ttu-id="06276-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="06276-259">DecimalFloat</span></span> |<span data-ttu-id="06276-260">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-260">Decimal</span></span> |
| <span data-ttu-id="06276-261">숫자</span><span class="sxs-lookup"><span data-stu-id="06276-261">Numeric</span></span> |<span data-ttu-id="06276-262">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-262">Decimal</span></span> |
| <span data-ttu-id="06276-263">Date</span><span class="sxs-lookup"><span data-stu-id="06276-263">Date</span></span> |<span data-ttu-id="06276-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="06276-264">DateTime</span></span> |
| <span data-ttu-id="06276-265">Time</span><span class="sxs-lookup"><span data-stu-id="06276-265">Time</span></span> |<span data-ttu-id="06276-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="06276-266">TimeSpan</span></span> |
| <span data-ttu-id="06276-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="06276-267">Timestamp</span></span> |<span data-ttu-id="06276-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="06276-268">DateTime</span></span> |
| <span data-ttu-id="06276-269">xml</span><span class="sxs-lookup"><span data-stu-id="06276-269">Xml</span></span> |<span data-ttu-id="06276-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-270">Byte[]</span></span> |
| <span data-ttu-id="06276-271">Char</span><span class="sxs-lookup"><span data-stu-id="06276-271">Char</span></span> |<span data-ttu-id="06276-272">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-272">String</span></span> |
| <span data-ttu-id="06276-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="06276-273">VarChar</span></span> |<span data-ttu-id="06276-274">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-274">String</span></span> |
| <span data-ttu-id="06276-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="06276-275">LongVarChar</span></span> |<span data-ttu-id="06276-276">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-276">String</span></span> |
| <span data-ttu-id="06276-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="06276-277">DB2DynArray</span></span> |<span data-ttu-id="06276-278">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-278">String</span></span> |
| <span data-ttu-id="06276-279">이진</span><span class="sxs-lookup"><span data-stu-id="06276-279">Binary</span></span> |<span data-ttu-id="06276-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-280">Byte[]</span></span> |
| <span data-ttu-id="06276-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="06276-281">VarBinary</span></span> |<span data-ttu-id="06276-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-282">Byte[]</span></span> |
| <span data-ttu-id="06276-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="06276-283">LongVarBinary</span></span> |<span data-ttu-id="06276-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-284">Byte[]</span></span> |
| <span data-ttu-id="06276-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="06276-285">Graphic</span></span> |<span data-ttu-id="06276-286">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-286">String</span></span> |
| <span data-ttu-id="06276-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="06276-287">VarGraphic</span></span> |<span data-ttu-id="06276-288">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-288">String</span></span> |
| <span data-ttu-id="06276-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="06276-289">LongVarGraphic</span></span> |<span data-ttu-id="06276-290">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-290">String</span></span> |
| <span data-ttu-id="06276-291">Clob</span><span class="sxs-lookup"><span data-stu-id="06276-291">Clob</span></span> |<span data-ttu-id="06276-292">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-292">String</span></span> |
| <span data-ttu-id="06276-293">Blob</span><span class="sxs-lookup"><span data-stu-id="06276-293">Blob</span></span> |<span data-ttu-id="06276-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-294">Byte[]</span></span> |
| <span data-ttu-id="06276-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="06276-295">DbClob</span></span> |<span data-ttu-id="06276-296">문자열</span><span class="sxs-lookup"><span data-stu-id="06276-296">String</span></span> |
| <span data-ttu-id="06276-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="06276-297">SmallInt</span></span> |<span data-ttu-id="06276-298">Int16</span><span class="sxs-lookup"><span data-stu-id="06276-298">Int16</span></span> |
| <span data-ttu-id="06276-299">Integer</span><span class="sxs-lookup"><span data-stu-id="06276-299">Integer</span></span> |<span data-ttu-id="06276-300">Int32</span><span class="sxs-lookup"><span data-stu-id="06276-300">Int32</span></span> |
| <span data-ttu-id="06276-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="06276-301">BigInt</span></span> |<span data-ttu-id="06276-302">Int64</span><span class="sxs-lookup"><span data-stu-id="06276-302">Int64</span></span> |
| <span data-ttu-id="06276-303">Real</span><span class="sxs-lookup"><span data-stu-id="06276-303">Real</span></span> |<span data-ttu-id="06276-304">단일</span><span class="sxs-lookup"><span data-stu-id="06276-304">Single</span></span> |
| <span data-ttu-id="06276-305">Double</span><span class="sxs-lookup"><span data-stu-id="06276-305">Double</span></span> |<span data-ttu-id="06276-306">Double</span><span class="sxs-lookup"><span data-stu-id="06276-306">Double</span></span> |
| <span data-ttu-id="06276-307">Float</span><span class="sxs-lookup"><span data-stu-id="06276-307">Float</span></span> |<span data-ttu-id="06276-308">Double</span><span class="sxs-lookup"><span data-stu-id="06276-308">Double</span></span> |
| <span data-ttu-id="06276-309">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-309">Decimal</span></span> |<span data-ttu-id="06276-310">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-310">Decimal</span></span> |
| <span data-ttu-id="06276-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="06276-311">DecimalFloat</span></span> |<span data-ttu-id="06276-312">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-312">Decimal</span></span> |
| <span data-ttu-id="06276-313">숫자</span><span class="sxs-lookup"><span data-stu-id="06276-313">Numeric</span></span> |<span data-ttu-id="06276-314">10진수</span><span class="sxs-lookup"><span data-stu-id="06276-314">Decimal</span></span> |
| <span data-ttu-id="06276-315">Date</span><span class="sxs-lookup"><span data-stu-id="06276-315">Date</span></span> |<span data-ttu-id="06276-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="06276-316">DateTime</span></span> |
| <span data-ttu-id="06276-317">Time</span><span class="sxs-lookup"><span data-stu-id="06276-317">Time</span></span> |<span data-ttu-id="06276-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="06276-318">TimeSpan</span></span> |
| <span data-ttu-id="06276-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="06276-319">Timestamp</span></span> |<span data-ttu-id="06276-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="06276-320">DateTime</span></span> |
| <span data-ttu-id="06276-321">xml</span><span class="sxs-lookup"><span data-stu-id="06276-321">Xml</span></span> |<span data-ttu-id="06276-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06276-322">Byte[]</span></span> |
| <span data-ttu-id="06276-323">Char</span><span class="sxs-lookup"><span data-stu-id="06276-323">Char</span></span> |<span data-ttu-id="06276-324">String</span><span class="sxs-lookup"><span data-stu-id="06276-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="06276-325">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="06276-325">Map source to sink columns</span></span>
<span data-ttu-id="06276-326">원본 데이터 집합의 열을 싱크 데이터 집합의 열에 매핑하는 방법을 알아보려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="06276-327">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="06276-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="06276-328">관계형 데이터 저장소에서 데이터를 복사할 때 의도하지 않은 결과를 방지하기 위해 반복성을 명심해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="06276-329">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="06276-330">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 다시 시도 **policy** 속성을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06276-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="06276-331">조각의 재실행 횟수 및 재실행 방법과 관계 없이 동일한 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06276-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="06276-332">자세한 내용은 [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06276-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="06276-333">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="06276-333">Performance and tuning</span></span>
<span data-ttu-id="06276-334">[복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)에서 복사 활동의 성능에 영향을 주는 주요 요소와 성능을 최적화하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="06276-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>