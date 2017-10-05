---
title: "ODBC 데이터 저장소에서 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 ODBC 데이터 저장소에서 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="2c7de-103">Azure 데이터 팩터리를 사용하여 ODBC 데이터 저장소에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="2c7de-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="2c7de-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 ODBC 데이터 저장소에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="2c7de-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="2c7de-106">ODBC 데이터 저장소에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="2c7de-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2c7de-108">현재 데이터 팩터리는 다른 데이터 저장소에서 ODBC 데이터 저장소로 데이터 이동이 아닌 ODBC 데이터 저장소에서 다른 데이터 저장소로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="2c7de-109">연결 사용</span><span class="sxs-lookup"><span data-stu-id="2c7de-109">Enabling connectivity</span></span>
<span data-ttu-id="2c7de-110">데이터 팩터리 서비스는 데이터 관리 게이트웨이를 사용하여 온-프레미스 ODBC 원본에 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="2c7de-111">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="2c7de-112">Azure IaaS VM에서 호스팅되는 경우 ODBC 데이터 저장소에 연결하려면 게이트웨이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="2c7de-113">게이트웨이를 동일한 온-프레미스 컴퓨터 또는 ODBC 데이터 저장소로 Azure VM에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="2c7de-114">그러나 리소스 경합을 방지하고 성능 향상을 꾀하려면 게이트웨이를 별도 컴퓨터/Azure IaaS VM에 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="2c7de-115">별도 컴퓨터에 게이트웨이를 설치하는 경우 컴퓨터는 ODBC 데이터 저장소를 사용하여 컴퓨터에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="2c7de-116">데이터 관리 게이트웨이 외에도 게이트웨이 컴퓨터에서 데이터 저장소에 대한 ODBC 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="2c7de-117">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2c7de-118">시작</span><span class="sxs-lookup"><span data-stu-id="2c7de-118">Getting started</span></span>
<span data-ttu-id="2c7de-119">다른 도구/API를 사용하여 ODBC 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="2c7de-120">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2c7de-121">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="2c7de-122">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2c7de-123">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2c7de-124">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="2c7de-125">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2c7de-126">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2c7de-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2c7de-128">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2c7de-129">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2c7de-130">ODBC 데이터 저장소의 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: ODBC 데이터 저장소에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-odbc-data-store-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2c7de-131">다음 섹션에서는 ODBC 데이터 저장소에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2c7de-132">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-132">Linked service properties</span></span>
<span data-ttu-id="2c7de-133">다음 테이블은 ODBC 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="2c7de-134">속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-134">Property</span></span> | <span data-ttu-id="2c7de-135">설명</span><span class="sxs-lookup"><span data-stu-id="2c7de-135">Description</span></span> | <span data-ttu-id="2c7de-136">필수</span><span class="sxs-lookup"><span data-stu-id="2c7de-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c7de-137">type</span><span class="sxs-lookup"><span data-stu-id="2c7de-137">type</span></span> |<span data-ttu-id="2c7de-138">형식 속성은 다음으로 설정해야 함: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="2c7de-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="2c7de-139">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-139">Yes</span></span> |
| <span data-ttu-id="2c7de-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="2c7de-140">connectionString</span></span> |<span data-ttu-id="2c7de-141">선택적 암호화된 자격 증명 및 연결 문자열의 비 액세스 자격 증명 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="2c7de-142">다음 섹션의 예제를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c7de-142">See examples in the following sections.</span></span> |<span data-ttu-id="2c7de-143">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-143">Yes</span></span> |
| <span data-ttu-id="2c7de-144">자격 증명</span><span class="sxs-lookup"><span data-stu-id="2c7de-144">credential</span></span> |<span data-ttu-id="2c7de-145">드라이버 관련 속성 값 형식에 지정된 연결 문자열의 액세스 자격 증명 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="2c7de-146">예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="2c7de-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="2c7de-147">아니요</span><span class="sxs-lookup"><span data-stu-id="2c7de-147">No</span></span> |
| <span data-ttu-id="2c7de-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2c7de-148">authenticationType</span></span> |<span data-ttu-id="2c7de-149">ODBC 데이터 저장소에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="2c7de-150">가능한 값은 익명 및 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="2c7de-151">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-151">Yes</span></span> |
| <span data-ttu-id="2c7de-152">username</span><span class="sxs-lookup"><span data-stu-id="2c7de-152">username</span></span> |<span data-ttu-id="2c7de-153">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="2c7de-154">아니요</span><span class="sxs-lookup"><span data-stu-id="2c7de-154">No</span></span> |
| <span data-ttu-id="2c7de-155">password</span><span class="sxs-lookup"><span data-stu-id="2c7de-155">password</span></span> |<span data-ttu-id="2c7de-156">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="2c7de-157">아니요</span><span class="sxs-lookup"><span data-stu-id="2c7de-157">No</span></span> |
| <span data-ttu-id="2c7de-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2c7de-158">gatewayName</span></span> |<span data-ttu-id="2c7de-159">데이터 팩터리 서비스가 ODBC 데이터 저장소에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="2c7de-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="2c7de-160">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="2c7de-161">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2c7de-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="2c7de-162">암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2c7de-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="2c7de-163">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx)(Azure PowerShell의 1.0 버전 ) cmdlet 또는 [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx)(Azure PowerShell의 0.9 이전 버전)를 사용하여 자격 증명을 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="2c7de-164">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2c7de-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="2c7de-165">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-165">Dataset properties</span></span>
<span data-ttu-id="2c7de-166">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2c7de-167">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="2c7de-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2c7de-168">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2c7de-169">**RelationalTable** 형식(ODBC 데이터 집합을 포함)의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="2c7de-170">속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-170">Property</span></span> | <span data-ttu-id="2c7de-171">설명</span><span class="sxs-lookup"><span data-stu-id="2c7de-171">Description</span></span> | <span data-ttu-id="2c7de-172">필수</span><span class="sxs-lookup"><span data-stu-id="2c7de-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c7de-173">tableName</span><span class="sxs-lookup"><span data-stu-id="2c7de-173">tableName</span></span> |<span data-ttu-id="2c7de-174">ODBC 데이터 저장소에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="2c7de-175">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2c7de-176">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-176">Copy activity properties</span></span>
<span data-ttu-id="2c7de-177">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2c7de-178">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="2c7de-179">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="2c7de-180">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2c7de-181">원본이 **RelationalSource** 형식인 복사 작업(ODBC 포함)에서 typeProperties 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2c7de-182">속성</span><span class="sxs-lookup"><span data-stu-id="2c7de-182">Property</span></span> | <span data-ttu-id="2c7de-183">설명</span><span class="sxs-lookup"><span data-stu-id="2c7de-183">Description</span></span> | <span data-ttu-id="2c7de-184">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="2c7de-184">Allowed values</span></span> | <span data-ttu-id="2c7de-185">필수</span><span class="sxs-lookup"><span data-stu-id="2c7de-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2c7de-186">쿼리</span><span class="sxs-lookup"><span data-stu-id="2c7de-186">query</span></span> |<span data-ttu-id="2c7de-187">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-187">Use the custom query to read data.</span></span> |<span data-ttu-id="2c7de-188">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="2c7de-188">SQL query string.</span></span> <span data-ttu-id="2c7de-189">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="2c7de-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="2c7de-190">예</span><span class="sxs-lookup"><span data-stu-id="2c7de-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="2c7de-191">JSON 예: ODBC 데이터 저장소에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2c7de-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="2c7de-192">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2c7de-193">이 샘플은 ODBC 원본에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="2c7de-194">그러나 Azure Data Factory의 복사 작업을 사용하여 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 에 설명한 싱크로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="2c7de-195">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="2c7de-196">[OnPremisesOdbc](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="2c7de-197">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="2c7de-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2c7de-198">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="2c7de-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2c7de-199">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="2c7de-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2c7de-200">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="2c7de-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2c7de-201">샘플은 ODBC 데이터 저장소의 쿼리 결과에서 Blob에 매시간 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="2c7de-202">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2c7de-203">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="2c7de-204">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2c7de-205">**ODBC 연결된 서비스** 이 예제에서는 기본 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="2c7de-206">사용할 수 있는 다른 유형의 인증은 [ODBC 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="2c7de-207">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="2c7de-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="2c7de-208">**ODBC 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="2c7de-208">**ODBC input dataset**</span></span>

