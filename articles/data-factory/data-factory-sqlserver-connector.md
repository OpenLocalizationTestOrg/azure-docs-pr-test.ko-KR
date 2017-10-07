---
title: "SQL Server에서 aaaMove 데이터 tooand | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 Azure VM에서 또는 toomove 데이터/SQL Server에서 데이터베이스 방법 즉 온-프레미스에 대 한 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="93f72-103">Azure 데이터 팩터리를 사용 하 여 데이터 tooand IaaS (Azure VM)에서 또는 SQL Server 온-프레미스에서 이동</span><span class="sxs-lookup"><span data-stu-id="93f72-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="93f72-104">이 문서에서는 toouse 온-프레미스 SQL Server 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="93f72-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="93f72-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="93f72-106">Supported scenarios</span></span>
<span data-ttu-id="93f72-107">데이터를 복사할 수 **SQL Server 데이터베이스에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="93f72-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="93f72-108">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooa SQL Server 데이터베이스**:</span><span class="sxs-lookup"><span data-stu-id="93f72-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="93f72-109">지원되는 SQL Server 버전</span><span class="sxs-lookup"><span data-stu-id="93f72-109">Supported SQL Server versions</span></span>
<span data-ttu-id="93f72-110">이 SQL Server 커넥터 지원 데이터를 복사 toohello 다음 버전의 호스트 인스턴스 온-프레미스 또는 둘 다 SQL 인증 및 Windows 인증을 사용 하 여 Azure IaaS에서 /: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="93f72-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="93f72-111">연결 사용</span><span class="sxs-lookup"><span data-stu-id="93f72-111">Enabling connectivity</span></span>
<span data-ttu-id="93f72-112">SQL Server가 호스팅된 온-프레미스 또는 Azure IaaS에서 (인프라-as a Service) Vm을 연결 하는 데 필요한 단계 및 hello 개념 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="93f72-113">두 경우 모두 연결에 대 한 데이터 관리 게이트웨이 toouse가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="93f72-114">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="93f72-115">SQL Server에 연결하기 위해서는 게이트웨이 인스턴스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="93f72-116">게이트웨이 설치할 수 있지만 hello에 동일한 온-프레미스 컴퓨터 또는 클라우드 VM 인스턴스 성능 향상을 위해 SQL Server hello, 별도 컴퓨터에 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="93f72-117">리소스 경합을 줄이는 hello 게이트웨이 SQL Server가 별도 컴퓨터에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="93f72-118">시작</span><span class="sxs-lookup"><span data-stu-id="93f72-118">Getting started</span></span>
<span data-ttu-id="93f72-119">다른 도구/API를 사용하여 온-프레미스 SQL Server 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="93f72-120">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="93f72-121">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="93f72-122">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="93f72-123">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="93f72-124">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="93f72-125">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-125">Create a **data factory**.</span></span> <span data-ttu-id="93f72-126">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="93f72-127">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="93f72-128">예를 들어 SQL Server 데이터베이스 tooan Azure blob 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink SQL Server 데이터베이스 및 Azure 저장소 계정 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="93f72-129">연결 된 서비스 속성 특정 tooSQL 서버 데이터베이스에 대해 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="93f72-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="93f72-130">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="93f72-131">예에서 hello hello 마지막 단계에서 언급 한 hello 입력된 데이터를 포함 하 여 SQL Server 데이터베이스에 데이터 집합 toospecify hello SQL 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="93f72-132">And, 다른 데이터 집합 toospecify hello blob 컨테이너 만들기 및 SQL Server 데이터베이스 hello에서 복사 된 hello 데이터를 보유 하는 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="93f72-133">데이터 집합 속성을 특정 tooSQL 서버 데이터베이스에 대 한 참조 [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="93f72-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="93f72-134">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="93f72-135">앞에서 언급 한 hello 예제를 사용 하 여 SqlSource 소스 및 BlobSink로는 싱크도 hello 복사 작업에 대 한.</span><span class="sxs-lookup"><span data-stu-id="93f72-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="93f72-136">마찬가지로, Azure Blob 저장소 tooSQL 서버 데이터베이스에서에서 복사 하는 경우 BlobSource 및 사용 SqlSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="93f72-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="93f72-137">복사 활동 속성을 특정 tooSQL 서버 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="93f72-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="93f72-138">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="93f72-139">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="93f72-140">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="93f72-141">샘플 은/온-프레미스 SQL Server 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-from-and-to-sql-server) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="93f72-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="93f72-142">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooSQL 서버에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="93f72-143">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="93f72-143">Linked service properties</span></span>
<span data-ttu-id="93f72-144">형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="93f72-145">다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="93f72-146">다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="93f72-147">속성</span><span class="sxs-lookup"><span data-stu-id="93f72-147">Property</span></span> | <span data-ttu-id="93f72-148">설명</span><span class="sxs-lookup"><span data-stu-id="93f72-148">Description</span></span> | <span data-ttu-id="93f72-149">필수</span><span class="sxs-lookup"><span data-stu-id="93f72-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93f72-150">type</span><span class="sxs-lookup"><span data-stu-id="93f72-150">type</span></span> |<span data-ttu-id="93f72-151">hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="93f72-152">예</span><span class="sxs-lookup"><span data-stu-id="93f72-152">Yes</span></span> |
| <span data-ttu-id="93f72-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="93f72-153">connectionString</span></span> |<span data-ttu-id="93f72-154">SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="93f72-155">예</span><span class="sxs-lookup"><span data-stu-id="93f72-155">Yes</span></span> |
| <span data-ttu-id="93f72-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="93f72-156">gatewayName</span></span> |<span data-ttu-id="93f72-157">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="93f72-158">예</span><span class="sxs-lookup"><span data-stu-id="93f72-158">Yes</span></span> |
| <span data-ttu-id="93f72-159">username</span><span class="sxs-lookup"><span data-stu-id="93f72-159">username</span></span> |<span data-ttu-id="93f72-160">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="93f72-161">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="93f72-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="93f72-162">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-162">No</span></span> |
| <span data-ttu-id="93f72-163">암호</span><span class="sxs-lookup"><span data-stu-id="93f72-163">password</span></span> |<span data-ttu-id="93f72-164">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="93f72-165">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-165">No</span></span> |

