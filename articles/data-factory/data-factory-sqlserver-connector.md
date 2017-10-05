---
title: "SQL Server 간 데이터 이동 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용하여 온-프레미스 또는 Azure VM에 있는 SQL Server 데이터베이스 간에 데이터를 이동하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="da9d3-103">Azure 데이터 팩터리를 사용하여 온-프레미스 또는 IaaS(Azure VM) SQL Server 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="da9d3-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="da9d3-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 SQL Server 데이터베이스의 데이터를 다른 곳으로 이동하는 방법 또는 그 반대로 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="da9d3-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="da9d3-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="da9d3-106">Supported scenarios</span></span>
<span data-ttu-id="da9d3-107">**SQL Server 데이터베이스**에서 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="da9d3-108">다음 데이터 저장소에서 **SQL Server 데이터베이스**로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="da9d3-109">지원되는 SQL Server 버전</span><span class="sxs-lookup"><span data-stu-id="da9d3-109">Supported SQL Server versions</span></span>
<span data-ttu-id="da9d3-110">이 SQL Server 커넥터는 SQL 인증 및 Windows 인증을 사용하여 온-프레미스 또는 Azure IaaS에서 호스트되는 인스턴스의 SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005 버전 간 데이터 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="da9d3-111">연결 사용</span><span class="sxs-lookup"><span data-stu-id="da9d3-111">Enabling connectivity</span></span>
<span data-ttu-id="da9d3-112">SQL Server가 호스팅되는 온-프레미스 또는 Azure IaaS(Infrastructure-as-a-Service) VM에 연결하는 데 필요한 개념과 단계는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="da9d3-113">두 경우 모두 연결에 데이터 관리 게이트웨이를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="da9d3-114">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="da9d3-115">SQL Server에 연결하기 위해서는 게이트웨이 인스턴스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="da9d3-116">성능 향상을 위해 게이트웨이를 동일한 온-프레미스 컴퓨터 또는 클라우드 VM 인스턴스에 SQL Server로 설치할 수는 있지만, 별도의 컴퓨터에 게이트웨이를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="da9d3-117">게이트웨이와 SQL Server를 각기 다른 컴퓨터에 설치하면 리소스 경합을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="da9d3-118">시작</span><span class="sxs-lookup"><span data-stu-id="da9d3-118">Getting started</span></span>
<span data-ttu-id="da9d3-119">다른 도구/API를 사용하여 온-프레미스 SQL Server 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="da9d3-120">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="da9d3-121">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="da9d3-122">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="da9d3-123">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="da9d3-124">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="da9d3-125">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-125">Create a **data factory**.</span></span> <span data-ttu-id="da9d3-126">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="da9d3-127">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="da9d3-128">예를 들어 SQL Server 데이터베이스에서 Azure Blob Storage로 복사하는 경우 SQL Server 데이터베이스 및 Azure Storage 계정을 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="da9d3-129">SQL Server 데이터베이스와 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="da9d3-130">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="da9d3-131">마지막 단계에서 설명한 예에서는 입력 데이터가 포함된 SQL Server 데이터베이스의 SQL 테이블을 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="da9d3-132">그리고 Blob 컨테이너와 SQL Server 데이터베이스에서 복사된 데이터가 저장되는 폴더를 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="da9d3-133">SQL Server 데이터베이스와 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="da9d3-134">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="da9d3-135">앞에서 언급한 예에서는 SqlSource를 원본으로, BlobSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="da9d3-136">마찬가지로, Azure Blob Storage에서 SQL Server 데이터베이스로 복사하는 경우 복사 작업에 BlobSource 및 SqlSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="da9d3-137">SQL Server 데이터베이스와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="da9d3-138">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="da9d3-139">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="da9d3-140">도구/API를 사용하는 경우(.NET API 제외) JSON 형식을 사용하여 데이터 팩터리 엔터티를 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="da9d3-141">다른 곳에서 온-프레미스 SQL Server 데이터베이스로 또는 그 반대로 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON의 예](#json-examples-for-copying-data-from-and-to-sql-server) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="da9d3-142">다음 섹션에서는 SQL Server에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="da9d3-143">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-143">Linked service properties</span></span>
<span data-ttu-id="da9d3-144">**OnPremisesSqlServer** 형식의 연결된 서비스를 만들어 온-프레미스 SQL Server Database를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="da9d3-145">다음 테이블은 온-프레미스 SQL Server 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="da9d3-146">다음 표에서는 SQL Server 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="da9d3-147">속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-147">Property</span></span> | <span data-ttu-id="da9d3-148">설명</span><span class="sxs-lookup"><span data-stu-id="da9d3-148">Description</span></span> | <span data-ttu-id="da9d3-149">필수</span><span class="sxs-lookup"><span data-stu-id="da9d3-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da9d3-150">type</span><span class="sxs-lookup"><span data-stu-id="da9d3-150">type</span></span> |<span data-ttu-id="da9d3-151">type 속성은 **OnPremisesSqlServer**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="da9d3-152">예</span><span class="sxs-lookup"><span data-stu-id="da9d3-152">Yes</span></span> |
| <span data-ttu-id="da9d3-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="da9d3-153">connectionString</span></span> |<span data-ttu-id="da9d3-154">SQL 인증 또는 Windows 인증을 사용하여 온-프레미스 SQL Server 데이터베이스에 연결하는 데 필요한 connectionString 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="da9d3-155">예</span><span class="sxs-lookup"><span data-stu-id="da9d3-155">Yes</span></span> |
| <span data-ttu-id="da9d3-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="da9d3-156">gatewayName</span></span> |<span data-ttu-id="da9d3-157">데이터 팩터리 서비스가 온-프레미스 SQL Server 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="da9d3-158">예</span><span class="sxs-lookup"><span data-stu-id="da9d3-158">Yes</span></span> |
| <span data-ttu-id="da9d3-159">username</span><span class="sxs-lookup"><span data-stu-id="da9d3-159">username</span></span> |<span data-ttu-id="da9d3-160">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="da9d3-161">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="da9d3-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="da9d3-162">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-162">No</span></span> |
| <span data-ttu-id="da9d3-163">password</span><span class="sxs-lookup"><span data-stu-id="da9d3-163">password</span></span> |<span data-ttu-id="da9d3-164">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="da9d3-165">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-165">No</span></span> |

