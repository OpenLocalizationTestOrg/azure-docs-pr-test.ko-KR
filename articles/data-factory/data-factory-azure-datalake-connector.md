---
title: "Azure Data Lake 저장소 간 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Data Lake Store 간 데이터를 복사하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="dac73-103">Data Factory를 사용하여 Data Lake Store 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="dac73-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="dac73-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure Data Lake Store 간에 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="dac73-105">이 문서는 복사 작업을 사용한 데이터 이동의 개요를 보여 주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="dac73-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="dac73-106">Supported scenarios</span></span>
<span data-ttu-id="dac73-107">**Azure Data Lake Store에서** 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="dac73-108">다음 데이터 저장소에서 **Azure Data Lake Store로** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="dac73-109">복사 작업을 사용하여 파이프라인을 만들기 전에 Data Lake Store 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="dac73-110">자세한 내용은 [Azure Data Lake Store 시작](../data-lake-store/data-lake-store-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="dac73-111">지원되는 인증 형식</span><span class="sxs-lookup"><span data-stu-id="dac73-111">Supported authentication types</span></span>
<span data-ttu-id="dac73-112">Data Lake Store 커넥터는 다음 인증 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="dac73-113">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="dac73-113">Service principal authentication</span></span>
* <span data-ttu-id="dac73-114">사용자 자격 증명(OAuth) 인증</span><span class="sxs-lookup"><span data-stu-id="dac73-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="dac73-115">특히 예약된 데이터 복사의 경우 서비스 주체 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="dac73-116">사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="dac73-117">구성 세부 정보에서 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="dac73-118">시작</span><span class="sxs-lookup"><span data-stu-id="dac73-118">Get started</span></span>
<span data-ttu-id="dac73-119">다른 도구/API를 사용하여 Azure Data Lake Store 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="dac73-120">데이터를 복사하기 위한 파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="dac73-121">복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 자습서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="dac73-122">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dac73-123">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="dac73-124">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="dac73-125">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-125">Create a **data factory**.</span></span> <span data-ttu-id="dac73-126">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="dac73-127">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="dac73-128">예를 들어 Azure Blob Storage에서 Azure Data Lake Store로 데이터를 복사하는 경우 Azure Storage 계정 및 Azure Data Lake Store를 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="dac73-129">Azure Data Lake Store와 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="dac73-130">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="dac73-131">마지막 단계에서 설명한 예제에서는 입력 데이터가 포함된 BLOB 컨테이너 및 폴더를 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="dac73-132">그리고 Blob Storage에서 복사한 데이터를 포함하는 Data Lake Store의 폴더 및 파일 경로를 지정하는 또 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="dac73-133">Azure Data Lake Store와 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="dac73-134">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="dac73-135">앞에서 언급한 예제에서는 BlobSource를 원본으로, AzureDataLakeStoreSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="dac73-136">마찬가지로 Azure Data Lake Store에서 Azure Blob Storage로 복사하는 경우 복사 작업에서 AzureDataLakeStoreSource 및 BlobSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="dac73-137">Azure Data Lake Store와 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="dac73-138">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="dac73-139">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="dac73-140">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="dac73-141">다른 곳에서 Azure Data Lake Store로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-data-lake-store) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="dac73-142">다음 섹션에서는 Data Lake Store에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="dac73-143">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="dac73-143">Linked service properties</span></span>
<span data-ttu-id="dac73-144">연결된 서비스는 데이터 저장소를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="dac73-145">Data Lake Store 데이터를 데이터 팩터리에 연결하는 **AzureDataLakeStore** 형식의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="dac73-146">다음 표에서는 Data Lake Store 연결된 서비스와 관련된 JSON 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="dac73-147">서비스 주체와 사용자 자격 증명 인증 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="dac73-148">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-148">Property</span></span> | <span data-ttu-id="dac73-149">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-149">Description</span></span> | <span data-ttu-id="dac73-150">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dac73-151">**type**</span><span class="sxs-lookup"><span data-stu-id="dac73-151">**type**</span></span> | <span data-ttu-id="dac73-152">type 속성은 **AzureDataLakeStore**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="dac73-153">예</span><span class="sxs-lookup"><span data-stu-id="dac73-153">Yes</span></span> |
| <span data-ttu-id="dac73-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="dac73-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="dac73-155">Azure Data Lake Store 계정에 대한 정보.</span><span class="sxs-lookup"><span data-stu-id="dac73-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="dac73-156">이 정보는 `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/` 형식 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="dac73-157">예</span><span class="sxs-lookup"><span data-stu-id="dac73-157">Yes</span></span> |
| <span data-ttu-id="dac73-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="dac73-158">**subscriptionId**</span></span> | <span data-ttu-id="dac73-159">Data Lake Store 계정이 속하는 Azure 구독 ID.</span><span class="sxs-lookup"><span data-stu-id="dac73-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="dac73-160">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="dac73-160">Required for sink</span></span> |
| <span data-ttu-id="dac73-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="dac73-161">**resourceGroupName**</span></span> | <span data-ttu-id="dac73-162">Data Lake Store 계정이 속하는 Azure 리소스 그룹 이름.</span><span class="sxs-lookup"><span data-stu-id="dac73-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="dac73-163">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="dac73-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="dac73-164">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="dac73-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="dac73-165">서비스 주체 인증을 사용하려면 Azure AD(Azure Active Directory)에서 응용 프로그램 엔터티를 등록한 후 Data Lake Store에서 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="dac73-166">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="dac73-167">연결된 서비스를 정의하는 데 사용되므로 다음 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="dac73-168">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="dac73-168">Application ID</span></span>
* <span data-ttu-id="dac73-169">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="dac73-169">Application key</span></span> 
* <span data-ttu-id="dac73-170">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="dac73-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dac73-171">복사 마법사를 사용하여 데이터 파이프라인을 작성하는 경우 Data Lake Store 계정에 대한 액세스 제어(IID 및 액세스 관리)의 **읽기 권한자** 역할 이상을 서비스 주체를 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="dac73-172">또한 서비스 주체에 Data Lake Store 루트("/") 및 그 하위 항목에 대한 **읽기+실행** 권한 이상을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="dac73-173">그렇지 않으면 "제공된 자격 증명이 유효하지 않습니다." 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="dac73-174">Azure AD에서 서비스 주체를 만들거나 업데이트한 후 변경 내용이 적용되는 데 몇 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="dac73-175">서비스 주체 및 Data Lake Store ACL(액세스 제어 목록) 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="dac73-176">"제공된 자격 증명이 잘못되었습니다."라는 메시지가 계속 표시되면 잠시 기다린 후 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="dac73-177">다음 속성을 지정하여 서비스 주체 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="dac73-178">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-178">Property</span></span> | <span data-ttu-id="dac73-179">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-179">Description</span></span> | <span data-ttu-id="dac73-180">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dac73-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="dac73-181">**servicePrincipalId**</span></span> | <span data-ttu-id="dac73-182">응용 프로그램의 클라이언트 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-182">Specify the application's client ID.</span></span> | <span data-ttu-id="dac73-183">예</span><span class="sxs-lookup"><span data-stu-id="dac73-183">Yes</span></span> |
| <span data-ttu-id="dac73-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="dac73-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="dac73-185">응용 프로그램의 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-185">Specify the application's key.</span></span> | <span data-ttu-id="dac73-186">예</span><span class="sxs-lookup"><span data-stu-id="dac73-186">Yes</span></span> |
| <span data-ttu-id="dac73-187">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="dac73-187">**tenant**</span></span> | <span data-ttu-id="dac73-188">응용 프로그램이 있는 테넌트 정보(도메인 이름 또는 테넌트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="dac73-189">Azure Portal의 오른쪽 위 모서리에 마우스를 이동하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="dac73-190">예</span><span class="sxs-lookup"><span data-stu-id="dac73-190">Yes</span></span> |

<span data-ttu-id="dac73-191">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="dac73-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="dac73-192">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="dac73-192">User credential authentication</span></span>
<span data-ttu-id="dac73-193">또는 아래 속성을 지정하여 사용자 자격 증명 인증을 사용하여 Data Lake Store로 데이터를 복사하거나 Data Lake Store에서 다른 위치로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="dac73-194">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-194">Property</span></span> | <span data-ttu-id="dac73-195">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-195">Description</span></span> | <span data-ttu-id="dac73-196">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dac73-197">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="dac73-197">**authorization**</span></span> | <span data-ttu-id="dac73-198">Data Factory 편집기에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 자동 생성된 authorization URL이 이 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="dac73-199">예</span><span class="sxs-lookup"><span data-stu-id="dac73-199">Yes</span></span> |
| <span data-ttu-id="dac73-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="dac73-200">**sessionId**</span></span> | <span data-ttu-id="dac73-201">OAuth 권한 부여 세션에서 가져온 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="dac73-202">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="dac73-203">이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="dac73-204">예</span><span class="sxs-lookup"><span data-stu-id="dac73-204">Yes</span></span> |

<span data-ttu-id="dac73-205">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="dac73-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="dac73-206">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="dac73-206">Token expiration</span></span>
<span data-ttu-id="dac73-207">**권한 부여** 단추를 사용하여 생성한 권한 부여 코드는 특정 시간 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="dac73-208">다음과 같은 메시지는 인증 토큰이 만료되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="dac73-209">자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="dac73-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="dac73-210">"자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS70008: 제공된 액세스 권한 부여가 만료되었거나 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="dac73-211">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21-09-31Z</span><span class="sxs-lookup"><span data-stu-id="dac73-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="dac73-212">다음 표에는 다양한 유형의 사용자 계정에 대한 만료 시간이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="dac73-213">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="dac73-213">User type</span></span> | <span data-ttu-id="dac73-214">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="dac73-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="dac73-215">Azure Active Directory에서 관리되지 *않는* 사용자 계정(예: @hotmail.com 또는 @live.com)</span><span class="sxs-lookup"><span data-stu-id="dac73-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="dac73-216">12시간</span><span class="sxs-lookup"><span data-stu-id="dac73-216">12 hours</span></span> |
| <span data-ttu-id="dac73-217">Azure Active Directory에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="dac73-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="dac73-218">마지막 조각이 실행되고 14일 후</span><span class="sxs-lookup"><span data-stu-id="dac73-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="dac73-219">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="dac73-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="dac73-220">토큰 만료 시간 전에 암호를 변경하면, 토큰이 즉시 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="dac73-221">이 섹션에 나와 있는 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="dac73-222">토큰이 만료되면 **권한 부여** 단추를 사용하여 계정을 다시 인증하고 연결된 서비스를 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="dac73-223">다음 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **authorization** 속성의 값을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="dac73-224">코드에 사용되는 Data Factory 클래스에 대한 세부 정보는 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="dac73-225">코드에 사용되는 `WindowsFormsWebAuthenticationDialog` 클래스에 대해 `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll`의 버전 `2.9.10826.1824`에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="dac73-226">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="dac73-226">Dataset properties</span></span>
<span data-ttu-id="dac73-227">Data Lake Store에서 입력 데이터를 표시할 데이터 집합을 지정하려면 데이터 집합의 **type** 속성을 **AzureDataLakeStore**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="dac73-228">데이터 집합의 **linkedServiceName** 속성을 Data Lake Store 연결된 서비스의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="dac73-229">데이터 집합 정의에 사용할 수 있는 JSON 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dac73-230">**구조**, **가용성** 및 **정책**과 JSON의 데이터 집합 섹션은 모든 데이터 집합 형식(예: SQL Database, Azure Blob, Azure 테이블)에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="dac73-231">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치, 서식 등에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="dac73-232">**AzureDataLakeStore** 형식의 데이터 집합에 대한 **typeProperties** 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="dac73-233">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-233">Property</span></span> | <span data-ttu-id="dac73-234">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-234">Description</span></span> | <span data-ttu-id="dac73-235">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dac73-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="dac73-236">**folderPath**</span></span> |<span data-ttu-id="dac73-237">Data Lake Store의 컨테이너 및 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="dac73-238">예</span><span class="sxs-lookup"><span data-stu-id="dac73-238">Yes</span></span> |
| <span data-ttu-id="dac73-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="dac73-239">**fileName**</span></span> |<span data-ttu-id="dac73-240">Azure Data Lake Store에 있는 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="dac73-241">**fileName** 속성은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="dac73-242">**fileName**을 지정하는 경우 활동(복사 포함)은 특정 파일에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="dac73-243">**fileName**을 지정하지 않으면 복사는 입력 데이터 집합에 대한 **folderPath**에 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="dac73-244">**fileName**이 출력 데이터 집합에 대해 지정되지 않았고 **preserveHierarchy**가 활동 싱크에 지정되지 않은 경우 생성된 파일의 이름은 Data._Guid_.txt' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="dac73-245">예제: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="dac73-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="dac73-246">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-246">No</span></span> |
| <span data-ttu-id="dac73-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="dac73-247">**partitionedBy**</span></span> |<span data-ttu-id="dac73-248">**partitionedBy** 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="dac73-249">시계열 데이터에 대한 동적 경로 및 파일 이름을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="dac73-250">예를 들어 **folderPath**는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="dac73-251">자세한 내용과 예제는 [partitionedBy 속성](#using-partitionedby-property)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="dac73-252">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-252">No</span></span> |
| <span data-ttu-id="dac73-253">**format**</span><span class="sxs-lookup"><span data-stu-id="dac73-253">**format**</span></span> | <span data-ttu-id="dac73-254">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** 및 **ParquetFormat** 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="dac73-255">**format**의 **type** 속성을 이 값 중 하나로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="dac73-256">자세한 내용은 [Azure Data Factory에서 지원하는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서의 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="dac73-257">파일 기반 저장소(이진 복사) 간에 파일을 “있는 그대로” 복사하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 `format` 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="dac73-258">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-258">No</span></span> |
| <span data-ttu-id="dac73-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="dac73-259">**compression**</span></span> | <span data-ttu-id="dac73-260">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="dac73-261">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="dac73-262">**Optimal** 및 **Fastest** 수준이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="dac73-263">자세한 내용은 [Azure Data Factory에서 지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="dac73-264">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="dac73-265">partitionedBy 속성</span><span class="sxs-lookup"><span data-stu-id="dac73-265">The partitionedBy property</span></span>
<span data-ttu-id="dac73-266">**partitionedBy** 속성, Data Factory 함수 및 시스템 변수를 사용하여 시계열 데이터의 동적 **folderPath** 및 **fileName** 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="dac73-267">자세한 내용은 [Azure Data Factory - 함수 및 시스템 변수](data-factory-functions-variables.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="dac73-268">다음 예제에서 `{Slice}`는 Data Factory 시스템 변수인 `SliceStart`의 값(`yyyyMMddHH` 형식)으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="dac73-269">이름 `SliceStart`는 조각의 시작 시간을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="dac73-270">`folderPath` 속성은 `wikidatagateway/wikisampledataout/2014100103` 또는 `wikidatagateway/wikisampledataout/2014100104`과 같이 조각마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="dac73-271">다음 예제에서 `SliceStart`의 연도, 월, 일 및 시간은 `folderPath` 및 `fileName` 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="dac73-272">시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [Azure Data Factory의 데이터 집합](data-factory-create-datasets.md) 및 [Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="dac73-273">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="dac73-273">Copy activity properties</span></span>
<span data-ttu-id="dac73-274">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dac73-275">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="dac73-276">활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="dac73-277">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="dac73-278">**AzureDataLakeStoreSource**는 **typeProperties** 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="dac73-279">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-279">Property</span></span> | <span data-ttu-id="dac73-280">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-280">Description</span></span> | <span data-ttu-id="dac73-281">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="dac73-281">Allowed values</span></span> | <span data-ttu-id="dac73-282">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dac73-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="dac73-283">**recursive**</span></span> |<span data-ttu-id="dac73-284">하위 폴더 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="dac73-285">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="dac73-285">True (default value), False</span></span> |<span data-ttu-id="dac73-286">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-286">No</span></span> |


<span data-ttu-id="dac73-287">**AzureDataLakeStoreSink**는 **typeProperties** 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="dac73-288">속성</span><span class="sxs-lookup"><span data-stu-id="dac73-288">Property</span></span> | <span data-ttu-id="dac73-289">설명</span><span class="sxs-lookup"><span data-stu-id="dac73-289">Description</span></span> | <span data-ttu-id="dac73-290">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="dac73-290">Allowed values</span></span> | <span data-ttu-id="dac73-291">필수</span><span class="sxs-lookup"><span data-stu-id="dac73-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dac73-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="dac73-292">**copyBehavior**</span></span> |<span data-ttu-id="dac73-293">복사 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="dac73-294"><b>PreserveHierarchy</b>: 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="dac73-295">원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="dac73-296"><b>FlattenHierarchy:</b> 원본 폴더의 모든 파일이 대상 폴더의 첫 번째 수준에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="dac73-297">대상 파일은 자동 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="dac73-298"><b>MergeFiles</b>: 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="dac73-299">병합되는 파일 이름은 지정된 파일 또는 Blob 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="dac73-300">그렇지 않은 경우 파일 이름이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="dac73-301">아니요</span><span class="sxs-lookup"><span data-stu-id="dac73-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="dac73-302">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="dac73-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="dac73-303">이 섹션에서는 다양한 recursive 및 copyBehavior 값 조합에 대한 복사 작업의 결과 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="dac73-304">recursive</span><span class="sxs-lookup"><span data-stu-id="dac73-304">recursive</span></span> | <span data-ttu-id="dac73-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="dac73-305">copyBehavior</span></span> | <span data-ttu-id="dac73-306">결과 동작</span><span class="sxs-lookup"><span data-stu-id="dac73-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dac73-307">true</span><span class="sxs-lookup"><span data-stu-id="dac73-307">true</span></span> |<span data-ttu-id="dac73-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="dac73-308">preserveHierarchy</span></span> |<span data-ttu-id="dac73-309">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-310">Folder1</span></span><br/><span data-ttu-id="dac73-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-317">Folder1 대상 폴더가 다음과 같이 원본 폴더와 동일한 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="dac73-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-318">Folder1</span></span><br/><span data-ttu-id="dac73-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="dac73-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="dac73-325">true</span><span class="sxs-lookup"><span data-stu-id="dac73-325">true</span></span> |<span data-ttu-id="dac73-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="dac73-326">flattenHierarchy</span></span> |<span data-ttu-id="dac73-327">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-328">Folder1</span></span><br/><span data-ttu-id="dac73-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-335">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-336">Folder1</span></span><br/><span data-ttu-id="dac73-337">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="dac73-338">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="dac73-339">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="dac73-340">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="dac73-341">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="dac73-342">true</span><span class="sxs-lookup"><span data-stu-id="dac73-342">true</span></span> |<span data-ttu-id="dac73-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="dac73-343">mergeFiles</span></span> |<span data-ttu-id="dac73-344">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-345">Folder1</span></span><br/><span data-ttu-id="dac73-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-352">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-353">Folder1</span></span><br/><span data-ttu-id="dac73-354">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="dac73-355">false</span><span class="sxs-lookup"><span data-stu-id="dac73-355">false</span></span> |<span data-ttu-id="dac73-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="dac73-356">preserveHierarchy</span></span> |<span data-ttu-id="dac73-357">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="dac73-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-358">Folder1</span></span><br/><span data-ttu-id="dac73-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-365">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="dac73-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-366">Folder1</span></span><br/><span data-ttu-id="dac73-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="dac73-369">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="dac73-370">false</span><span class="sxs-lookup"><span data-stu-id="dac73-370">false</span></span> |<span data-ttu-id="dac73-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="dac73-371">flattenHierarchy</span></span> |<span data-ttu-id="dac73-372">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="dac73-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-373">Folder1</span></span><br/><span data-ttu-id="dac73-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-380">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="dac73-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-381">Folder1</span></span><br/><span data-ttu-id="dac73-382">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="dac73-383">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="dac73-384">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="dac73-385">false</span><span class="sxs-lookup"><span data-stu-id="dac73-385">false</span></span> |<span data-ttu-id="dac73-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="dac73-386">mergeFiles</span></span> |<span data-ttu-id="dac73-387">다음 구조를 가진 원본 폴더 Folder1의 경우: </span><span class="sxs-lookup"><span data-stu-id="dac73-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="dac73-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-388">Folder1</span></span><br/><span data-ttu-id="dac73-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="dac73-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dac73-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="dac73-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dac73-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="dac73-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dac73-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="dac73-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dac73-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="dac73-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dac73-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="dac73-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dac73-395">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="dac73-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="dac73-396">Folder1</span></span><br/><span data-ttu-id="dac73-397">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="dac73-398">File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="dac73-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="dac73-399">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="dac73-400">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="dac73-400">Supported file and compression formats</span></span>
<span data-ttu-id="dac73-401">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="dac73-402">Data Lake Store로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="dac73-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="dac73-403">다음 예제에서는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="dac73-404">이러한 샘플 정의를 사용하여 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)에서 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dac73-405">이 예제에서는 Data Lake Store 및 Azure Blob Storage 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="dac73-406">그러나 임의의 원본에서 지원되는 싱크로 _직접_ 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="dac73-407">자세한 내용은 [복사 작업을 사용하여 데이터 이동](data-factory-data-movement-activities.md) 문서에서 "지원되는 데이터 저장소 및 형식" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="dac73-408">예제: Azure Blob Storage에서 Azure Data Lake Store로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="dac73-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="dac73-409">이 섹션의 예제 코드는 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-409">The example code in this section shows:</span></span>

* <span data-ttu-id="dac73-410">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="dac73-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="dac73-411">[AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="dac73-412">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="dac73-413">[AzureDataLakeStore](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="dac73-414">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureDataLakeStoreSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="dac73-415">이 예제에서는 Azure Blob Storage에서 Data Lake Store로 매시간 시계열 데이터가 복사되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="dac73-416">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="dac73-416">**Azure Storage linked service**</span></span>

```JSON
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

<span data-ttu-id="dac73-417">**Azure Data Lake Store 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="dac73-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="dac73-418">구성 세부 정보에서 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="dac73-419">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="dac73-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="dac73-420">다음 예제에서 매시간 새 Blob에서 데이터가 선택됩니다(`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="dac73-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="dac73-421">Blob에 대한 폴더 경로 및 파일 이름은 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="dac73-422">폴더 경로는 시작 시간의 년, 월 및 일 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="dac73-423">파일 이름은 시작 시간의 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="dac73-424">`"external": true` 설정은 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="dac73-425">**Azure Data Lake Store 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="dac73-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="dac73-426">다음 예제에서는 Data Lake Store로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="dac73-427">새 데이터가 Data Lake Store로 매시간 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-427">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="dac73-428">**Blob 원본 및 Data Lake Store 싱크를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="dac73-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="dac73-429">다음 예제에서 파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="dac73-430">복사 작업은 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="dac73-431">파이프라인 JSON 정의에서 `source` 형식은 `BlobSource`로, `sink` 형식은 `AzureDataLakeStoreSink`로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="dac73-432">예제: Azure Data Lake Store에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="dac73-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="dac73-433">이 섹션의 예제 코드는 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-433">The example code in this section shows:</span></span>

* <span data-ttu-id="dac73-434">[AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="dac73-435">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="dac73-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="dac73-436">[AzureDataLakeStore](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="dac73-437">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="dac73-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="dac73-438">[AzureDataLakeStoreSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dac73-439">이 코드는 Data Lake Store에서 Azure Blob로 매시간 시계열 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="dac73-440">**Azure Data Lake Store 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="dac73-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="dac73-441">구성 세부 정보에서 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="dac73-442">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="dac73-442">**Azure Storage linked service**</span></span>

```JSON
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
<span data-ttu-id="dac73-443">**Azure Data Lake 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="dac73-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="dac73-444">이 예제에서 `"external"`을 `true`로 설정하면 테이블이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="dac73-445">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="dac73-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="dac73-446">다음 예제에서 데이터는 매시간 새 Blob에 기록됩니다(`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="dac73-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="dac73-447">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="dac73-448">폴더 경로는 시작 시간의 년, 월, 일 및 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
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

<span data-ttu-id="dac73-449">**Azure Data Lake Store 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="dac73-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="dac73-450">다음 예제에서 파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="dac73-451">복사 작업은 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="dac73-452">파이프라인 JSON 정의에서 `source` 형식은 `AzureDataLakeStoreSource`로, `sink` 형식은 `BlobSink`로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="dac73-453">복사 작업 정의에서 원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac73-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="dac73-454">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dac73-455">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="dac73-455">Performance and tuning</span></span>
<span data-ttu-id="dac73-456">복사 작업 성능에 영향을 주는 요소 및 최적화하는 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dac73-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