<span data-ttu-id="93f72-166">Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):</span><span class="sxs-lookup"><span data-stu-id="93f72-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="93f72-167">샘플</span><span class="sxs-lookup"><span data-stu-id="93f72-167">Samples</span></span>
<span data-ttu-id="93f72-168">**SQL 인증을 사용하는 JSON**</span><span class="sxs-lookup"><span data-stu-id="93f72-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="93f72-169">**Windows 인증을 사용하는 JSON**</span><span class="sxs-lookup"><span data-stu-id="93f72-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="93f72-170">데이터 관리 게이트웨이 지정 된 hello를 가장 하는 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="93f72-171">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="93f72-171">Dataset properties</span></span>
<span data-ttu-id="93f72-172">형식의 데이터 집합 hello 샘플에서 사용한 **SqlServerTable** toorepresent SQL Server 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="93f72-173">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="93f72-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="93f72-174">데이터 집합 JSON의 structure, availability, policy와 같은 섹션은 SQL Server, Azure Blob, Azure 테이블 등의 모든 데이터베이스 형식에 대해 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="93f72-175">hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="93f72-176">hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **SqlServerTable** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="93f72-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="93f72-177">속성</span><span class="sxs-lookup"><span data-stu-id="93f72-177">Property</span></span> | <span data-ttu-id="93f72-178">설명</span><span class="sxs-lookup"><span data-stu-id="93f72-178">Description</span></span> | <span data-ttu-id="93f72-179">필수</span><span class="sxs-lookup"><span data-stu-id="93f72-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93f72-180">tableName</span><span class="sxs-lookup"><span data-stu-id="93f72-180">tableName</span></span> |<span data-ttu-id="93f72-181">Hello 테이블 또는 뷰의 연결 된 서비스는 hello SQL Server 데이터베이스 인스턴스의 이름이 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="93f72-182">예</span><span class="sxs-lookup"><span data-stu-id="93f72-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="93f72-183">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="93f72-183">Copy activity properties</span></span>
<span data-ttu-id="93f72-184">SQL Server 데이터베이스에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**SqlSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="93f72-185">마찬가지로, 데이터 tooa SQL Server 데이터베이스를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="93f72-186">이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="93f72-187">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="93f72-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="93f72-188">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="93f72-189">복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="93f72-190">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="93f72-191">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="93f72-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="93f72-192">SqlSource</span></span>
<span data-ttu-id="93f72-193">복사 작업의 원본 유형의 경우 **SqlSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="93f72-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="93f72-194">속성</span><span class="sxs-lookup"><span data-stu-id="93f72-194">Property</span></span> | <span data-ttu-id="93f72-195">설명</span><span class="sxs-lookup"><span data-stu-id="93f72-195">Description</span></span> | <span data-ttu-id="93f72-196">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="93f72-196">Allowed values</span></span> | <span data-ttu-id="93f72-197">필수</span><span class="sxs-lookup"><span data-stu-id="93f72-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93f72-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="93f72-198">sqlReaderQuery</span></span> |<span data-ttu-id="93f72-199">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="93f72-200">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="93f72-200">SQL query string.</span></span> <span data-ttu-id="93f72-201">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="93f72-201">For example: select * from MyTable.</span></span> <span data-ttu-id="93f72-202">Hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스에서 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="93f72-203">지정 하지 않으면 실행 되는 SQL 문을 hello: MyTable 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="93f72-204">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-204">No</span></span> |
| <span data-ttu-id="93f72-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="93f72-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="93f72-206">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="93f72-207">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-207">Name of hello stored procedure.</span></span> <span data-ttu-id="93f72-208">hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="93f72-209">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-209">No</span></span> |
| <span data-ttu-id="93f72-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="93f72-210">storedProcedureParameters</span></span> |<span data-ttu-id="93f72-211">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="93f72-212">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-212">Name/value pairs.</span></span> <span data-ttu-id="93f72-213">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="93f72-214">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-214">No</span></span> |

