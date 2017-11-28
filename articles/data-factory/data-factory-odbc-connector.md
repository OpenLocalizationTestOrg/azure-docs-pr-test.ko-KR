---
title: "ODBC 데이터 저장소에서 데이터 aaaMove | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 toomove 데이터를 ODBC 데이터에서에서을 저장 하는 방법을 알아봅니다."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="748e1-103">Azure 데이터 팩터리를 사용하여 ODBC 데이터 저장소에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="748e1-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="748e1-104">이 문서에서는 toouse hello 복사 작업에서는 온-프레미스 ODBC 데이터 Azure Data Factory toomove 데이터에 저장 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="748e1-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="748e1-106">ODBC 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="748e1-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="748e1-108">데이터 팩터리는 현재 tooother 데이터 저장소를 저장 하는 데이터를 ODBC 데이터에서에서 이동 뿐만 아니라 다른 데이터 저장소 tooan ODBC 데이터 저장소에서 데이터 이동에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="748e1-109">연결 사용</span><span class="sxs-lookup"><span data-stu-id="748e1-109">Enabling connectivity</span></span>
<span data-ttu-id="748e1-110">데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 ODBC 원본을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="748e1-111">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="748e1-112">Azure IaaS VM에서 호스팅되는 경우에 hello 게이트웨이 tooconnect tooan ODBC 데이터 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="748e1-113">Hello 동일한 온-프레미스 컴퓨터 또는 hello hello ODBC 데이터 저장소로 Azure VM에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="748e1-114">하지만 별도 컴퓨터/Azure IaaS VM에 hello 게이트웨이 설치 하는 권장 tooavoid 리소스 경합 및 성능 향상을 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="748e1-115">별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 hello ODBC 데이터 저장소를 사용 하 여 수 tooaccess hello 컴퓨터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="748e1-116">데이터 관리 게이트웨이 hello와는 별도로 hello 데이터 저장소 hello 게이트웨이 컴퓨터에 대 한 tooinstall hello ODBC 드라이버를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="748e1-117">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="748e1-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="748e1-118">시작</span><span class="sxs-lookup"><span data-stu-id="748e1-118">Getting started</span></span>
<span data-ttu-id="748e1-119">다른 도구/API를 사용하여 ODBC 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="748e1-120">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="748e1-121">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="748e1-122">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="748e1-123">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="748e1-124">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="748e1-125">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="748e1-126">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="748e1-127">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="748e1-128">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="748e1-129">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="748e1-130">Data Factory 된 엔터티를 ODBC 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: tooAzure Blob을 저장 하는 ODBC 데이터에서 데이터 복사](#json-example-copy-data-from-odbc-data-store-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="748e1-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="748e1-131">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooODBC 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="748e1-132">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="748e1-132">Linked service properties</span></span>
<span data-ttu-id="748e1-133">다음 표에서 hello JSON 요소 특정 tooODBC 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="748e1-134">속성</span><span class="sxs-lookup"><span data-stu-id="748e1-134">Property</span></span> | <span data-ttu-id="748e1-135">설명</span><span class="sxs-lookup"><span data-stu-id="748e1-135">Description</span></span> | <span data-ttu-id="748e1-136">필수</span><span class="sxs-lookup"><span data-stu-id="748e1-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="748e1-137">type</span><span class="sxs-lookup"><span data-stu-id="748e1-137">type</span></span> |<span data-ttu-id="748e1-138">hello type 속성 설정 해야 합니다: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="748e1-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="748e1-139">예</span><span class="sxs-lookup"><span data-stu-id="748e1-139">Yes</span></span> |
| <span data-ttu-id="748e1-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="748e1-140">connectionString</span></span> |<span data-ttu-id="748e1-141">hello 연결 문자열 및 선택적의 hello이 아닌 액세스 자격 증명 일부분 자격 증명을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="748e1-142">Hello 다음 섹션의에서 예를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-142">See examples in hello following sections.</span></span> |<span data-ttu-id="748e1-143">예</span><span class="sxs-lookup"><span data-stu-id="748e1-143">Yes</span></span> |
| <span data-ttu-id="748e1-144">자격 증명</span><span class="sxs-lookup"><span data-stu-id="748e1-144">credential</span></span> |<span data-ttu-id="748e1-145">hello 액세스 자격 증명 드라이버 관련 속성 값 형식으로 지정 하는 hello 연결 문자열의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="748e1-146">예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="748e1-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="748e1-147">아니요</span><span class="sxs-lookup"><span data-stu-id="748e1-147">No</span></span> |
| <span data-ttu-id="748e1-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="748e1-148">authenticationType</span></span> |<span data-ttu-id="748e1-149">Tooconnect toohello ODBC 데이터 저장소를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="748e1-150">가능한 값은 익명 및 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="748e1-151">예</span><span class="sxs-lookup"><span data-stu-id="748e1-151">Yes</span></span> |
| <span data-ttu-id="748e1-152">username</span><span class="sxs-lookup"><span data-stu-id="748e1-152">username</span></span> |<span data-ttu-id="748e1-153">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="748e1-154">아니요</span><span class="sxs-lookup"><span data-stu-id="748e1-154">No</span></span> |
| <span data-ttu-id="748e1-155">암호</span><span class="sxs-lookup"><span data-stu-id="748e1-155">password</span></span> |<span data-ttu-id="748e1-156">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="748e1-157">아니요</span><span class="sxs-lookup"><span data-stu-id="748e1-157">No</span></span> |
| <span data-ttu-id="748e1-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="748e1-158">gatewayName</span></span> |<span data-ttu-id="748e1-159">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello ODBC 데이터 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="748e1-160">예</span><span class="sxs-lookup"><span data-stu-id="748e1-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="748e1-161">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="748e1-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="748e1-162">암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="748e1-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="748e1-163">Hello를 사용 하 여 hello 자격 증명을 암호화할 수 [새로 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 버전의 Azure PowerShell) cmdlet 또는 [New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 또는 이전 버전의 hello Azure PowerShell)입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="748e1-164">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="748e1-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="748e1-165">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="748e1-165">Dataset properties</span></span>
<span data-ttu-id="748e1-166">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="748e1-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="748e1-167">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="748e1-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="748e1-168">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="748e1-169">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **RelationalTable** hello 다음과 같은 속성에 (ODBC 데이터 집합 포함)</span><span class="sxs-lookup"><span data-stu-id="748e1-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="748e1-170">속성</span><span class="sxs-lookup"><span data-stu-id="748e1-170">Property</span></span> | <span data-ttu-id="748e1-171">설명</span><span class="sxs-lookup"><span data-stu-id="748e1-171">Description</span></span> | <span data-ttu-id="748e1-172">필수</span><span class="sxs-lookup"><span data-stu-id="748e1-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="748e1-173">tableName</span><span class="sxs-lookup"><span data-stu-id="748e1-173">tableName</span></span> |<span data-ttu-id="748e1-174">Hello ODBC 데이터 저장소의 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="748e1-175">예</span><span class="sxs-lookup"><span data-stu-id="748e1-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="748e1-176">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="748e1-176">Copy activity properties</span></span>
<span data-ttu-id="748e1-177">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="748e1-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="748e1-178">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="748e1-179">Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="748e1-180">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="748e1-181">복사 작업에서는 원본 유형인 경우 **RelationalSource** (ODBC 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="748e1-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="748e1-182">속성</span><span class="sxs-lookup"><span data-stu-id="748e1-182">Property</span></span> | <span data-ttu-id="748e1-183">설명</span><span class="sxs-lookup"><span data-stu-id="748e1-183">Description</span></span> | <span data-ttu-id="748e1-184">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="748e1-184">Allowed values</span></span> | <span data-ttu-id="748e1-185">필수</span><span class="sxs-lookup"><span data-stu-id="748e1-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="748e1-186">쿼리</span><span class="sxs-lookup"><span data-stu-id="748e1-186">query</span></span> |<span data-ttu-id="748e1-187">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="748e1-188">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="748e1-188">SQL query string.</span></span> <span data-ttu-id="748e1-189">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="748e1-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="748e1-190">예</span><span class="sxs-lookup"><span data-stu-id="748e1-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="748e1-191">JSON의 예: tooAzure Blob을 저장 하는 ODBC 데이터에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="748e1-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="748e1-192">이 예에서는 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="748e1-193">ODBC에서 toocopy 데이터 tooan Azure Blob 저장소를 원본 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="748e1-194">그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="748e1-195">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="748e1-196">[OnPremisesOdbc](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="748e1-197">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="748e1-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="748e1-198">[RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="748e1-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="748e1-199">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="748e1-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="748e1-200">[RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="748e1-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="748e1-201">hello 샘플 데이터 복사는 ODBC 데이터 저장소 tooa blob에 쿼리 결과에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="748e1-202">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="748e1-203">첫 번째 단계로 hello 데이터 관리 게이트웨이를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="748e1-204">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="748e1-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="748e1-205">**ODBC 연결 된 서비스** 이 예제를 사용 하 여 hello 기본 인증.</span><span class="sxs-lookup"><span data-stu-id="748e1-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="748e1-206">사용할 수 있는 다른 유형의 인증은 [ODBC 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="748e1-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="748e1-207">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="748e1-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="748e1-208">**ODBC 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="748e1-208">**ODBC input dataset**</span></span>

<span data-ttu-id="748e1-209">hello 샘플 가정 ODBC 데이터베이스에 "MyTable" 테이블을 만든 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="748e1-210">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="748e1-211">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="748e1-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="748e1-212">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="748e1-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="748e1-213">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="748e1-214">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="748e1-215">**ODBC 원본(RelationalSource) 및 Blob 싱크 (BlobSink)를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="748e1-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="748e1-216">복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="748e1-217">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="748e1-218">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="748e1-219">ODBC에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="748e1-219">Type mapping for ODBC</span></span>
<span data-ttu-id="748e1-220">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="748e1-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="748e1-221">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="748e1-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="748e1-222">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="748e1-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="748e1-223">Hello에 설명 된 대로 ODBC 데이터 형식은 매핑된 too.NET 형식 ODBC 데이터 저장소에서 데이터를 이동할 때는 [ODBC 데이터 형식 매핑](https://msdn.microsoft.com/library/cc668763.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="748e1-224">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="748e1-224">Map source toosink columns</span></span>
<span data-ttu-id="748e1-225">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="748e1-226">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="748e1-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="748e1-227">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="748e1-228">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="748e1-229">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="748e1-230">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="748e1-231">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="748e1-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="748e1-232">GE Historian 저장소</span><span class="sxs-lookup"><span data-stu-id="748e1-232">GE Historian store</span></span>
<span data-ttu-id="748e1-233">ODBC 연결 된 서비스 toolink 만들면는 [GE Proficy 사 학자 (이제 GE 사 학자)](http://www.geautomation.com/products/proficy-historian) hello 다음 예제와 같이 저장소 tooan Azure 데이터 팩터리에 데이터:</span><span class="sxs-lookup"><span data-stu-id="748e1-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="748e1-234">온-프레미스 컴퓨터에 데이터 관리 게이트웨이 설치 하 고 hello 포털과 hello 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="748e1-235">온-프레미스 컴퓨터에 설치 하는 hello 게이트웨이 GE 사 학자 tooconnect toohello GE 사 학자 데이터 저장소에 대 한 hello ODBC 드라이버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="748e1-236">그러므로 hello 게이트웨이 컴퓨터에 아직 설치 되지 않은 경우에 hello 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="748e1-237">자세한 내용은 [연결 사용](#enabling-connectivity) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="748e1-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="748e1-238">데이터 팩터리 솔루션에서 GE 사 학자를 저장 하는 hello를 사용 하기 전에 hello 게이트웨이 hello 다음 섹션의 지침을 사용 하 여 toohello 데이터 저장소에 연결할 수 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="748e1-239">ODBC 데이터를 사용 하 여 자세한 개요는 hello부터에서 hello 문서 읽기 복사 작업에서 원본 데이터 저장소로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="748e1-240">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="748e1-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="748e1-241">tootroubleshoot 연결 문제를 사용 하 여 hello **진단** 탭 **데이터 관리 게이트웨이 구성 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="748e1-242">**데이터 관리 게이트웨이 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="748e1-243">에 대 한 "C:\Program Files\Microsoft 데이터 관리 Gateway\1.0\Shared\ConfigManager.exe" 직접 (또는) 검색을 실행 하거나 **게이트웨이** toofind 링크 너무**Microsoft 데이터 관리 게이트웨이** 다음 이미지는 hello와 같이 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![게이트웨이 검색](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="748e1-245">Toohello 전환 **진단** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-245">Switch toohello **Diagnostics** tab.</span></span>

    ![게이트웨이 진단](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="748e1-247">선택 hello **형식** 데이터 (연결 된 서비스)를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="748e1-248">지정 **인증** 입력 **자격 증명** (또는) 입력 **연결 문자열** 사용 되는 tooconnect toohello 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="748e1-249">클릭 **연결 테스트** tootest hello 연결 toohello 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="748e1-250">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="748e1-250">Performance and Tuning</span></span>
<span data-ttu-id="748e1-251">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="748e1-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