<span data-ttu-id="2c7de-209">샘플은 ODBC 데이터베이스에서 만든 테이블 "MyTable"에 시계열 데이터에 대한 "timestampcolumn"이라는 열이 포함되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="2c7de-210">"external": "true"로 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="2c7de-211">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="2c7de-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="2c7de-212">데이터는 매시간 새 blob에 기록됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="2c7de-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2c7de-213">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2c7de-214">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="2c7de-215">**ODBC 원본(RelationalSource) 및 Blob 싱크 (BlobSink)를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="2c7de-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="2c7de-216">파이프라인은 이러한 입력 및 출력 데이터 집합을 사용하도록 구성되며 매시간 실행되도록 예약되는 복사 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2c7de-217">파이프라인 JSON 정의에서 **source** 형식은 **RelationalSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2c7de-218">**query** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="2c7de-219">ODBC에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="2c7de-219">Type mapping for ODBC</span></span>
<span data-ttu-id="2c7de-220">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼 복사 작업은 다음 2단계 접근 방법 사용하여 원본 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="2c7de-221">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="2c7de-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="2c7de-222">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="2c7de-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="2c7de-223">ODBC 데이터 저장소에서 데이터를 이동할 때 [ODBC 데이터 형식 매핑](https://msdn.microsoft.com/library/cc668763.aspx) 토픽에서 설명된 대로 ODBC 데이터 형식은 .NET 형식에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="2c7de-224">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="2c7de-224">Map source to sink columns</span></span>
<span data-ttu-id="2c7de-225">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하는 방법은 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2c7de-226">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="2c7de-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="2c7de-227">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2c7de-228">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2c7de-229">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2c7de-230">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2c7de-231">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="2c7de-232">GE Historian 저장소</span><span class="sxs-lookup"><span data-stu-id="2c7de-232">GE Historian store</span></span>
<span data-ttu-id="2c7de-233">다음 예제와 같이 [GE Proficy Historian(현재 GE Historian)](http://www.geautomation.com/products/proficy-historian) 데이터 저장소를 Azure Data Factory에 연결하는 ODBC 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="2c7de-234">온-프레미스 컴퓨터에서 데이터 관리 게이트웨이를 설치하고 포털에 게이트웨이를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="2c7de-235">온-프레미스 컴퓨터에 설치된 게이트웨이는 GE Historian용 ODBC 드라이버를 사용하여 GE Historian 데이터 저장소에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="2c7de-236">따라서 게이트웨이 컴퓨터에 아직 설치되지 않은 경우 해당 드라이버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="2c7de-237">자세한 내용은 [연결 사용](#enabling-connectivity) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="2c7de-238">Data Factory 솔루션에서 GE Historian 저장소를 사용하기 전에 게이트웨이에서 다음 섹션의 지침을 사용하여 데이터 저장소에 연결할 수 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="2c7de-239">복사 작업에서 ODBC 데이터 저장소를 원본 데이터 저장소로 사용하는 데 대한 자세한 개요를 보려면 문서를 처음부터 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="2c7de-240">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2c7de-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="2c7de-241">연결 문제를 해결하려면 **데이터 관리 게이트웨이 구성 관리자**의 **진단** 탭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="2c7de-242">**데이터 관리 게이트웨이 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="2c7de-243">"C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe"를 직접 실행하거나 다음 이미지에서처럼 **게이트웨이**를 검색하여 **Microsoft 데이터 관리 게이트웨이** 응용 프로그램에 대한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![게이트웨이 검색](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="2c7de-245">**진단** 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-245">Switch to the **Diagnostics** tab.</span></span>

    ![게이트웨이 진단](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="2c7de-247">데이터 저장소(연결된 서비스)의 **형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="2c7de-248">**인증**을 지정하고 데이터 저장소에 연결된 **자격 증명**을 입력하거나 **연결 문자열**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="2c7de-249">**연결 테스트**를 클릭하여 데이터 저장소에 대한 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7de-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2c7de-250">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="2c7de-250">Performance and Tuning</span></span>
<span data-ttu-id="2c7de-251">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c7de-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