<span data-ttu-id="da9d3-166">**New-AzureRmDataFactoryEncryptValue** cmdlet를 사용하여 자격 증명을 암호화하고 다음 예제와 같이 연결 문자열에 해당 자격 증명을 사용할 수 있습니다(**EncryptedCredential** 속성).</span><span class="sxs-lookup"><span data-stu-id="da9d3-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="da9d3-167">샘플</span><span class="sxs-lookup"><span data-stu-id="da9d3-167">Samples</span></span>
<span data-ttu-id="da9d3-168">**SQL 인증을 사용하는 JSON**</span><span class="sxs-lookup"><span data-stu-id="da9d3-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="da9d3-169">**Windows 인증을 사용하는 JSON**</span><span class="sxs-lookup"><span data-stu-id="da9d3-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="da9d3-170">데이터 관리 게이트웨이는 지정된 사용자 계정을 가장하여 온-프레미스 SQL Server Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="da9d3-171">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-171">Dataset properties</span></span>
<span data-ttu-id="da9d3-172">샘플에서 SQL Server 데이터베이스의 테이블을 나타내는 데 **SqlServerTable** 형식의 데이터 집합을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="da9d3-173">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="da9d3-174">데이터 집합 JSON의 structure, availability, policy와 같은 섹션은 SQL Server, Azure Blob, Azure 테이블 등의 모든 데이터베이스 형식에 대해 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="da9d3-175">typeProperties 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="da9d3-176">**SqlServerTable** 데이터 집합 형식의 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="da9d3-177">속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-177">Property</span></span> | <span data-ttu-id="da9d3-178">설명</span><span class="sxs-lookup"><span data-stu-id="da9d3-178">Description</span></span> | <span data-ttu-id="da9d3-179">필수</span><span class="sxs-lookup"><span data-stu-id="da9d3-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da9d3-180">tableName</span><span class="sxs-lookup"><span data-stu-id="da9d3-180">tableName</span></span> |<span data-ttu-id="da9d3-181">연결된 서비스가 참조하는 SQL Server 데이터베이스 인스턴스에서 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="da9d3-182">예</span><span class="sxs-lookup"><span data-stu-id="da9d3-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="da9d3-183">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-183">Copy activity properties</span></span>
<span data-ttu-id="da9d3-184">SQL Server 데이터베이스에서 데이터를 이동하는 경우 복사 작업의 원본 유형을 **SqlSource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="da9d3-185">마찬가지로 SQL Server 데이터베이스로 데이터를 이동하는 경우 복사 작업의 싱크 유형을 **SqlSink**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="da9d3-186">이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="da9d3-187">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="da9d3-188">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="da9d3-189">복사 작업은 하나의 입력을 가지고 하나의 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="da9d3-190">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="da9d3-191">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="da9d3-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="da9d3-192">SqlSource</span></span>
<span data-ttu-id="da9d3-193">복사 활동의 소스가 **SqlSource** 형식인 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="da9d3-194">속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-194">Property</span></span> | <span data-ttu-id="da9d3-195">설명</span><span class="sxs-lookup"><span data-stu-id="da9d3-195">Description</span></span> | <span data-ttu-id="da9d3-196">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="da9d3-196">Allowed values</span></span> | <span data-ttu-id="da9d3-197">필수</span><span class="sxs-lookup"><span data-stu-id="da9d3-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da9d3-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="da9d3-198">sqlReaderQuery</span></span> |<span data-ttu-id="da9d3-199">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-199">Use the custom query to read data.</span></span> |<span data-ttu-id="da9d3-200">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="da9d3-200">SQL query string.</span></span> <span data-ttu-id="da9d3-201">예: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="da9d3-201">For example: select * from MyTable.</span></span> <span data-ttu-id="da9d3-202">입력 데이터 집합에 의해 참조되는 데이터베이스의 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="da9d3-203">지정하지 않는 경우 실행되는 SQL 문: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="da9d3-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="da9d3-204">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-204">No</span></span> |
| <span data-ttu-id="da9d3-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="da9d3-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="da9d3-206">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="da9d3-207">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-207">Name of the stored procedure.</span></span> <span data-ttu-id="da9d3-208">마지막 SQL 문은 저장 프로시저의 SELECT 문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="da9d3-209">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-209">No</span></span> |
| <span data-ttu-id="da9d3-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="da9d3-210">storedProcedureParameters</span></span> |<span data-ttu-id="da9d3-211">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="da9d3-212">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-212">Name/value pairs.</span></span> <span data-ttu-id="da9d3-213">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="da9d3-214">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-214">No</span></span> |