<span data-ttu-id="93f72-215">경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="93f72-216">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="93f72-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="93f72-217">Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="93f72-218">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="93f72-219">사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="93f72-220">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="93f72-221">파이프라인</span><span class="sxs-lookup"><span data-stu-id="93f72-221">SqlSink</span></span>
<span data-ttu-id="93f72-222">**SqlSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="93f72-223">속성</span><span class="sxs-lookup"><span data-stu-id="93f72-223">Property</span></span> | <span data-ttu-id="93f72-224">설명</span><span class="sxs-lookup"><span data-stu-id="93f72-224">Description</span></span> | <span data-ttu-id="93f72-225">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="93f72-225">Allowed values</span></span> | <span data-ttu-id="93f72-226">필수</span><span class="sxs-lookup"><span data-stu-id="93f72-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93f72-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="93f72-227">writeBatchTimeout</span></span> |<span data-ttu-id="93f72-228">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="93f72-229">timespan</span><span class="sxs-lookup"><span data-stu-id="93f72-229">timespan</span></span><br/><br/> <span data-ttu-id="93f72-230">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="93f72-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="93f72-231">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-231">No</span></span> |
| <span data-ttu-id="93f72-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="93f72-232">writeBatchSize</span></span> |<span data-ttu-id="93f72-233">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="93f72-234">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="93f72-234">Integer (number of rows)</span></span> |<span data-ttu-id="93f72-235">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="93f72-235">No (default: 10000)</span></span> |
| <span data-ttu-id="93f72-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="93f72-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="93f72-237">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="93f72-238">자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="93f72-239">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-239">A query statement.</span></span> |<span data-ttu-id="93f72-240">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-240">No</span></span> |
| <span data-ttu-id="93f72-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="93f72-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="93f72-242">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="93f72-243">자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="93f72-244">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="93f72-245">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-245">No</span></span> |
| <span data-ttu-id="93f72-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="93f72-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="93f72-247">Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="93f72-248">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="93f72-249">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-249">No</span></span> |
| <span data-ttu-id="93f72-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="93f72-250">storedProcedureParameters</span></span> |<span data-ttu-id="93f72-251">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="93f72-252">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-252">Name/value pairs.</span></span> <span data-ttu-id="93f72-253">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="93f72-254">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-254">No</span></span> |
| <span data-ttu-id="93f72-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="93f72-255">sqlWriterTableType</span></span> |<span data-ttu-id="93f72-256">테이블 형식 이름 toobe hello 저장 프로시저에 사용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="93f72-257">복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="93f72-258">저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="93f72-259">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="93f72-259">A table type name.</span></span> |<span data-ttu-id="93f72-260">아니요</span><span class="sxs-lookup"><span data-stu-id="93f72-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="93f72-261">TooSQL 서버와의 데이터를 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="93f72-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="93f72-262">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="93f72-263">샘플 표시 방법을 따르는 hello toocopy 데이터 tooand SQL Server와 Azure Blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="93f72-264">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="93f72-265">예: SQL Server tooAzure Blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="93f72-266">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="93f72-266">hello following sample shows:</span></span>

