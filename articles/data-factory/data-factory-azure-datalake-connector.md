---
title: "Azure 데이터 레이크 저장소에서 데이터 tooand aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 toocopy 데이터 tooand 데이터 레이크 저장소에서 Azure 데이터 팩터리를 사용 하 여"
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
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="5ef94-103">데이터 팩터리를 사용 하 여 데이터 tooand 데이터 레이크 저장소에서 복사</span><span class="sxs-lookup"><span data-stu-id="5ef94-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="5ef94-104">이 문서에서는 설명 방법에서 Azure 데이터 레이크 저장소에서 Azure Data Factory toomove 데이터 tooand toouse 복사 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="5ef94-105">Hello에 기반 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서 복사 작업으로 데이터 이동에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="5ef94-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="5ef94-106">Supported scenarios</span></span>
<span data-ttu-id="5ef94-107">데이터를 복사할 수 **Azure 데이터 레이크 저장소에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="5ef94-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="5ef94-108">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure 데이터 레이크 저장소**:</span><span class="sxs-lookup"><span data-stu-id="5ef94-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="5ef94-109">복사 작업을 사용하여 파이프라인을 만들기 전에 Data Lake Store 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="5ef94-110">자세한 내용은 [Azure Data Lake Store 시작](../data-lake-store/data-lake-store-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef94-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="5ef94-111">지원되는 인증 형식</span><span class="sxs-lookup"><span data-stu-id="5ef94-111">Supported authentication types</span></span>
<span data-ttu-id="5ef94-112">데이터 레이크 저장소 커넥터 hello 이러한 인증 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="5ef94-113">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="5ef94-113">Service principal authentication</span></span>
* <span data-ttu-id="5ef94-114">사용자 자격 증명(OAuth) 인증</span><span class="sxs-lookup"><span data-stu-id="5ef94-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="5ef94-115">특히 예약된 데이터 복사의 경우 서비스 주체 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="5ef94-116">사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="5ef94-117">구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="5ef94-118">시작</span><span class="sxs-lookup"><span data-stu-id="5ef94-118">Get started</span></span>
<span data-ttu-id="5ef94-119">다른 도구/API를 사용하여 Azure Data Lake Store 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="5ef94-120">hello 가장 쉬운 방법은 toocreate 파이프라인 toocopy 데이터는 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5ef94-121">Hello 복사 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 자습서를 참조 하십시오. [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5ef94-122">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5ef94-123">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="5ef94-124">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5ef94-125">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-125">Create a **data factory**.</span></span> <span data-ttu-id="5ef94-126">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="5ef94-127">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="5ef94-128">예를 들어 Azure blob 저장소 tooan Azure 데이터 레이크 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure 데이터 레이크 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="5ef94-129">데이터 레이크 저장소 특정 tooAzure 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="5ef94-130">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="5ef94-131">Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="5ef94-132">고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello 데이터 레이크 저장소의 다른 데이터 집합 toospecify hello 폴더 및 파일 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="5ef94-133">특정 tooAzure 데이터 레이크 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="5ef94-134">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="5ef94-135">앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 AzureDataLakeStoreSink 싱크도 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="5ef94-136">마찬가지로, Azure 데이터 레이크 저장소 tooAzure Blob 저장소에서에서 복사 하는 경우 AzureDataLakeStoreSource 및 사용 BlobSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="5ef94-137">복사 활동 속성을 특정 tooAzure 데이터 레이크 저장소를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="5ef94-138">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="5ef94-139">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5ef94-140">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5ef94-141">샘플은 Azure 데이터 레이크 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-data-lake-store) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="5ef94-142">다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooData Lake 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5ef94-143">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-143">Linked service properties</span></span>
<span data-ttu-id="5ef94-144">연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="5ef94-145">형식의 연결 된 서비스를 만들면 **AzureDataLakeStore** toolink 데이터 레이크 저장소 데이터 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="5ef94-146">다음 표에서 hello JSON 요소 특정 tooData Lake 저장소 연결 된 서비스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="5ef94-147">서비스 주체와 사용자 자격 증명 인증 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="5ef94-148">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-148">Property</span></span> | <span data-ttu-id="5ef94-149">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-149">Description</span></span> | <span data-ttu-id="5ef94-150">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5ef94-151">**type**</span><span class="sxs-lookup"><span data-stu-id="5ef94-151">**type**</span></span> | <span data-ttu-id="5ef94-152">너무 hello 유형 속성을 설정 해야**AzureDataLakeStore**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="5ef94-153">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-153">Yes</span></span> |
| <span data-ttu-id="5ef94-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="5ef94-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="5ef94-155">Hello Azure 데이터 레이크 저장소 계정에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="5ef94-156">이 정보는 hello 다음 형식 중 하나: `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="5ef94-157">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-157">Yes</span></span> |
| <span data-ttu-id="5ef94-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="5ef94-158">**subscriptionId**</span></span> | <span data-ttu-id="5ef94-159">Azure 구독 ID toowhich hello Data Lake 저장소 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="5ef94-160">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="5ef94-160">Required for sink</span></span> |
| <span data-ttu-id="5ef94-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="5ef94-161">**resourceGroupName**</span></span> | <span data-ttu-id="5ef94-162">Azure 리소스 그룹 이름 toowhich hello Data Lake 저장소 계정에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="5ef94-163">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="5ef94-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="5ef94-164">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="5ef94-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="5ef94-165">toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="5ef94-166">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef94-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="5ef94-167">사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:</span><span class="sxs-lookup"><span data-stu-id="5ef94-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="5ef94-168">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="5ef94-168">Application ID</span></span>
* <span data-ttu-id="5ef94-169">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="5ef94-169">Application key</span></span> 
* <span data-ttu-id="5ef94-170">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="5ef94-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ef94-171">Hello 복사 마법사 tooauthor 데이터 파이프라인을 사용 하는 경우 hello 서비스 보안 주체에 부여 했는지 확인 적어도 **판독기** hello Data Lake 저장소 계정에 대 한 액세스 제어 (id 및 액세스 관리)에 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="5ef94-172">또한, 적어도 hello 서비스 사용자 권한을 부여 **읽기 + Execute** 권한 tooyour 데이터 레이크 저장소 루트 ("/") 및 해당 하위 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="5ef94-173">그렇지 않으면 "hello 지정한 자격 증명에 사용할 수 없습니다." hello 메시지를 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="5ef94-174">만들거나 Azure AD에서 서비스 사용자를 업데이트 한 후 hello 변경 tootake 효과 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="5ef94-175">Hello 서비스 사용자와 데이터 레이크 저장소 액세스 제어 목록 (ACL) 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5ef94-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="5ef94-176">"Hello 지정한 자격 증명에 사용할 수 없습니다" hello 메시지를 계속 나타나면 잠시 기다린 후 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5ef94-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="5ef94-177">Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="5ef94-178">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-178">Property</span></span> | <span data-ttu-id="5ef94-179">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-179">Description</span></span> | <span data-ttu-id="5ef94-180">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5ef94-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="5ef94-181">**servicePrincipalId**</span></span> | <span data-ttu-id="5ef94-182">Hello 응용 프로그램의 클라이언트 ID를 지정</span><span class="sxs-lookup"><span data-stu-id="5ef94-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="5ef94-183">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-183">Yes</span></span> |
| <span data-ttu-id="5ef94-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="5ef94-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="5ef94-185">Hello 응용 프로그램의 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-185">Specify hello application's key.</span></span> | <span data-ttu-id="5ef94-186">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-186">Yes</span></span> |
| <span data-ttu-id="5ef94-187">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="5ef94-187">**tenant**</span></span> | <span data-ttu-id="5ef94-188">응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="5ef94-189">Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="5ef94-190">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-190">Yes</span></span> |

<span data-ttu-id="5ef94-191">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="5ef94-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="5ef94-192">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="5ef94-192">User credential authentication</span></span>
<span data-ttu-id="5ef94-193">또는 hello 다음과 같은 속성을 지정 하 여 사용자 자격 증명 인증 toocopy에서 또는 tooData Lake 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="5ef94-194">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-194">Property</span></span> | <span data-ttu-id="5ef94-195">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-195">Description</span></span> | <span data-ttu-id="5ef94-196">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5ef94-197">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="5ef94-197">**authorization**</span></span> | <span data-ttu-id="5ef94-198">Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="5ef94-199">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-199">Yes</span></span> |
| <span data-ttu-id="5ef94-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="5ef94-200">**sessionId**</span></span> | <span data-ttu-id="5ef94-201">Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="5ef94-202">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="5ef94-203">이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="5ef94-204">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-204">Yes</span></span> |

<span data-ttu-id="5ef94-205">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="5ef94-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="5ef94-206">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="5ef94-206">Token expiration</span></span>
<span data-ttu-id="5ef94-207">hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 시간이 지난 후에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="5ef94-208">hello 메시지의 뒤에 해당 hello 인증 토큰이 만료 되었습니다.을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="5ef94-209">자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="5ef94-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="5ef94-210">AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="5ef94-211">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21-09-31Z</span><span class="sxs-lookup"><span data-stu-id="5ef94-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="5ef94-212">hello 다음 표에 다양 한 유형의 사용자 계정의 hello 만료 시간:</span><span class="sxs-lookup"><span data-stu-id="5ef94-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="5ef94-213">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="5ef94-213">User type</span></span> | <span data-ttu-id="5ef94-214">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="5ef94-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ef94-215">Azure Active Directory에서 관리되지 *않는* 사용자 계정(예: @hotmail.com 또는 @live.com)</span><span class="sxs-lookup"><span data-stu-id="5ef94-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="5ef94-216">12시간</span><span class="sxs-lookup"><span data-stu-id="5ef94-216">12 hours</span></span> |
| <span data-ttu-id="5ef94-217">Azure Active Directory에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="5ef94-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="5ef94-218">hello 마지막 조각 실행 한 후 14 일</span><span class="sxs-lookup"><span data-stu-id="5ef94-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="5ef94-219">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="5ef94-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="5ef94-220">Hello 토큰 만료 시간 전에 암호를 변경한 경우 hello 토큰 즉시 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="5ef94-221">이 섹션의 앞에서 언급 한 hello 메시지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="5ef94-222">Hello를 사용 하 여 hello 계정 권한을 다시 부여한 다음 수 **Authorize** hello 토큰 tooredeploy hello 만료 되 면 단추는 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="5ef94-223">Hello에 대 한 값을 생성할 수도 있습니다 **sessionId** 및 **권한 부여** 다음 코드를 사용 하 여 프로그래밍 방식으로 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="5ef94-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


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
<span data-ttu-id="5ef94-224">Hello 코드에서 사용 되는 hello 데이터 팩터리 클래스에 대 한 자세한 참조 hello [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [ AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="5ef94-225">추가 참조 tooversion `2.9.10826.1824` 의 `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` hello에 대 한 `WindowsFormsWebAuthenticationDialog` hello 코드에서 사용 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="5ef94-226">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-226">Dataset properties</span></span>
<span data-ttu-id="5ef94-227">데이터 레이크 저장소에서 데이터 집합 toorepresent 입력된 데이터 toospecify 설정한 hello **형식** hello 데이터 집합의 속성 너무**AzureDataLakeStore**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="5ef94-228">집합 hello **linkedServiceName** hello 데이터 레이크 저장소의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="5ef94-229">JSON 섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5ef94-230">**구조**, **가용성** 및 **정책**과 JSON의 데이터 집합 섹션은 모든 데이터 집합 형식(예: SQL Database, Azure Blob, Azure 테이블)에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="5ef94-231">hello **typeProperties** 섹션은 데이터 집합의 각 유형에 대해 서로 다른 및 위치와 hello 데이터 저장소에 hello 데이터 형식과 같은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="5ef94-232">hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **AzureDataLakeStore** hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="5ef94-233">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-233">Property</span></span> | <span data-ttu-id="5ef94-234">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-234">Description</span></span> | <span data-ttu-id="5ef94-235">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5ef94-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="5ef94-236">**folderPath**</span></span> |<span data-ttu-id="5ef94-237">경로 toohello 컨테이너 및 데이터 레이크 저장소의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="5ef94-238">예</span><span class="sxs-lookup"><span data-stu-id="5ef94-238">Yes</span></span> |
| <span data-ttu-id="5ef94-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="5ef94-239">**fileName**</span></span> |<span data-ttu-id="5ef94-240">Azure 데이터 레이크 저장소의 hello 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="5ef94-241">hello **fileName** 속성은 선택 사항이 고 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="5ef94-242">지정 하는 경우 **fileName**, hello 특정 파일에서 작동 하는 hello 활동 (복사본 포함).</span><span class="sxs-lookup"><span data-stu-id="5ef94-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="5ef94-243">때 **fileName** 를 지정 하지 않으면에 모든 파일을 포함 하는 복사 **folderPath** hello 입력된 데이터 집합의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="5ef94-244">때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello hello 생성 된 파일의 이름이 데이터 hello 형태로 활동 싱크에 지정 되지 않은. _Guid_.txt'.</span><span class="sxs-lookup"><span data-stu-id="5ef94-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="5ef94-245">예제: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="5ef94-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="5ef94-246">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-246">No</span></span> |
| <span data-ttu-id="5ef94-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="5ef94-247">**partitionedBy**</span></span> |<span data-ttu-id="5ef94-248">hello **partitionedBy** 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="5ef94-249">동적 경로 toospecify와 시계열 데이터에 대 한 파일 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="5ef94-250">예를 들어 **folderPath**는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="5ef94-251">세부 정보 및 예제 참조 [partitionedBy 속성 hello](#using-partitionedby-property)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="5ef94-252">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-252">No</span></span> |
| <span data-ttu-id="5ef94-253">**format**</span><span class="sxs-lookup"><span data-stu-id="5ef94-253">**format**</span></span> | <span data-ttu-id="5ef94-254">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, 및  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="5ef94-255">집합 hello **형식** 아래의 속성 **형식** tooone 다음이 값 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="5ef94-256">자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) hello의 섹션에서는 [Azure Data Factory에서 지 원하는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="5ef94-257">Toocopy 파일 "으로-는" 파일 기반 저장소 (이진 복사), 간에 hello 건너뜁니다 `format` 두 입력 및 출력 데이터 집합 정의에 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5ef94-258">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-258">No</span></span> |
| <span data-ttu-id="5ef94-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="5ef94-259">**compression**</span></span> | <span data-ttu-id="5ef94-260">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="5ef94-261">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5ef94-262">**Optimal** 및 **Fastest** 수준이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5ef94-263">자세한 내용은 [Azure Data Factory에서 지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef94-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5ef94-264">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="5ef94-265">hello partitionedBy 속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-265">hello partitionedBy property</span></span>
<span data-ttu-id="5ef94-266">동적으로 지정할 수 **folderPath** 및 **fileName** hello 사용 하 여 시계열 데이터에 대 한 속성 **partitionedBy** 속성, 데이터 팩터리 함수 및 시스템 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="5ef94-267">자세한 내용은 참조 hello [Azure 데이터 팩터리-함수 및 시스템 변수](data-factory-functions-variables.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="5ef94-268">다음 예에서는, hello에 `{Slice}` hello hello 데이터 팩터리 시스템 변수 값으로 대체 됩니다 `SliceStart` hello 형식 지정 (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="5ef94-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="5ef94-269">hello 이름 `SliceStart` hello 조각의 toohello 시작 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="5ef94-270">hello `folderPath` 속성은 다음과 같이 각 조각에 대 한 다른 `wikidatagateway/wikisampledataout/2014100103` 또는 `wikidatagateway/wikisampledataout/2014100104`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="5ef94-271">다음 예에서는, hello 연도, 월, 일 및 시간을 hello에 `SliceStart` hello에서 사용 되는 개별 변수로 추출 `folderPath` 및 `fileName` 속성:</span><span class="sxs-lookup"><span data-stu-id="5ef94-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="5ef94-272">시계열 데이터 집합에 대 한 자세한 내용은 예약 및 조각이 참조 hello [Azure Data Factory에서 데이터 집합](data-factory-create-datasets.md) 및 [Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="5ef94-273">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-273">Copy activity properties</span></span>
<span data-ttu-id="5ef94-274">섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5ef94-275">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5ef94-276">hello에 사용할 수 있는 속성 hello **typeProperties** 각 활동 유형에 활동의 섹션에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="5ef94-277">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5ef94-278">**AzureDataLakeStoreSource** hello에서 속성을 다음 hello 지원 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="5ef94-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="5ef94-279">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-279">Property</span></span> | <span data-ttu-id="5ef94-280">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-280">Description</span></span> | <span data-ttu-id="5ef94-281">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="5ef94-281">Allowed values</span></span> | <span data-ttu-id="5ef94-282">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5ef94-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="5ef94-283">**recursive**</span></span> |<span data-ttu-id="5ef94-284">Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="5ef94-285">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="5ef94-285">True (default value), False</span></span> |<span data-ttu-id="5ef94-286">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-286">No</span></span> |


<span data-ttu-id="5ef94-287">**AzureDataLakeStoreSink** hello 다음과 같은 hello에 대 한 속성을 지 원하는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="5ef94-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="5ef94-288">속성</span><span class="sxs-lookup"><span data-stu-id="5ef94-288">Property</span></span> | <span data-ttu-id="5ef94-289">설명</span><span class="sxs-lookup"><span data-stu-id="5ef94-289">Description</span></span> | <span data-ttu-id="5ef94-290">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="5ef94-290">Allowed values</span></span> | <span data-ttu-id="5ef94-291">필수</span><span class="sxs-lookup"><span data-stu-id="5ef94-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5ef94-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="5ef94-292">**copyBehavior**</span></span> |<span data-ttu-id="5ef94-293">Hello 복사 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="5ef94-294"><b>PreserveHierarchy</b>: hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="5ef94-295">hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="5ef94-296"><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 hello 대상 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="5ef94-297">hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="5ef94-298"><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="5ef94-299">Hello 파일이 나 blob 이름을 지정 하는 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="5ef94-300">그렇지 않으면 hello 파일 이름이 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="5ef94-301">아니요</span><span class="sxs-lookup"><span data-stu-id="5ef94-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="5ef94-302">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="5ef94-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="5ef94-303">이 섹션에서는 hello 재귀 및 copyBehavior 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="5ef94-304">recursive</span><span class="sxs-lookup"><span data-stu-id="5ef94-304">recursive</span></span> | <span data-ttu-id="5ef94-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5ef94-305">copyBehavior</span></span> | <span data-ttu-id="5ef94-306">결과 동작</span><span class="sxs-lookup"><span data-stu-id="5ef94-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ef94-307">true</span><span class="sxs-lookup"><span data-stu-id="5ef94-307">true</span></span> |<span data-ttu-id="5ef94-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5ef94-308">preserveHierarchy</span></span> |<span data-ttu-id="5ef94-309">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-310">Folder1</span></span><br/><span data-ttu-id="5ef94-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-317">hello 대상 폴더가 Folder1 hello 소스로 구조체 같은 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="5ef94-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-318">Folder1</span></span><br/><span data-ttu-id="5ef94-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="5ef94-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="5ef94-325">true</span><span class="sxs-lookup"><span data-stu-id="5ef94-325">true</span></span> |<span data-ttu-id="5ef94-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5ef94-326">flattenHierarchy</span></span> |<span data-ttu-id="5ef94-327">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-328">Folder1</span></span><br/><span data-ttu-id="5ef94-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-335">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-336">Folder1</span></span><br/><span data-ttu-id="5ef94-337">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5ef94-338">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="5ef94-339">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="5ef94-340">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="5ef94-341">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="5ef94-342">true</span><span class="sxs-lookup"><span data-stu-id="5ef94-342">true</span></span> |<span data-ttu-id="5ef94-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5ef94-343">mergeFiles</span></span> |<span data-ttu-id="5ef94-344">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-345">Folder1</span></span><br/><span data-ttu-id="5ef94-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-352">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-353">Folder1</span></span><br/><span data-ttu-id="5ef94-354">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="5ef94-355">false</span><span class="sxs-lookup"><span data-stu-id="5ef94-355">false</span></span> |<span data-ttu-id="5ef94-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5ef94-356">preserveHierarchy</span></span> |<span data-ttu-id="5ef94-357">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="5ef94-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-358">Folder1</span></span><br/><span data-ttu-id="5ef94-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-365">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5ef94-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-366">Folder1</span></span><br/><span data-ttu-id="5ef94-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="5ef94-369">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5ef94-370">false</span><span class="sxs-lookup"><span data-stu-id="5ef94-370">false</span></span> |<span data-ttu-id="5ef94-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5ef94-371">flattenHierarchy</span></span> |<span data-ttu-id="5ef94-372">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="5ef94-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-373">Folder1</span></span><br/><span data-ttu-id="5ef94-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-380">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5ef94-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-381">Folder1</span></span><br/><span data-ttu-id="5ef94-382">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5ef94-383">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="5ef94-384">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5ef94-385">false</span><span class="sxs-lookup"><span data-stu-id="5ef94-385">false</span></span> |<span data-ttu-id="5ef94-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5ef94-386">mergeFiles</span></span> |<span data-ttu-id="5ef94-387">원본 폴더의 Folder1 구조를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ef94-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="5ef94-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-388">Folder1</span></span><br/><span data-ttu-id="5ef94-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5ef94-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5ef94-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5ef94-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5ef94-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5ef94-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5ef94-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5ef94-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5ef94-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5ef94-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5ef94-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5ef94-395">Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="5ef94-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="5ef94-396">Folder1</span></span><br/><span data-ttu-id="5ef94-397">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="5ef94-398">File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="5ef94-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="5ef94-399">File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="5ef94-400">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="5ef94-400">Supported file and compression formats</span></span>
<span data-ttu-id="5ef94-401">자세한 내용은 참조 hello [Azure Data Factory에서 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="5ef94-402">데이터 레이크 저장소에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="5ef94-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="5ef94-403">hello 예제 따르는 샘플 JSON 정의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="5ef94-404">이러한 샘플 정의 toocreate 파이프라인을 사용 하 여 hello를 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5ef94-405">예제에서는 보여 어떻게 hello 데이터 레이크 저장소 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="5ef94-406">그러나 데이터를 복사할 수 있습니다 _직접_ 지원 hello 싱크 hello 소스 tooany 중 어디에서 든 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="5ef94-407">자세한 내용은 hello에서 "지원 되는 데이터 저장소와 형식" hello 섹션 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="5ef94-408">예: Azure Blob 저장소 tooAzure 데이터 레이크 저장소에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="5ef94-409">이 섹션의 예제 코드에서는 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="5ef94-410">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="5ef94-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5ef94-411">[AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="5ef94-412">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5ef94-413">[AzureDataLakeStore](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="5ef94-414">[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureDataLakeStoreSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="5ef94-415">hello 예제 방식을 보여 시계열 데이터를 Azure Blob 저장소 1 시간 마다 tooData Lake 저장소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="5ef94-416">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="5ef94-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="5ef94-417">**Azure Data Lake Store 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="5ef94-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="5ef94-418">구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="5ef94-419">**Azure Blob 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="5ef94-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="5ef94-420">다음 예제는 hello에서 데이터를 선택 새 blob에서 매시간 (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="5ef94-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="5ef94-421">hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5ef94-422">hello 폴더 경로 hello 연도, 월 및 hello 시작 시간의 일 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="5ef94-423">hello 파일 이름은 hello 시간 hello 부분의 시작 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="5ef94-424">hello `"external": true` 설정 알립니다 hello 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="5ef94-425">**Azure Data Lake Store 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="5ef94-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="5ef94-426">다음 예에서는 복사본 데이터 레이크 저장소 tooData 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="5ef94-427">새 데이터를 복사할 1 시간 마다 tooData Lake 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-427">New data is copied tooData Lake Store every hour.</span></span>

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


<span data-ttu-id="5ef94-428">**Blob 원본 및 Data Lake Store 싱크를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="5ef94-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="5ef94-429">다음 예제는 hello, hello 파이프라인에 구성 된 복사 활동 toouse hello 입력 및 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="5ef94-430">hello 복사 작업은 예약 된 toorun 마다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="5ef94-431">Hello 파이프라인 JSON 정의에서 hello `source` 형식이 너무 설정`BlobSource`, 및 hello `sink` 형식이 너무 설정`AzureDataLakeStoreSink`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="5ef94-432">예: Azure 데이터 레이크 저장소 tooan Azure blob에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="5ef94-433">이 섹션의 예제 코드에서는 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="5ef94-434">[AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="5ef94-435">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="5ef94-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5ef94-436">[AzureDataLakeStore](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="5ef94-437">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="5ef94-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5ef94-438">[AzureDataLakeStoreSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5ef94-439">hello 코드 시계열 데이터 복사 Data Lake 저장소 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="5ef94-440">**Azure Data Lake Store 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="5ef94-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="5ef94-441">구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5ef94-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="5ef94-442">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="5ef94-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="5ef94-443">**Azure Data Lake 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="5ef94-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="5ef94-444">이 예제에서는 설정 `"external"` 너무`true` 알리고 hello Data Factory 서비스가 해당 hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="5ef94-445">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="5ef94-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="5ef94-446">다음 예제는 hello, 데이터 작성 된 새 blob tooa 매시간 (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="5ef94-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="5ef94-447">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5ef94-448">hello 폴더 경로 hello 연도, 월, 일 및 시간 부분의 hello 시작 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

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

<span data-ttu-id="5ef94-449">**Azure Data Lake Store 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업**</span><span class="sxs-lookup"><span data-stu-id="5ef94-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="5ef94-450">다음 예제는 hello, hello 파이프라인에 구성 된 복사 활동 toouse hello 입력 및 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="5ef94-451">hello 복사 작업은 예약 된 toorun 마다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="5ef94-452">Hello 파이프라인 JSON 정의에서 hello `source` 형식이 너무 설정`AzureDataLakeStoreSource`, 및 hello `sink` 형식이 너무 설정`BlobSink`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

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

<span data-ttu-id="5ef94-453">Hello 복사 활동 정의의 hello 원본 데이터 집합 toocolumns hello 싱크 데이터 집합의 열을 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef94-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="5ef94-454">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef94-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5ef94-455">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="5ef94-455">Performance and tuning</span></span>
<span data-ttu-id="5ef94-456">복사 활동 성능에 영향을 주는 hello 요소에 대해 toolearn와 방법을 toooptimize, hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ef94-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