<span data-ttu-id="da9d3-215">**sqlReaderQuery** 가 SqlSource에 지정되면 복사 작업은 데이터를 가져오는 SQL Server 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="da9d3-216">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="da9d3-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="da9d3-217">sqlReaderQuery 또는 sqlReaderStoredProcedureName을 지정하지 않으면 structure 섹션에 정의된 열을 사용하여 SQL Server Database에 대해 실행할 선택 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="da9d3-218">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="da9d3-219">**sqlReaderStoredProcedureName**을 사용하는 경우에도 데이터 집합 JSON에서 **tableName** 속성 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="da9d3-220">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="da9d3-221">파이프라인</span><span class="sxs-lookup"><span data-stu-id="da9d3-221">SqlSink</span></span>
<span data-ttu-id="da9d3-222">**SqlSink** 는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="da9d3-223">속성</span><span class="sxs-lookup"><span data-stu-id="da9d3-223">Property</span></span> | <span data-ttu-id="da9d3-224">설명</span><span class="sxs-lookup"><span data-stu-id="da9d3-224">Description</span></span> | <span data-ttu-id="da9d3-225">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="da9d3-225">Allowed values</span></span> | <span data-ttu-id="da9d3-226">필수</span><span class="sxs-lookup"><span data-stu-id="da9d3-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da9d3-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="da9d3-227">writeBatchTimeout</span></span> |<span data-ttu-id="da9d3-228">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="da9d3-229">timespan</span><span class="sxs-lookup"><span data-stu-id="da9d3-229">timespan</span></span><br/><br/> <span data-ttu-id="da9d3-230">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="da9d3-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="da9d3-231">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-231">No</span></span> |
| <span data-ttu-id="da9d3-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="da9d3-232">writeBatchSize</span></span> |<span data-ttu-id="da9d3-233">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="da9d3-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="da9d3-234">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="da9d3-234">Integer (number of rows)</span></span> |<span data-ttu-id="da9d3-235">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="da9d3-235">No (default: 10000)</span></span> |
| <span data-ttu-id="da9d3-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="da9d3-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="da9d3-237">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="da9d3-238">자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="da9d3-239">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-239">A query statement.</span></span> |<span data-ttu-id="da9d3-240">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-240">No</span></span> |
| <span data-ttu-id="da9d3-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="da9d3-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="da9d3-242">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="da9d3-243">자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="da9d3-244">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="da9d3-245">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-245">No</span></span> |
| <span data-ttu-id="da9d3-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="da9d3-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="da9d3-247">대상 테이블에 대한 데이터 Upsert(업데이트/삽입)를 수행하는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="da9d3-248">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-248">Name of the stored procedure.</span></span> |<span data-ttu-id="da9d3-249">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-249">No</span></span> |
| <span data-ttu-id="da9d3-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="da9d3-250">storedProcedureParameters</span></span> |<span data-ttu-id="da9d3-251">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="da9d3-252">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-252">Name/value pairs.</span></span> <span data-ttu-id="da9d3-253">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="da9d3-254">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-254">No</span></span> |
| <span data-ttu-id="da9d3-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="da9d3-255">sqlWriterTableType</span></span> |<span data-ttu-id="da9d3-256">저장 프로시저에 사용할 테이블 형식 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="da9d3-257">복사 작업을 사용하면 이 테이블 형식으로 임시 테이블에서 사용할 수 있는 데이터를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="da9d3-258">그러면 저장 프로시저 코드가 복사되는 데이터를 기존 데이터와 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="da9d3-259">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="da9d3-259">A table type name.</span></span> |<span data-ttu-id="da9d3-260">아니요</span><span class="sxs-lookup"><span data-stu-id="da9d3-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="da9d3-261">SQL Server로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="da9d3-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="da9d3-262">다음 예에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="da9d3-263">다음 샘플은 SQL Server 및 Azure Blob 저장소 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="da9d3-264">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="da9d3-265">예: SQL Server에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="da9d3-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="da9d3-266">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-266">The following sample shows:</span></span>