1. <span data-ttu-id="93f72-267">[OnPremisesSqlServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="93f72-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="93f72-268">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="93f72-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="93f72-269">[SqlServerTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="93f72-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="93f72-270">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="93f72-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="93f72-271">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="93f72-272">hello 샘플 시계열 데이터 복사 SQL Server 테이블 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="93f72-273">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="93f72-274">첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="93f72-275">hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="93f72-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="93f72-276">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="93f72-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="93f72-277">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="93f72-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="93f72-278">**SQL Server 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="93f72-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="93f72-279">hello 샘플 테이블 "MyTable" SQL Server에서 만들고 시계열 데이터에 대 한 "timestampcolumn" 라는 열이 포함 된 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="93f72-280">TableName typeProperty hello 데이터 집합의 단일 데이터 집합 이지만 단일 테이블을 사용 하 여 동일한 데이터베이스를 사용 해야 하는 hello 내에서 여러 테이블에 대해 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="93f72-281">설정 "외부": "true" 알리고 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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
<span data-ttu-id="93f72-282">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="93f72-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="93f72-283">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="93f72-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="93f72-284">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="93f72-285">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="93f72-286">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="93f72-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="93f72-287">복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="93f72-288">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="93f72-289">hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="93f72-290">이 예제에서는 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="93f72-291">복사 활동 hello hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="93f72-292">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="93f72-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="93f72-293">hello sqlReaderQuery hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스 내에서 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="93f72-294">데이터 집합의 tableName typeProperty hello으로 설정 하는 제한 된 tooonly hello 테이블이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="93f72-295">Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="93f72-296">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="93f72-297">Hello 참조 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello SqlSource에서 BlobSink로 지원 되는 속성 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="93f72-298">예: Azure Blob tooSQL 서버에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="93f72-299">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="93f72-299">hello following sample shows:</span></span>

1. <span data-ttu-id="93f72-300">hello는 연결 된 서비스 유형의 [OnPremisesSqlServer](#linked-service-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="93f72-301">hello는 연결 된 서비스 유형의 [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="93f72-302">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="93f72-303">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="93f72-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="93f72-304">hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#sql-server-copy-activity-type-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="93f72-305">hello 샘플 시계열 데이터 복사, Azure blob tooa SQL Server 테이블에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="93f72-306">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="93f72-307">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="93f72-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="93f72-308">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="93f72-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="93f72-309">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="93f72-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="93f72-310">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="93f72-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="93f72-311">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="93f72-312">연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="93f72-313">"external": "true" 설정을 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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
<span data-ttu-id="93f72-314">**SQL Server 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="93f72-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="93f72-315">hello 샘플 SQL Server에서 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="93f72-316">SQL Server에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="93f72-317">새 행 1 시간 마다 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="93f72-318">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="93f72-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="93f72-319">복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="93f72-320">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="93f72-321">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="93f72-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="93f72-322">SQL Server tooaccept 원격 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="93f72-323">**SQL Server Management Studio**를 시작하고 **서버**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="93f72-324">선택 **연결** hello 목록 및 검사에서 **허용 원격 연결 toohello 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![원격 연결 사용](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="93f72-326">참조 [hello 원격 액세스 서버 구성 옵션 구성](https://msdn.microsoft.com/library/ms191464.aspx) 자세한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="93f72-327">**SQL Server 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="93f72-328">확장 **SQL Server 네트워크 구성** hello에 대 한 인스턴스 마우스 선택 **MSSQLSERVER에 대 한 프로토콜**합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="93f72-329">프로토콜 hello 오른쪽 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="93f72-330">**TCP/IP**를 마우스 오른쪽 단추로 클릭하고 **사용**을 클릭하여 TCP/IP를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP 사용](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="93f72-332">TCP/IP 프로토콜을 사용하는 다른 방법 및 자세한 내용은 [서버 네트워크 프로토콜 사용 또는 사용 안 함](https://msdn.microsoft.com/library/ms191294.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="93f72-333">같은 창 hello에서 두 번 클릭 **TCP/IP** toolaunch **TCP/IP 속성** 창.</span><span class="sxs-lookup"><span data-stu-id="93f72-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="93f72-334">Toohello 전환 **IP 주소** 탭 합니다. Toosee 아래로 스크롤하여 **IPAll** 섹션.</span><span class="sxs-lookup"><span data-stu-id="93f72-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="93f72-335">Hello 다운 참고 * * TCP 포트 * * (기본값은 **1433**).</span><span class="sxs-lookup"><span data-stu-id="93f72-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="93f72-336">만들기는 **hello Windows 방화벽에 대 한 규칙** hello 컴퓨터 tooallow이이 포트를 통해 들어오는 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="93f72-337">**연결을 확인**: tooconnect toohello 정규화 된 이름을 사용 하 여 SQL Server는 다른 컴퓨터에서 SQL Server Management Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="93f72-338">예: "<machine><domain>.corp<company>.com,1433".</span><span class="sxs-lookup"><span data-stu-id="93f72-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="93f72-339">참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="93f72-340">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="93f72-341">Hello 대상 데이터베이스의 id 열</span><span class="sxs-lookup"><span data-stu-id="93f72-341">Identity columns in hello target database</span></span>
<span data-ttu-id="93f72-342">이 섹션에서는 id 열이 있는 없는 id 열 tooa 대상 테이블에 있는 원본 테이블에서 데이터를 복사 하는 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="93f72-343">**원본 테이블:**</span><span class="sxs-lookup"><span data-stu-id="93f72-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="93f72-344">**대상 테이블:**</span><span class="sxs-lookup"><span data-stu-id="93f72-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="93f72-345">해당 hello 대상 테이블에 id 열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="93f72-346">**원본 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="93f72-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="93f72-347">**대상 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="93f72-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="93f72-348">원본 테이블과 대상 테이블의 스키마가 서로 다릅니다(대상에 ID가 포함된 추가 열이 있음).</span><span class="sxs-lookup"><span data-stu-id="93f72-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="93f72-349">이 시나리오에서는 toospecify 필요 **구조** hello id 열이 포함 되지 않으면 hello 대상 데이터 집합 정의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="93f72-350">SQL 싱크에서 저장된 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="93f72-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="93f72-351">파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="93f72-352">SQL 서버에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="93f72-352">Type mapping for SQL server</span></span>
<span data-ttu-id="93f72-353">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 hello 복사 활동 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:</span><span class="sxs-lookup"><span data-stu-id="93f72-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="93f72-354">네이티브 소스 형식 too.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="93f72-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="93f72-355">.NET 형식 toonative 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="93f72-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="93f72-356">데이터를 이동 너무 및 SQL server에서 hello SQL 형식 too.NET 형식에서 그 반대의 다음 매핑이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="93f72-357">hello 매핑 hello ADO.NET에 대 한 SQL Server 데이터 형식 매핑과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="93f72-358">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="93f72-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="93f72-359">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="93f72-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="93f72-360">bigint</span><span class="sxs-lookup"><span data-stu-id="93f72-360">bigint</span></span> |<span data-ttu-id="93f72-361">Int64</span><span class="sxs-lookup"><span data-stu-id="93f72-361">Int64</span></span> |
| <span data-ttu-id="93f72-362">binary</span><span class="sxs-lookup"><span data-stu-id="93f72-362">binary</span></span> |<span data-ttu-id="93f72-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-363">Byte[]</span></span> |
| <span data-ttu-id="93f72-364">bit</span><span class="sxs-lookup"><span data-stu-id="93f72-364">bit</span></span> |<span data-ttu-id="93f72-365">Boolean</span><span class="sxs-lookup"><span data-stu-id="93f72-365">Boolean</span></span> |
| <span data-ttu-id="93f72-366">char</span><span class="sxs-lookup"><span data-stu-id="93f72-366">char</span></span> |<span data-ttu-id="93f72-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-367">String, Char[]</span></span> |
| <span data-ttu-id="93f72-368">date</span><span class="sxs-lookup"><span data-stu-id="93f72-368">date</span></span> |<span data-ttu-id="93f72-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="93f72-369">DateTime</span></span> |
| <span data-ttu-id="93f72-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="93f72-370">Datetime</span></span> |<span data-ttu-id="93f72-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="93f72-371">DateTime</span></span> |
| <span data-ttu-id="93f72-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="93f72-372">datetime2</span></span> |<span data-ttu-id="93f72-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="93f72-373">DateTime</span></span> |
| <span data-ttu-id="93f72-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="93f72-374">Datetimeoffset</span></span> |<span data-ttu-id="93f72-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="93f72-375">DateTimeOffset</span></span> |
| <span data-ttu-id="93f72-376">10진수</span><span class="sxs-lookup"><span data-stu-id="93f72-376">Decimal</span></span> |<span data-ttu-id="93f72-377">10진수</span><span class="sxs-lookup"><span data-stu-id="93f72-377">Decimal</span></span> |
| <span data-ttu-id="93f72-378">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="93f72-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="93f72-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-379">Byte[]</span></span> |
| <span data-ttu-id="93f72-380">Float</span><span class="sxs-lookup"><span data-stu-id="93f72-380">Float</span></span> |<span data-ttu-id="93f72-381">Double</span><span class="sxs-lookup"><span data-stu-id="93f72-381">Double</span></span> |
| <span data-ttu-id="93f72-382">이미지</span><span class="sxs-lookup"><span data-stu-id="93f72-382">image</span></span> |<span data-ttu-id="93f72-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-383">Byte[]</span></span> |
| <span data-ttu-id="93f72-384">int</span><span class="sxs-lookup"><span data-stu-id="93f72-384">int</span></span> |<span data-ttu-id="93f72-385">Int32</span><span class="sxs-lookup"><span data-stu-id="93f72-385">Int32</span></span> |
| <span data-ttu-id="93f72-386">money</span><span class="sxs-lookup"><span data-stu-id="93f72-386">money</span></span> |<span data-ttu-id="93f72-387">10진수</span><span class="sxs-lookup"><span data-stu-id="93f72-387">Decimal</span></span> |
| <span data-ttu-id="93f72-388">nchar</span><span class="sxs-lookup"><span data-stu-id="93f72-388">nchar</span></span> |<span data-ttu-id="93f72-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-389">String, Char[]</span></span> |
| <span data-ttu-id="93f72-390">ntext</span><span class="sxs-lookup"><span data-stu-id="93f72-390">ntext</span></span> |<span data-ttu-id="93f72-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-391">String, Char[]</span></span> |
| <span data-ttu-id="93f72-392">numeric</span><span class="sxs-lookup"><span data-stu-id="93f72-392">numeric</span></span> |<span data-ttu-id="93f72-393">10진수</span><span class="sxs-lookup"><span data-stu-id="93f72-393">Decimal</span></span> |
| <span data-ttu-id="93f72-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="93f72-394">nvarchar</span></span> |<span data-ttu-id="93f72-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-395">String, Char[]</span></span> |
| <span data-ttu-id="93f72-396">real</span><span class="sxs-lookup"><span data-stu-id="93f72-396">real</span></span> |<span data-ttu-id="93f72-397">단일</span><span class="sxs-lookup"><span data-stu-id="93f72-397">Single</span></span> |
| <span data-ttu-id="93f72-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="93f72-398">rowversion</span></span> |<span data-ttu-id="93f72-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-399">Byte[]</span></span> |
| <span data-ttu-id="93f72-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="93f72-400">smalldatetime</span></span> |<span data-ttu-id="93f72-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="93f72-401">DateTime</span></span> |
| <span data-ttu-id="93f72-402">smallint</span><span class="sxs-lookup"><span data-stu-id="93f72-402">smallint</span></span> |<span data-ttu-id="93f72-403">Int16</span><span class="sxs-lookup"><span data-stu-id="93f72-403">Int16</span></span> |
| <span data-ttu-id="93f72-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="93f72-404">smallmoney</span></span> |<span data-ttu-id="93f72-405">10진수</span><span class="sxs-lookup"><span data-stu-id="93f72-405">Decimal</span></span> |
| <span data-ttu-id="93f72-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="93f72-406">sql_variant</span></span> |<span data-ttu-id="93f72-407">개체 *</span><span class="sxs-lookup"><span data-stu-id="93f72-407">Object *</span></span> |
| <span data-ttu-id="93f72-408">텍스트</span><span class="sxs-lookup"><span data-stu-id="93f72-408">text</span></span> |<span data-ttu-id="93f72-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-409">String, Char[]</span></span> |
| <span data-ttu-id="93f72-410">실시간</span><span class="sxs-lookup"><span data-stu-id="93f72-410">time</span></span> |<span data-ttu-id="93f72-411">timespan</span><span class="sxs-lookup"><span data-stu-id="93f72-411">TimeSpan</span></span> |
| <span data-ttu-id="93f72-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="93f72-412">timestamp</span></span> |<span data-ttu-id="93f72-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-413">Byte[]</span></span> |
| <span data-ttu-id="93f72-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="93f72-414">tinyint</span></span> |<span data-ttu-id="93f72-415">Byte</span><span class="sxs-lookup"><span data-stu-id="93f72-415">Byte</span></span> |
| <span data-ttu-id="93f72-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="93f72-416">uniqueidentifier</span></span> |<span data-ttu-id="93f72-417">Guid</span><span class="sxs-lookup"><span data-stu-id="93f72-417">Guid</span></span> |
| <span data-ttu-id="93f72-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="93f72-418">varbinary</span></span> |<span data-ttu-id="93f72-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="93f72-419">Byte[]</span></span> |
| <span data-ttu-id="93f72-420">varchar</span><span class="sxs-lookup"><span data-stu-id="93f72-420">varchar</span></span> |<span data-ttu-id="93f72-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="93f72-421">String, Char[]</span></span> |
| <span data-ttu-id="93f72-422">xml</span><span class="sxs-lookup"><span data-stu-id="93f72-422">xml</span></span> |<span data-ttu-id="93f72-423">xml</span><span class="sxs-lookup"><span data-stu-id="93f72-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="93f72-424">소스 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="93f72-424">Mapping source toosink columns</span></span>
<span data-ttu-id="93f72-425">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="93f72-426">반복 가능한 복사</span><span class="sxs-lookup"><span data-stu-id="93f72-426">Repeatable copy</span></span>
<span data-ttu-id="93f72-427">데이터 tooSQL 서버 데이터베이스를 복사할 때 hello 복사 활동 기본적으로 데이터 toohello 싱크 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="93f72-428">UPSERT tooperform 대신 참조 [반복 쓰기 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서.</span><span class="sxs-lookup"><span data-stu-id="93f72-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="93f72-429">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="93f72-430">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="93f72-431">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="93f72-432">Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="93f72-433">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93f72-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="93f72-434">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="93f72-434">Performance and Tuning</span></span>
<span data-ttu-id="93f72-435">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93f72-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
