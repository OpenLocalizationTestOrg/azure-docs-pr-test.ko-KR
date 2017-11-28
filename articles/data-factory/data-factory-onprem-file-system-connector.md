---
title: "Azure 데이터 팩터리를 사용 하 여 파일 시스템에서 데이터를 aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 Azure 데이터 팩터리를 사용 하 여 온-프레미스 파일 시스템에서 데이터 tooand toocopy 합니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="d03aa-103">Azure 데이터 팩터리를 사용 하 여 온-프레미스 파일 시스템에서 데이터 tooand 복사</span><span class="sxs-lookup"><span data-stu-id="d03aa-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="d03aa-104">이 문서에서는 toouse 온-프레미스 파일 시스템에서 Azure Data Factory toocopy 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="d03aa-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d03aa-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="d03aa-106">Supported scenarios</span></span>
<span data-ttu-id="d03aa-107">데이터를 복사할 수 **온-프레미스 파일 시스템에서** toohello 데이터 저장소를 다음:</span><span class="sxs-lookup"><span data-stu-id="d03aa-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d03aa-108">Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooan 온-프레미스 파일 시스템**:</span><span class="sxs-lookup"><span data-stu-id="d03aa-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="d03aa-109">복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="d03aa-110">성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="d03aa-111">연결 사용</span><span class="sxs-lookup"><span data-stu-id="d03aa-111">Enabling connectivity</span></span>
<span data-ttu-id="d03aa-112">데이터 팩터리를 통해 온-프레미스 파일 시스템에서 연결 tooand 지원 **데이터 관리 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="d03aa-113">Hello Data Factory 서비스 tooconnect tooany 지원 되는 온-프레미스 데이터 저장소 용 파일 시스템을 포함 하 여 온-프레미스 환경에서 hello 데이터 관리 게이트웨이 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="d03aa-114">toolearn hello 게이트웨이 설정에 대 한 단계별 지침은 및 데이터 관리 게이트웨이 대 한 참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="d03aa-115">데이터 관리 게이트웨이 외에도 다른 이진 파일이 설치 toobe toocommunicate tooand 온-프레미스 파일 시스템에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="d03aa-116">설치 하 고 hello 파일 시스템은 Azure IaaS VM의 경우에 hello 데이터 관리 게이트웨이 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="d03aa-117">Hello 게이트웨이에 대 한 자세한 내용은 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="d03aa-118">toouse Linux 파일 공유, 설치 [Samba](https://www.samba.org/) Linux 서버 및 Windows 서버에서 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="d03aa-119">Linux 서버에 대한 데이터 관리 게이트웨이 설치는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d03aa-120">시작</span><span class="sxs-lookup"><span data-stu-id="d03aa-120">Getting started</span></span>
<span data-ttu-id="d03aa-121">다른 도구/API를 사용하여 파일 시스템 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="d03aa-122">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d03aa-123">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d03aa-124">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d03aa-125">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="d03aa-126">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d03aa-127">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-127">Create a **data factory**.</span></span> <span data-ttu-id="d03aa-128">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d03aa-129">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="d03aa-130">예를 들어 Azure blob 저장소 tooan 온-프레미스 파일 시스템에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink 온-프레미스 파일 시스템 및 Azure 저장소 계정 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="d03aa-131">연결 된 서비스를 속성에는 특정 tooan 온-프레미스 파일 시스템에 대 한 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="d03aa-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="d03aa-132">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="d03aa-133">Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="d03aa-134">고 다른 데이터 집합 toospecify hello 폴더 및 파일 이름 파일 시스템에서 (선택 사항)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="d03aa-135">데이터 집합 속성을 특정 tooon 온-프레미스 파일 시스템에 대 한 참조 [데이터 집합 속성](#dataset-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="d03aa-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d03aa-136">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d03aa-137">앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 FileSystemSink 싱크도 hello 복사 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="d03aa-138">마찬가지로, 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 복사 하는 경우 FileSystemSource 및 사용 BlobSink hello 복사 활동에서.</span><span class="sxs-lookup"><span data-stu-id="d03aa-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="d03aa-139">복사 활동 속성을 특정 tooon 온-프레미스 파일 시스템에 대 한 참조 [활동 속성을 복사](#copy-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="d03aa-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d03aa-140">에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="d03aa-141">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d03aa-142">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d03aa-143">샘플 은/파일 시스템에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-file-system) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="d03aa-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="d03aa-144">사용 되는 toodefine Data Factory 엔터티에 특정 toofile 시스템은 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:</span><span class="sxs-lookup"><span data-stu-id="d03aa-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d03aa-145">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-145">Linked service properties</span></span>
<span data-ttu-id="d03aa-146">온-프레미스 파일 시스템 tooan Azure 데이터 팩터리에 hello로 연결할 수 있습니다 **온-프레미스 파일 서버** 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="d03aa-147">다음 표에서 hello JSON 요소를 특정 toohello 온-프레미스 파일 서버를 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="d03aa-148">속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-148">Property</span></span> | <span data-ttu-id="d03aa-149">설명</span><span class="sxs-lookup"><span data-stu-id="d03aa-149">Description</span></span> | <span data-ttu-id="d03aa-150">필수</span><span class="sxs-lookup"><span data-stu-id="d03aa-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d03aa-151">type</span><span class="sxs-lookup"><span data-stu-id="d03aa-151">type</span></span> |<span data-ttu-id="d03aa-152">Hello type 속성이 너무 설정 되어 있는지 확인**OnPremisesFileServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="d03aa-153">예</span><span class="sxs-lookup"><span data-stu-id="d03aa-153">Yes</span></span> |
| <span data-ttu-id="d03aa-154">host</span><span class="sxs-lookup"><span data-stu-id="d03aa-154">host</span></span> |<span data-ttu-id="d03aa-155">Toocopy hello 폴더의 hello 루트 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="d03aa-156">Hello 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d03aa-157">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="d03aa-158">예</span><span class="sxs-lookup"><span data-stu-id="d03aa-158">Yes</span></span> |
| <span data-ttu-id="d03aa-159">userid</span><span class="sxs-lookup"><span data-stu-id="d03aa-159">userid</span></span> |<span data-ttu-id="d03aa-160">Hello 있는 사용자에 게 액세스 toohello 서버 hello ID를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="d03aa-161">아니요(encryptedCredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="d03aa-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="d03aa-162">암호</span><span class="sxs-lookup"><span data-stu-id="d03aa-162">password</span></span> |<span data-ttu-id="d03aa-163">Hello 사용자 (userid)에 대 한 hello 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="d03aa-164">아니요(encryptedcredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="d03aa-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="d03aa-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d03aa-165">encryptedCredential</span></span> |<span data-ttu-id="d03aa-166">새로 만들기-AzureRmDataFactoryEncryptValue hello cmdlet을 실행 하 여 얻을 수 있는 암호화 hello 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="d03aa-167">아니요 (일반 텍스트로 toospecify userid 및 password 선택) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d03aa-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="d03aa-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d03aa-168">gatewayName</span></span> |<span data-ttu-id="d03aa-169">데이터 팩터리 tooconnect toohello 온-프레미스 파일 서버를 사용 해야 하는 hello 게이트웨이의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="d03aa-170">예</span><span class="sxs-lookup"><span data-stu-id="d03aa-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="d03aa-171">연결된 서비스 및 데이터 집합 정의 샘플</span><span class="sxs-lookup"><span data-stu-id="d03aa-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="d03aa-172">시나리오</span><span class="sxs-lookup"><span data-stu-id="d03aa-172">Scenario</span></span> | <span data-ttu-id="d03aa-173">연결된 서비스 정의의 호스트</span><span class="sxs-lookup"><span data-stu-id="d03aa-173">Host in linked service definition</span></span> | <span data-ttu-id="d03aa-174">데이터 집합 정의의 folderPath</span><span class="sxs-lookup"><span data-stu-id="d03aa-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d03aa-175">데이터 관리 게이트웨이 컴퓨터의 로컬 폴더: </span><span class="sxs-lookup"><span data-stu-id="d03aa-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="d03aa-176">예: D:\\\* 또는 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="d03aa-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="d03aa-177">D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="d03aa-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="d03aa-178">localhost(데이터 관리 게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="d03aa-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="d03aa-179">.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="d03aa-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="d03aa-180">D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="d03aa-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="d03aa-181">원격 공유 폴더: </span><span class="sxs-lookup"><span data-stu-id="d03aa-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="d03aa-182">예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="d03aa-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="d03aa-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="d03aa-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="d03aa-184">.\\\\ 또는 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="d03aa-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="d03aa-185">예제: 일반 텍스트에 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="d03aa-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="d03aa-186">예제: encryptedcredential 사용</span><span class="sxs-lookup"><span data-stu-id="d03aa-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d03aa-187">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-187">Dataset properties</span></span>
<span data-ttu-id="d03aa-188">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="d03aa-189">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="d03aa-190">hello typeProperties 섹션은 데이터 집합의 각 유형에 대해 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="d03aa-191">Hello 위치와 hello 데이터 저장소에 hello 데이터 형식과 같은 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="d03aa-192">hello typeProperties 형식의 hello 데이터 집합에 대 한 섹션 **FileShare** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="d03aa-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="d03aa-193">속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-193">Property</span></span> | <span data-ttu-id="d03aa-194">설명</span><span class="sxs-lookup"><span data-stu-id="d03aa-194">Description</span></span> | <span data-ttu-id="d03aa-195">필수</span><span class="sxs-lookup"><span data-stu-id="d03aa-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d03aa-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="d03aa-196">folderPath</span></span> |<span data-ttu-id="d03aa-197">Hello 하위 경로 toohello 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="d03aa-198">Hello 이스케이프 문자를 사용 하 여 ' \' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="d03aa-199">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d03aa-200">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d03aa-201">예</span><span class="sxs-lookup"><span data-stu-id="d03aa-201">Yes</span></span> |
| <span data-ttu-id="d03aa-202">fileName</span><span class="sxs-lookup"><span data-stu-id="d03aa-202">fileName</span></span> |<span data-ttu-id="d03aa-203">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d03aa-204">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d03aa-205">때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello hello 생성 된 파일의 이름이 형식에 따라 hello에 활동 싱크에 지정 되지 않은:</span><span class="sxs-lookup"><span data-stu-id="d03aa-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="d03aa-206">`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="d03aa-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="d03aa-207">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-207">No</span></span> |
| <span data-ttu-id="d03aa-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="d03aa-208">fileFilter</span></span> |<span data-ttu-id="d03aa-209">필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="d03aa-210">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d03aa-211">예 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="d03aa-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="d03aa-212">예 2: "fileFilter": 2014-1-?. txt "</span><span class="sxs-lookup"><span data-stu-id="d03aa-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="d03aa-213">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="d03aa-214">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-214">No</span></span> |
| <span data-ttu-id="d03aa-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d03aa-215">partitionedBy</span></span> |<span data-ttu-id="d03aa-216">시계열 데이터에 대 한 partitionedBy toospecify 동적 folderPath/파일 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="d03aa-217">예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d03aa-218">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-218">No</span></span> |
| <span data-ttu-id="d03aa-219">format</span><span class="sxs-lookup"><span data-stu-id="d03aa-219">format</span></span> | <span data-ttu-id="d03aa-220">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d03aa-221">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d03aa-222">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d03aa-223">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="d03aa-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d03aa-224">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-224">No</span></span> |
| <span data-ttu-id="d03aa-225">압축</span><span class="sxs-lookup"><span data-stu-id="d03aa-225">compression</span></span> | <span data-ttu-id="d03aa-226">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d03aa-227">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d03aa-228">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d03aa-229">[Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d03aa-230">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d03aa-231">fileName 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="d03aa-232">partitionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="d03aa-232">Using partitionedBy property</span></span>
<span data-ttu-id="d03aa-233">동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="d03aa-234">toounderstand 시계열 데이터 집합, 일정 및 분할에 대 한 자세한 내용은 참조 [데이터 집합을 만드는](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d03aa-235">샘플 1:</span><span class="sxs-lookup"><span data-stu-id="d03aa-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="d03aa-236">이 예제에서 {Slice} hello (yyyymmddhh)에서 hello 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="d03aa-237">SliceStart는 hello 조각의 toostart 시간을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="d03aa-238">hello folderPath 각 조각에 대 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="d03aa-239">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d03aa-240">샘플 2:</span><span class="sxs-lookup"><span data-stu-id="d03aa-240">Sample 2:</span></span>

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

<span data-ttu-id="d03aa-241">이 예제에서는 SliceStart의 년, 월, 일, 시간과 hello folderPath 및 fileName 속성에 사용 하는 개별 변수로 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d03aa-242">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-242">Copy activity properties</span></span>
<span data-ttu-id="d03aa-243">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="d03aa-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d03aa-244">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="d03aa-245">반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="d03aa-246">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="d03aa-247">온-프레미스 파일 시스템에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**FileSystemSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="d03aa-248">마찬가지로, 데이터 tooan를 이동 하는 경우 온-프레미스 파일 시스템, 너무 hello 복사 작업에서 싱크 유형이 hello을 설정**FileSystemSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="d03aa-249">이 섹션에서는 FileSystemSource 및 FileSystemSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="d03aa-250">**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="d03aa-251">속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-251">Property</span></span> | <span data-ttu-id="d03aa-252">설명</span><span class="sxs-lookup"><span data-stu-id="d03aa-252">Description</span></span> | <span data-ttu-id="d03aa-253">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="d03aa-253">Allowed values</span></span> | <span data-ttu-id="d03aa-254">필수</span><span class="sxs-lookup"><span data-stu-id="d03aa-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d03aa-255">recursive</span><span class="sxs-lookup"><span data-stu-id="d03aa-255">recursive</span></span> |<span data-ttu-id="d03aa-256">Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="d03aa-257">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="d03aa-257">True, False (default)</span></span> |<span data-ttu-id="d03aa-258">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-258">No</span></span> |

<span data-ttu-id="d03aa-259">**FileSystemSink** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="d03aa-260">속성</span><span class="sxs-lookup"><span data-stu-id="d03aa-260">Property</span></span> | <span data-ttu-id="d03aa-261">설명</span><span class="sxs-lookup"><span data-stu-id="d03aa-261">Description</span></span> | <span data-ttu-id="d03aa-262">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="d03aa-262">Allowed values</span></span> | <span data-ttu-id="d03aa-263">필수</span><span class="sxs-lookup"><span data-stu-id="d03aa-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d03aa-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d03aa-264">copyBehavior</span></span> |<span data-ttu-id="d03aa-265">파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="d03aa-266">**PreserveHierarchy:** hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="d03aa-267">즉, hello 소스 파일 toohello 원본 폴더의 상대 경로 hello hello hello 대상 파일 toohello 대상 폴더의 상대 경로와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="d03aa-268">**FlattenHierarchy:** hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="d03aa-269">hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="d03aa-270">**MergeFiles:** hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="d03aa-271">Hello 파일 이름/blob 이름이 지정 된 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="d03aa-272">그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="d03aa-273">아니요</span><span class="sxs-lookup"><span data-stu-id="d03aa-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="d03aa-274">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="d03aa-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="d03aa-275">이 섹션에서는 hello hello 재귀 및 copyBehavior 속성에 대 한 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="d03aa-276">recursive 값</span><span class="sxs-lookup"><span data-stu-id="d03aa-276">recursive value</span></span> | <span data-ttu-id="d03aa-277">copyBehavior 값</span><span class="sxs-lookup"><span data-stu-id="d03aa-277">copyBehavior value</span></span> | <span data-ttu-id="d03aa-278">결과 동작</span><span class="sxs-lookup"><span data-stu-id="d03aa-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d03aa-279">true</span><span class="sxs-lookup"><span data-stu-id="d03aa-279">true</span></span> |<span data-ttu-id="d03aa-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d03aa-280">preserveHierarchy</span></span> |<span data-ttu-id="d03aa-281">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-282">Folder1</span></span><br/><span data-ttu-id="d03aa-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-289">hello 소스로 구조체 같은 hello로 Folder1 hello 대상 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="d03aa-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-290">Folder1</span></span><br/><span data-ttu-id="d03aa-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="d03aa-297">true</span><span class="sxs-lookup"><span data-stu-id="d03aa-297">true</span></span> |<span data-ttu-id="d03aa-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d03aa-298">flattenHierarchy</span></span> |<span data-ttu-id="d03aa-299">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-300">Folder1</span></span><br/><span data-ttu-id="d03aa-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-307">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="d03aa-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-308">Folder1</span></span><br/><span data-ttu-id="d03aa-309">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="d03aa-310">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="d03aa-311">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="d03aa-312">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="d03aa-313">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="d03aa-314">true</span><span class="sxs-lookup"><span data-stu-id="d03aa-314">true</span></span> |<span data-ttu-id="d03aa-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d03aa-315">mergeFiles</span></span> |<span data-ttu-id="d03aa-316">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-317">Folder1</span></span><br/><span data-ttu-id="d03aa-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-324">hello 대상 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="d03aa-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-325">Folder1</span></span><br/><span data-ttu-id="d03aa-326">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="d03aa-327">false</span><span class="sxs-lookup"><span data-stu-id="d03aa-327">false</span></span> |<span data-ttu-id="d03aa-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="d03aa-328">preserveHierarchy</span></span> |<span data-ttu-id="d03aa-329">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-330">Folder1</span></span><br/><span data-ttu-id="d03aa-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-337">hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="d03aa-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-338">Folder1</span></span><br/><span data-ttu-id="d03aa-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="d03aa-341">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="d03aa-342">false</span><span class="sxs-lookup"><span data-stu-id="d03aa-342">false</span></span> |<span data-ttu-id="d03aa-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="d03aa-343">flattenHierarchy</span></span> |<span data-ttu-id="d03aa-344">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-345">Folder1</span></span><br/><span data-ttu-id="d03aa-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-352">hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="d03aa-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-353">Folder1</span></span><br/><span data-ttu-id="d03aa-354">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="d03aa-355">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="d03aa-356">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="d03aa-357">false</span><span class="sxs-lookup"><span data-stu-id="d03aa-357">false</span></span> |<span data-ttu-id="d03aa-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="d03aa-358">mergeFiles</span></span> |<span data-ttu-id="d03aa-359">구조에 따라 hello로 Folder1 소스 폴더에 대 한</span><span class="sxs-lookup"><span data-stu-id="d03aa-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="d03aa-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-360">Folder1</span></span><br/><span data-ttu-id="d03aa-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="d03aa-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="d03aa-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="d03aa-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="d03aa-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="d03aa-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="d03aa-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="d03aa-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="d03aa-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="d03aa-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="d03aa-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="d03aa-367">hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="d03aa-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="d03aa-368">Folder1</span></span><br/><span data-ttu-id="d03aa-369">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="d03aa-370">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="d03aa-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="d03aa-371">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="d03aa-372">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="d03aa-372">Supported file and compression formats</span></span>
<span data-ttu-id="d03aa-373">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="d03aa-374">파일 시스템에서 데이터 tooand 복사 하기 위한 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="d03aa-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="d03aa-375">hello 다음 예에서는 샘플 JSON 정의 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d03aa-376">표시 방법을 toocopy 데이터 tooand에서 온-프레미스 파일 시스템 및 Azure Blob 저장소의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="d03aa-377">그러나 데이터를 복사할 수 있습니다 *직접* hello 싱크에 나열 된 hello 소스 tooany 중 어디에서 든 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="d03aa-378">예: 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="d03aa-379">이 샘플은 어떻게 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="d03aa-380">hello 샘플 Data Factory 엔터티에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="d03aa-381">[OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d03aa-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="d03aa-382">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d03aa-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d03aa-383">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d03aa-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="d03aa-384">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d03aa-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d03aa-385">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d03aa-386">다음 예제는 hello 시계열 데이터 복사 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="d03aa-387">이 예제에 사용 되는 hello JSON 속성 hello 샘플 후 hello 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="d03aa-388">첫 번째 단계로, 설정 데이터 관리 게이트웨이 hello 지침에 따라 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="d03aa-389">**온-프레미스 파일 서버 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="d03aa-390">Hello를 사용 하는 것이 좋습니다 **encryptedCredential** 속성 대신 hello **userid** 및 **암호** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="d03aa-391">이 연결 서비스에 대한 자세한 내용은 [파일 서버 연결 서비스](#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="d03aa-392">**Azure 저장소 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="d03aa-393">**온-프레미스 파일 시스템 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="d03aa-394">데이터는 매시간 새 파일에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="d03aa-395">hello folderPath 및 fileName 속성 hello 조각의 hello 시작 시간에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="d03aa-396">설정 `"external": "true"` 알리고 Data Factory hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="d03aa-397">**Azure Blob 저장소 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="d03aa-398">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="d03aa-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d03aa-399">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d03aa-400">hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="d03aa-401">**파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="d03aa-402">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="d03aa-403">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="d03aa-404">예: Azure SQL 데이터베이스 tooan 온-프레미스 파일 시스템에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="d03aa-405">다음 샘플에서는 hello:</span><span class="sxs-lookup"><span data-stu-id="d03aa-405">hello following sample shows:</span></span>

* <span data-ttu-id="d03aa-406">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="d03aa-407">[OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d03aa-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="d03aa-408">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d03aa-409">[FileShare](#dataset-properties) 형식의 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="d03aa-410">[SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 및 [FileSystemSink](#copy-activity-properties)를 사용하는 복사 작업의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d03aa-411">hello 샘플 시계열 데이터 복사 Azure SQL 테이블 tooan 온-프레미스 파일 시스템에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="d03aa-412">이 예제에 사용 되는 hello JSON 속성은 hello 샘플 이후 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="d03aa-413">**Azure SQL Database 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="d03aa-414">**온-프레미스 파일 서버 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="d03aa-415">Hello를 사용 하는 것이 좋습니다 **encryptedCredential** hello를 사용 하는 대신 속성 **userid** 및 **암호** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="d03aa-416">이 연결 서비스에 대한 자세한 내용은 [파일 시스템 연결 서비스](#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="d03aa-417">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="d03aa-418">hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 되었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="d03aa-419">설정 ``“external”: ”true”`` 알리고 Data Factory hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="d03aa-420">**온-프레미스 파일 시스템 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="d03aa-421">데이터 복사 tooa 새 파일을 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="d03aa-422">hello folderPath 및 fileName hello blob에 대 한 hello 조각의 hello 시작 시간에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="d03aa-423">**SQL 원본 및 파일 시스템 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="d03aa-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="d03aa-424">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="d03aa-425">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource**, 및 hello **싱크** 형식이 너무 설정**FileSystemSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="d03aa-426">hello에 대해 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="d03aa-427">원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="d03aa-428">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d03aa-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d03aa-429">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="d03aa-429">Performance and tuning</span></span>
 <span data-ttu-id="d03aa-430">toolearn 키에 대 한 해당 hello 성능에 영향을 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d03aa-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