1. <span data-ttu-id="da9d3-267">[OnPremisesSqlServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="da9d3-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="da9d3-268">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="da9d3-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="da9d3-269">[SqlServerTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="da9d3-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="da9d3-270">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="da9d3-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="da9d3-271">[SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="da9d3-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="da9d3-272">이 샘플은 SQL Server 테이블에서 Azure Blob로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="da9d3-273">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="da9d3-274">첫 번째 단계로 데이터 관리 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="da9d3-275">해당 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="da9d3-276">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="da9d3-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="da9d3-277">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="da9d3-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="da9d3-278">**SQL Server 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="da9d3-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="da9d3-279">샘플은 Azure SQL에서 만든 "MyTable" 테이블에 시계열 데이터에 대한 "timestampcolumn"이라는 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="da9d3-280">단일 데이터 집합을 사용하여 동일한 데이터베이스 내 여러 테이블에 대해 쿼리를 실행할 수 있지만, 데이터 집합의 tableName typeProperty에 대해서는 단일 테이블이 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="da9d3-281">"external": "true"를 설정하면 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="da9d3-282">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="da9d3-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="da9d3-283">데이터는 매시간 새 blob에 기록됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="da9d3-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="da9d3-284">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="da9d3-285">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="da9d3-286">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="da9d3-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="da9d3-287">파이프라인은 이러한 입력 및 출력 데이터 집합을 사용하도록 구성되며 매시간 실행되도록 예약되는 복사 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="da9d3-288">파이프라인 JSON 정의에서 **source** 형식은 **SqlSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="da9d3-289">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 과거 한 시간에서 복사할 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="da9d3-290">위의 예에서는 SqlSource에 대해 **sqlReaderQuery** 가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="da9d3-291">복사 작업은 데이터를 가져오는 SQL Server 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="da9d3-292">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="da9d3-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="da9d3-293">sqlReaderQuery는 입력 데이터 집합에서 참조하는 데이터베이스 내의 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="da9d3-294">즉, 데이터 집합의 tableName typeProperty로 설정된 테이블만 참조하도록 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="da9d3-295">sqlReaderQuery 또는 sqlReaderStoredProcedureName을 지정하지 않으면 structure 섹션에 정의된 열을 사용하여 SQL Server Database에 대해 실행할 선택 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="da9d3-296">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="da9d3-297">SqlSource 및 BlobSink에서 지원하는 속성 목록은 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="da9d3-298">예: Azure Blob에서 SQL Server로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="da9d3-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="da9d3-299">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-299">The following sample shows:</span></span>

1. <span data-ttu-id="da9d3-300">[OnPremisesSqlServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="da9d3-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="da9d3-301">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="da9d3-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="da9d3-302">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="da9d3-303">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="da9d3-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="da9d3-304">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#sql-server-copy-activity-type-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="da9d3-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="da9d3-305">이 샘플은 Azure Blob에서 SQL Server 테이블로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="da9d3-306">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="da9d3-307">**SQL Server 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="da9d3-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="da9d3-308">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="da9d3-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="da9d3-309">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="da9d3-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="da9d3-310">데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="da9d3-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="da9d3-311">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="da9d3-312">폴더 경로에는 시작 시간의 년/월/일 부분이 사용되고 파일 이름에는 시작 시간의 시간 부분이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="da9d3-313">"external": "true" 설정을 사용하는 경우 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 정보가 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="da9d3-314">**SQL Server 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="da9d3-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="da9d3-315">샘플은 SQL Server의 "MyTable"이라는 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="da9d3-316">Blob CSV 파일에 포함될 것으로 예상되는 것과 같은 수의 열을 사용하여 SQL Server에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="da9d3-317">새 행은 매시간 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-317">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="da9d3-318">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="da9d3-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="da9d3-319">파이프라인은 이러한 입력 및 출력 데이터 집합을 사용하도록 구성되며 매시간 실행되도록 예약되는 복사 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="da9d3-320">파이프라인 JSON 정의에서 **원본** 형식은 **BlobSource**로 설정되고 **싱크** 형식은 **SqlSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="da9d3-321">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="da9d3-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="da9d3-322">원격 연결을 허용하도록 SQL Server를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="da9d3-323">**SQL Server Management Studio**를 시작하고 **서버**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="da9d3-324">목록에서 **연결**을 선택하고 **서버에 대한 원격 연결 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![원격 연결 사용](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="da9d3-326">자세한 단계를 보려면 [원격 액세스 서버 구성 옵션 구성](https://msdn.microsoft.com/library/ms191464.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="da9d3-327">**SQL Server 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="da9d3-328">사용하려는 인스턴스에 대한 **SQL Server 네트워크 구성**을 확장하고 **MSSQLSERVER용 프로토콜**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="da9d3-329">오른쪽 창에 프로토콜이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="da9d3-330">**TCP/IP**를 마우스 오른쪽 단추로 클릭하고 **사용**을 클릭하여 TCP/IP를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP 사용](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="da9d3-332">TCP/IP 프로토콜을 사용하는 다른 방법 및 자세한 내용은 [서버 네트워크 프로토콜 사용 또는 사용 안 함](https://msdn.microsoft.com/library/ms191294.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="da9d3-333">같은 창에서 **TCP/IP**를 두 번 클릭하여 **TCP/IP 속성** 창을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="da9d3-334">**IP 주소** 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="da9d3-335">아래로 스크롤하여 **IPAll** 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="da9d3-336">**TCP 포트**(기본값은 **1433**)를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="da9d3-337">컴퓨터에 **Windows 방화벽에 대한 규칙** 을 만들어 이 포트를 통해 들어오는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="da9d3-338">**연결 확인**: 정규화된 이름을 사용하여 SQL Server에 연결하려면 다른 컴퓨터의 SQL Server Management Studio를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="da9d3-339">예: "<machine><domain>.corp<company>.com,1433".</span><span class="sxs-lookup"><span data-stu-id="da9d3-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="da9d3-340">자세한 내용은 [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="da9d3-341">연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="da9d3-342">대상 데이터베이스의 ID 열</span><span class="sxs-lookup"><span data-stu-id="da9d3-342">Identity columns in the target database</span></span>
<span data-ttu-id="da9d3-343">이 섹션에서는 ID 열이 없는 소스 테이블에서 ID 열이 있는 대상 테이블로 데이터를 복사하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="da9d3-344">**원본 테이블:**</span><span class="sxs-lookup"><span data-stu-id="da9d3-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="da9d3-345">**대상 테이블:**</span><span class="sxs-lookup"><span data-stu-id="da9d3-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="da9d3-346">대상 테이블에 ID 열이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="da9d3-347">**원본 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="da9d3-347">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="da9d3-348">**대상 데이터 집합 JSON 정의**</span><span class="sxs-lookup"><span data-stu-id="da9d3-348">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="da9d3-349">원본 테이블과 대상 테이블의 스키마가 서로 다릅니다(대상에 ID가 포함된 추가 열이 있음).</span><span class="sxs-lookup"><span data-stu-id="da9d3-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="da9d3-350">이 시나리오에서는 ID 열을 포함하지 않는 대상 데이터 집합 정의에서 **structure** 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="da9d3-351">SQL 싱크에서 저장된 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="da9d3-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="da9d3-352">파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="da9d3-353">SQL 서버에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="da9d3-353">Type mapping for SQL server</span></span>
<span data-ttu-id="da9d3-354">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 설명한 것처럼, 복사 활동은 다음과 같은 2단계 방식을 사용해 소스 형식에서 싱크 형식으로 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="da9d3-355">네이티브 원본 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="da9d3-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="da9d3-356">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="da9d3-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="da9d3-357">SQL 서버 간에 데이터를 이동할 때는 SQL 형식에서 .NET 형식으로 또는 그 반대로 다음과 같은 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="da9d3-358">매핑은 ADO.NET에 대한 SQL Server 데이터 형식 매핑과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="da9d3-359">SQL Server 데이터베이스 엔진 형식</span><span class="sxs-lookup"><span data-stu-id="da9d3-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="da9d3-360">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="da9d3-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="da9d3-361">bigint</span><span class="sxs-lookup"><span data-stu-id="da9d3-361">bigint</span></span> |<span data-ttu-id="da9d3-362">Int64</span><span class="sxs-lookup"><span data-stu-id="da9d3-362">Int64</span></span> |
| <span data-ttu-id="da9d3-363">binary</span><span class="sxs-lookup"><span data-stu-id="da9d3-363">binary</span></span> |<span data-ttu-id="da9d3-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-364">Byte[]</span></span> |
| <span data-ttu-id="da9d3-365">bit</span><span class="sxs-lookup"><span data-stu-id="da9d3-365">bit</span></span> |<span data-ttu-id="da9d3-366">Boolean</span><span class="sxs-lookup"><span data-stu-id="da9d3-366">Boolean</span></span> |
| <span data-ttu-id="da9d3-367">char</span><span class="sxs-lookup"><span data-stu-id="da9d3-367">char</span></span> |<span data-ttu-id="da9d3-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-368">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-369">date</span><span class="sxs-lookup"><span data-stu-id="da9d3-369">date</span></span> |<span data-ttu-id="da9d3-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="da9d3-370">DateTime</span></span> |
| <span data-ttu-id="da9d3-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="da9d3-371">Datetime</span></span> |<span data-ttu-id="da9d3-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="da9d3-372">DateTime</span></span> |
| <span data-ttu-id="da9d3-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="da9d3-373">datetime2</span></span> |<span data-ttu-id="da9d3-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="da9d3-374">DateTime</span></span> |
| <span data-ttu-id="da9d3-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da9d3-375">Datetimeoffset</span></span> |<span data-ttu-id="da9d3-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="da9d3-376">DateTimeOffset</span></span> |
| <span data-ttu-id="da9d3-377">10진수</span><span class="sxs-lookup"><span data-stu-id="da9d3-377">Decimal</span></span> |<span data-ttu-id="da9d3-378">10진수</span><span class="sxs-lookup"><span data-stu-id="da9d3-378">Decimal</span></span> |
| <span data-ttu-id="da9d3-379">FILESTREAM 특성(varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="da9d3-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="da9d3-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-380">Byte[]</span></span> |
| <span data-ttu-id="da9d3-381">Float</span><span class="sxs-lookup"><span data-stu-id="da9d3-381">Float</span></span> |<span data-ttu-id="da9d3-382">Double</span><span class="sxs-lookup"><span data-stu-id="da9d3-382">Double</span></span> |
| <span data-ttu-id="da9d3-383">이미지</span><span class="sxs-lookup"><span data-stu-id="da9d3-383">image</span></span> |<span data-ttu-id="da9d3-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-384">Byte[]</span></span> |
| <span data-ttu-id="da9d3-385">int</span><span class="sxs-lookup"><span data-stu-id="da9d3-385">int</span></span> |<span data-ttu-id="da9d3-386">Int32</span><span class="sxs-lookup"><span data-stu-id="da9d3-386">Int32</span></span> |
| <span data-ttu-id="da9d3-387">money</span><span class="sxs-lookup"><span data-stu-id="da9d3-387">money</span></span> |<span data-ttu-id="da9d3-388">10진수</span><span class="sxs-lookup"><span data-stu-id="da9d3-388">Decimal</span></span> |
| <span data-ttu-id="da9d3-389">nchar</span><span class="sxs-lookup"><span data-stu-id="da9d3-389">nchar</span></span> |<span data-ttu-id="da9d3-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-390">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-391">ntext</span><span class="sxs-lookup"><span data-stu-id="da9d3-391">ntext</span></span> |<span data-ttu-id="da9d3-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-392">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-393">numeric</span><span class="sxs-lookup"><span data-stu-id="da9d3-393">numeric</span></span> |<span data-ttu-id="da9d3-394">10진수</span><span class="sxs-lookup"><span data-stu-id="da9d3-394">Decimal</span></span> |
| <span data-ttu-id="da9d3-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="da9d3-395">nvarchar</span></span> |<span data-ttu-id="da9d3-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-396">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-397">real</span><span class="sxs-lookup"><span data-stu-id="da9d3-397">real</span></span> |<span data-ttu-id="da9d3-398">단일</span><span class="sxs-lookup"><span data-stu-id="da9d3-398">Single</span></span> |
| <span data-ttu-id="da9d3-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="da9d3-399">rowversion</span></span> |<span data-ttu-id="da9d3-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-400">Byte[]</span></span> |
| <span data-ttu-id="da9d3-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="da9d3-401">smalldatetime</span></span> |<span data-ttu-id="da9d3-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="da9d3-402">DateTime</span></span> |
| <span data-ttu-id="da9d3-403">smallint</span><span class="sxs-lookup"><span data-stu-id="da9d3-403">smallint</span></span> |<span data-ttu-id="da9d3-404">Int16</span><span class="sxs-lookup"><span data-stu-id="da9d3-404">Int16</span></span> |
| <span data-ttu-id="da9d3-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="da9d3-405">smallmoney</span></span> |<span data-ttu-id="da9d3-406">10진수</span><span class="sxs-lookup"><span data-stu-id="da9d3-406">Decimal</span></span> |
| <span data-ttu-id="da9d3-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="da9d3-407">sql_variant</span></span> |<span data-ttu-id="da9d3-408">개체 *</span><span class="sxs-lookup"><span data-stu-id="da9d3-408">Object *</span></span> |
| <span data-ttu-id="da9d3-409">텍스트</span><span class="sxs-lookup"><span data-stu-id="da9d3-409">text</span></span> |<span data-ttu-id="da9d3-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-410">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-411">실시간</span><span class="sxs-lookup"><span data-stu-id="da9d3-411">time</span></span> |<span data-ttu-id="da9d3-412">timespan</span><span class="sxs-lookup"><span data-stu-id="da9d3-412">TimeSpan</span></span> |
| <span data-ttu-id="da9d3-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="da9d3-413">timestamp</span></span> |<span data-ttu-id="da9d3-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-414">Byte[]</span></span> |
| <span data-ttu-id="da9d3-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="da9d3-415">tinyint</span></span> |<span data-ttu-id="da9d3-416">Byte</span><span class="sxs-lookup"><span data-stu-id="da9d3-416">Byte</span></span> |
| <span data-ttu-id="da9d3-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="da9d3-417">uniqueidentifier</span></span> |<span data-ttu-id="da9d3-418">Guid</span><span class="sxs-lookup"><span data-stu-id="da9d3-418">Guid</span></span> |
| <span data-ttu-id="da9d3-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="da9d3-419">varbinary</span></span> |<span data-ttu-id="da9d3-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-420">Byte[]</span></span> |
| <span data-ttu-id="da9d3-421">varchar</span><span class="sxs-lookup"><span data-stu-id="da9d3-421">varchar</span></span> |<span data-ttu-id="da9d3-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="da9d3-422">String, Char[]</span></span> |
| <span data-ttu-id="da9d3-423">xml</span><span class="sxs-lookup"><span data-stu-id="da9d3-423">xml</span></span> |<span data-ttu-id="da9d3-424">xml</span><span class="sxs-lookup"><span data-stu-id="da9d3-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="da9d3-425">원본을 싱크 열로 매핑</span><span class="sxs-lookup"><span data-stu-id="da9d3-425">Mapping source to sink columns</span></span>
<span data-ttu-id="da9d3-426">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="da9d3-427">반복 가능한 복사</span><span class="sxs-lookup"><span data-stu-id="da9d3-427">Repeatable copy</span></span>
<span data-ttu-id="da9d3-428">SQL Server 데이터베이스로 데이터를 복사할 때 복사 작업은 기본적으로 싱크 테이블에 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="da9d3-429">그 대신 UPSERT를 수행하려면 [SqlSink에 반복 가능한 쓰기](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="da9d3-430">관계형 데이터 저장소에서 데이터를 복사할 때는 의도치 않는 결과를 방지하기 위해 반복성을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="da9d3-431">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="da9d3-432">또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="da9d3-433">어느 쪽이든 조각이 재실행되는 경우 조각이 실행되는 횟수에 관계없이 같은 데이터를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9d3-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="da9d3-434">[관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="da9d3-435">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="da9d3-435">Performance and Tuning</span></span>
<span data-ttu-id="da9d3-436">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da9d3-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
