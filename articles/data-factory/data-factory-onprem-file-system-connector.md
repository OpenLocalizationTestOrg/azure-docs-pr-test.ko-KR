---
title: "Azure Data Factory를 사용하여 파일 시스템 간에 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 온-프레미스 파일 시스템에서 데이터를 복사하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="9db89-103">Azure Data Factory를 통한 온-프레미스 파일 시스템에서의 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="9db89-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="9db89-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스 파일 시스템의 데이터를 다른 곳으로 복사하는 방법 또는 그 반대로 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="9db89-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="9db89-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="9db89-106">Supported scenarios</span></span>
<span data-ttu-id="9db89-107">**온-프레미스 파일 시스템에서** 다음 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="9db89-108">다음 데이터 저장소에서 **온-프레미스 파일 시스템으로** 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="9db89-109">복사 작업 시 원본 파일이 대상에 성공적으로 복사된 후 원본 파일이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="9db89-110">성공적 복사 후 원본 파일을 삭제해야 할 경우 파일을 삭제하는 사용자 지정 작업을 만들고 파이프라인에서 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="9db89-111">연결 사용</span><span class="sxs-lookup"><span data-stu-id="9db89-111">Enabling connectivity</span></span>
<span data-ttu-id="9db89-112">Data Factory는 **데이터 관리 게이트웨이**를 통해 온-프레미스 파일 시스템 간의 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="9db89-113">Data Factory 서비스에서 파일 시스템을 비롯한 지원되는 온-프레미스 데이터 저장소에 연결하도록 허용하려면 온-프레미스 환경에 데이터 관리 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="9db89-114">데이터 관리 게이트웨이 및 단계별 게이트웨이 설정 지침을 알아보려면 [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="9db89-115">데이터 관리 게이트웨이와 달리 온-프레미스 파일 시스템과 통신하기 위해 다른 이진 파일을 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="9db89-116">파일 시스템이 Azure IaaS VM인 경우에도 데이터 관리 게이트웨이를 설치하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="9db89-117">게이트웨이에 대한 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="9db89-118">Linux 파일 공유를 사용하려면 Linux 서버에 [Samba](https://www.samba.org/)를 설치하고 Windows 서버에 데이터 관리 게이트웨이를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="9db89-119">Linux 서버에 대한 데이터 관리 게이트웨이 설치는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9db89-120">시작</span><span class="sxs-lookup"><span data-stu-id="9db89-120">Getting started</span></span>
<span data-ttu-id="9db89-121">다른 도구/API를 사용하여 파일 시스템 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="9db89-122">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9db89-123">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="9db89-124">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9db89-125">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="9db89-126">도구를 사용하든 API를 사용하든, 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9db89-127">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-127">Create a **data factory**.</span></span> <span data-ttu-id="9db89-128">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="9db89-129">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="9db89-130">예를 들어 Azure Blob Storage에서 온-프레미스 파일 시스템으로 데이터를 복사하는 경우 온-프레미스 파일 시스템 및 Azure Storage 계정을 데이터 팩터리에 연결하는 두 개의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="9db89-131">온-프레미스 파일 시스템과 관련된 연결된 서비스 속성은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="9db89-132">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="9db89-133">마지막 단계에서 설명한 예제에서는 입력 데이터가 포함된 BLOB 컨테이너 및 폴더를 지정하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="9db89-134">또한 파일 시스템의 폴더 및 파일 이름(선택 사항)을 지정하는 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="9db89-135">온-프레미스 파일 시스템과 관련된 데이터 집합 속성은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="9db89-136">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="9db89-137">앞에서 언급한 예에서는 BlobSource를 원본으로, FileSystemSink를 복사 작업의 싱크로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="9db89-138">마찬가지로, 온-프레미스 파일 시스템에서 Azure Blob Storage로 복사하는 경우 복사 작업에 FileSystemSource 및 BlobSink를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="9db89-139">온-프레미스 파일 시스템과 관련된 복사 작업 속성은 [복사 작업 속성](#copy-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="9db89-140">원본 또는 싱크로 데이터 저장소를 사용하는 방법에 대한 자세한 내용을 보려면 데이터 저장소에 대한 이전 섹션의 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="9db89-141">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9db89-142">도구/API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 Data Factory 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9db89-143">다른 곳에서 파일 시스템으로 또는 그 반대로 데이터를 복사하는 데 사용되는 Data Factory 엔터티의 JSON 정의가 포함된 샘플은 이 문서의 [JSON 예](#json-examples-for-copying-data-to-and-from-file-system) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="9db89-144">다음 섹션에서는 파일 시스템에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9db89-145">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="9db89-145">Linked service properties</span></span>
<span data-ttu-id="9db89-146">**온-프레미스 파일 서버** 연결 서비스를 사용하면 Azure Data Factory에 온-프레미스 파일 시스템을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="9db89-147">다음 표에서는 온-프레미스 파일 서버 연결 서비스에 지정된 JSON 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="9db89-148">속성</span><span class="sxs-lookup"><span data-stu-id="9db89-148">Property</span></span> | <span data-ttu-id="9db89-149">설명</span><span class="sxs-lookup"><span data-stu-id="9db89-149">Description</span></span> | <span data-ttu-id="9db89-150">필수</span><span class="sxs-lookup"><span data-stu-id="9db89-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9db89-151">type</span><span class="sxs-lookup"><span data-stu-id="9db89-151">type</span></span> |<span data-ttu-id="9db89-152">type 속성은 **OnPremisesFileServer**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="9db89-153">예</span><span class="sxs-lookup"><span data-stu-id="9db89-153">Yes</span></span> |
| <span data-ttu-id="9db89-154">host</span><span class="sxs-lookup"><span data-stu-id="9db89-154">host</span></span> |<span data-ttu-id="9db89-155">복사할 폴더의 루트 경로를 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="9db89-156">문자열에서 특수 문자로 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="9db89-157">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="9db89-158">예</span><span class="sxs-lookup"><span data-stu-id="9db89-158">Yes</span></span> |
| <span data-ttu-id="9db89-159">userId</span><span class="sxs-lookup"><span data-stu-id="9db89-159">userid</span></span> |<span data-ttu-id="9db89-160">서버에 대한 액세스 권한이 있는 사용자의 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="9db89-161">아니요(encryptedCredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="9db89-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="9db89-162">password</span><span class="sxs-lookup"><span data-stu-id="9db89-162">password</span></span> |<span data-ttu-id="9db89-163">사용자(userid)의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="9db89-164">아니요(encryptedcredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="9db89-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="9db89-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9db89-165">encryptedCredential</span></span> |<span data-ttu-id="9db89-166">New-AzureRmDataFactoryEncryptValue cmdlet을 실행하여 얻을 수 있는 암호화된 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="9db89-167">아니요(일반 텍스트에 userid 및 암호를 지정하는 경우)</span><span class="sxs-lookup"><span data-stu-id="9db89-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="9db89-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9db89-168">gatewayName</span></span> |<span data-ttu-id="9db89-169">Data Factory에서 온-프레미스 파일 서버에 연결하는 데 사용해야 하는 게이트웨이의 이름을 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="9db89-170">예</span><span class="sxs-lookup"><span data-stu-id="9db89-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="9db89-171">연결된 서비스 및 데이터 집합 정의 샘플</span><span class="sxs-lookup"><span data-stu-id="9db89-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="9db89-172">시나리오</span><span class="sxs-lookup"><span data-stu-id="9db89-172">Scenario</span></span> | <span data-ttu-id="9db89-173">연결된 서비스 정의의 호스트</span><span class="sxs-lookup"><span data-stu-id="9db89-173">Host in linked service definition</span></span> | <span data-ttu-id="9db89-174">데이터 집합 정의의 folderPath</span><span class="sxs-lookup"><span data-stu-id="9db89-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9db89-175">데이터 관리 게이트웨이 컴퓨터의 로컬 폴더: </span><span class="sxs-lookup"><span data-stu-id="9db89-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="9db89-176">예: D:\\\* 또는 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="9db89-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="9db89-177">D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="9db89-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="9db89-178">localhost(데이터 관리 게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="9db89-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="9db89-179">.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="9db89-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="9db89-180">D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="9db89-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="9db89-181">원격 공유 폴더: </span><span class="sxs-lookup"><span data-stu-id="9db89-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="9db89-182">예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="9db89-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="9db89-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="9db89-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="9db89-184">.\\\\ 또는 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="9db89-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="9db89-185">예제: 일반 텍스트에 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="9db89-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="9db89-186">예제: encryptedcredential 사용</span><span class="sxs-lookup"><span data-stu-id="9db89-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="9db89-187">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="9db89-187">Dataset properties</span></span>
<span data-ttu-id="9db89-188">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="9db89-189">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="9db89-190">typeProperties 섹션은 데이터 집합의 각 형식마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="9db89-191">데이터 저장소에 있는 데이터의 위치 및 형식과 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="9db89-192">**FileShare** 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음과 같은 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="9db89-193">속성</span><span class="sxs-lookup"><span data-stu-id="9db89-193">Property</span></span> | <span data-ttu-id="9db89-194">설명</span><span class="sxs-lookup"><span data-stu-id="9db89-194">Description</span></span> | <span data-ttu-id="9db89-195">필수</span><span class="sxs-lookup"><span data-stu-id="9db89-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9db89-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="9db89-196">folderPath</span></span> |<span data-ttu-id="9db89-197">폴더의 하위 경로를 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="9db89-198">문자열에서 특수 문자로 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="9db89-199">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="9db89-200">이 속성을 **partitionBy** 와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="9db89-201">예</span><span class="sxs-lookup"><span data-stu-id="9db89-201">Yes</span></span> |
| <span data-ttu-id="9db89-202">fileName</span><span class="sxs-lookup"><span data-stu-id="9db89-202">fileName</span></span> |<span data-ttu-id="9db89-203">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="9db89-204">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="9db89-205">**fileName**이 출력 데이터 집합에 대해 지정되지 않았고 **preserveHierarchy**가 활동 싱크에 지정되지 않은 경우 생성된 파일의 이름은 다음 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="9db89-206">`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="9db89-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="9db89-207">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-207">No</span></span> |
| <span data-ttu-id="9db89-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="9db89-208">fileFilter</span></span> |<span data-ttu-id="9db89-209">모든 파일이 아닌 folderPath의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="9db89-210">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="9db89-211">예 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="9db89-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="9db89-212">예 2: "fileFilter": 2014-1-?. txt "</span><span class="sxs-lookup"><span data-stu-id="9db89-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="9db89-213">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="9db89-214">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-214">No</span></span> |
| <span data-ttu-id="9db89-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9db89-215">partitionedBy</span></span> |<span data-ttu-id="9db89-216">partitionedBy를 사용하면 시계열 데이터의 동적 folderPath/fileName을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="9db89-217">예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="9db89-218">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-218">No</span></span> |
| <span data-ttu-id="9db89-219">format</span><span class="sxs-lookup"><span data-stu-id="9db89-219">format</span></span> | <span data-ttu-id="9db89-220">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="9db89-221">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="9db89-222">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="9db89-223">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="9db89-224">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-224">No</span></span> |
| <span data-ttu-id="9db89-225">압축</span><span class="sxs-lookup"><span data-stu-id="9db89-225">compression</span></span> | <span data-ttu-id="9db89-226">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="9db89-227">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="9db89-228">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="9db89-229">[Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="9db89-230">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="9db89-231">fileName 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="9db89-232">partitionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="9db89-232">Using partitionedBy property</span></span>
<span data-ttu-id="9db89-233">이전 섹션에서 설명했듯이 **partitionedBy** 속성, [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 사용하여 시계열 데이터의 동적 folderPath와 filename을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="9db89-234">시계열 데이터 집합, 예약 및 조각에 대해 자세히 이해하려면 [데이터 집합 만들기](data-factory-create-datasets.md), [예약 및 실행](data-factory-scheduling-and-execution.md) 그리고 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="9db89-235">샘플 1:</span><span class="sxs-lookup"><span data-stu-id="9db89-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="9db89-236">이 예제에서 {Slice}는 Data Factory 시스템 변수인 SliceStart의 값(YYYYMMDDHH 형식)으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="9db89-237">SliceStart는 조각의 시작 시간을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="9db89-238">folderPath는 각 조각에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="9db89-239">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="9db89-240">샘플 2:</span><span class="sxs-lookup"><span data-stu-id="9db89-240">Sample 2:</span></span>

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

<span data-ttu-id="9db89-241">이 예제에서 SliceStart의 년, 월, 일 및 시는 folderPath 및 fileName 속성에서 사용하는 별도의 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9db89-242">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="9db89-242">Copy activity properties</span></span>
<span data-ttu-id="9db89-243">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9db89-244">이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="9db89-245">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="9db89-246">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="9db89-247">온-프레미스 파일 시스템에서 데이터를 이동하는 경우 복사 작업의 원본 유형을 **FileSystemSource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="9db89-248">온-프레미스 파일 시스템으로 데이터를 이동하는 경우 복사 작업의 싱크 유형을 **FileSystemSink**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="9db89-249">이 섹션에서는 FileSystemSource 및 FileSystemSink에서 지원되는 속성의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="9db89-250">**FileSystemSource**는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="9db89-251">속성</span><span class="sxs-lookup"><span data-stu-id="9db89-251">Property</span></span> | <span data-ttu-id="9db89-252">설명</span><span class="sxs-lookup"><span data-stu-id="9db89-252">Description</span></span> | <span data-ttu-id="9db89-253">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="9db89-253">Allowed values</span></span> | <span data-ttu-id="9db89-254">필수</span><span class="sxs-lookup"><span data-stu-id="9db89-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9db89-255">recursive</span><span class="sxs-lookup"><span data-stu-id="9db89-255">recursive</span></span> |<span data-ttu-id="9db89-256">하위 폴더 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="9db89-257">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="9db89-257">True, False (default)</span></span> |<span data-ttu-id="9db89-258">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-258">No</span></span> |

<span data-ttu-id="9db89-259">**FileSystemSink**에서 지원하는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="9db89-260">속성</span><span class="sxs-lookup"><span data-stu-id="9db89-260">Property</span></span> | <span data-ttu-id="9db89-261">설명</span><span class="sxs-lookup"><span data-stu-id="9db89-261">Description</span></span> | <span data-ttu-id="9db89-262">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="9db89-262">Allowed values</span></span> | <span data-ttu-id="9db89-263">필수</span><span class="sxs-lookup"><span data-stu-id="9db89-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9db89-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="9db89-264">copyBehavior</span></span> |<span data-ttu-id="9db89-265">원본이 BlobSource 또는 FileSystem인 경우 복사 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="9db89-266">**PreserveHierarchy:** 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="9db89-267">즉, 원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="9db89-268">**FlattenHierarchy:** 원본 폴더의 모든 파일이 대상 폴더의 첫 번째 수준에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="9db89-269">대상 파일은 자동 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="9db89-270">**MergeFiles:** 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="9db89-271">병합되는 파일 이름은 지정된 파일 이름/Blob 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="9db89-272">그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="9db89-273">아니요</span><span class="sxs-lookup"><span data-stu-id="9db89-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="9db89-274">recursive 및 copyBehavior 예제</span><span class="sxs-lookup"><span data-stu-id="9db89-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="9db89-275">이 섹션에서는 recursive 및 copyBehavior 값의 다양한 조합에 대한 복사 작업의 결과 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="9db89-276">recursive 값</span><span class="sxs-lookup"><span data-stu-id="9db89-276">recursive value</span></span> | <span data-ttu-id="9db89-277">copyBehavior 값</span><span class="sxs-lookup"><span data-stu-id="9db89-277">copyBehavior value</span></span> | <span data-ttu-id="9db89-278">결과 동작</span><span class="sxs-lookup"><span data-stu-id="9db89-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9db89-279">true</span><span class="sxs-lookup"><span data-stu-id="9db89-279">true</span></span> |<span data-ttu-id="9db89-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="9db89-280">preserveHierarchy</span></span> |<span data-ttu-id="9db89-281">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-282">Folder1</span></span><br/><span data-ttu-id="9db89-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-289">Folder1 대상 폴더가 다음과 같이 원본 폴더와 동일한 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="9db89-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-290">Folder1</span></span><br/><span data-ttu-id="9db89-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="9db89-297">true</span><span class="sxs-lookup"><span data-stu-id="9db89-297">true</span></span> |<span data-ttu-id="9db89-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="9db89-298">flattenHierarchy</span></span> |<span data-ttu-id="9db89-299">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-300">Folder1</span></span><br/><span data-ttu-id="9db89-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-307">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="9db89-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-308">Folder1</span></span><br/><span data-ttu-id="9db89-309">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="9db89-310">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="9db89-311">&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="9db89-312">&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="9db89-313">&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="9db89-314">true</span><span class="sxs-lookup"><span data-stu-id="9db89-314">true</span></span> |<span data-ttu-id="9db89-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="9db89-315">mergeFiles</span></span> |<span data-ttu-id="9db89-316">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-317">Folder1</span></span><br/><span data-ttu-id="9db89-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-324">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="9db89-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-325">Folder1</span></span><br/><span data-ttu-id="9db89-326">&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="9db89-327">false</span><span class="sxs-lookup"><span data-stu-id="9db89-327">false</span></span> |<span data-ttu-id="9db89-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="9db89-328">preserveHierarchy</span></span> |<span data-ttu-id="9db89-329">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-330">Folder1</span></span><br/><span data-ttu-id="9db89-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-337">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9db89-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-338">Folder1</span></span><br/><span data-ttu-id="9db89-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="9db89-341">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="9db89-342">false</span><span class="sxs-lookup"><span data-stu-id="9db89-342">false</span></span> |<span data-ttu-id="9db89-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="9db89-343">flattenHierarchy</span></span> |<span data-ttu-id="9db89-344">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-345">Folder1</span></span><br/><span data-ttu-id="9db89-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-352">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9db89-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-353">Folder1</span></span><br/><span data-ttu-id="9db89-354">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="9db89-355">&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="9db89-356">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="9db89-357">false</span><span class="sxs-lookup"><span data-stu-id="9db89-357">false</span></span> |<span data-ttu-id="9db89-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="9db89-358">mergeFiles</span></span> |<span data-ttu-id="9db89-359">다음과 같은 구조의 Folder1 원본 폴더인 경우</span><span class="sxs-lookup"><span data-stu-id="9db89-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9db89-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-360">Folder1</span></span><br/><span data-ttu-id="9db89-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="9db89-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9db89-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="9db89-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9db89-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9db89-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9db89-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="9db89-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9db89-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9db89-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9db89-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9db89-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9db89-367">Folder1 대상 폴더가 다음과 같은 구조로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9db89-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="9db89-368">Folder1</span></span><br/><span data-ttu-id="9db89-369">&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="9db89-370">&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동 생성된 이름</span><span class="sxs-lookup"><span data-stu-id="9db89-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="9db89-371">File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="9db89-372">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="9db89-372">Supported file and compression formats</span></span>
<span data-ttu-id="9db89-373">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="9db89-374">파일 시스템으로/에서 데이터를 복사하는 JSON 예제</span><span class="sxs-lookup"><span data-stu-id="9db89-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="9db89-375">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공하며,</span><span class="sxs-lookup"><span data-stu-id="9db89-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9db89-376">온-프레미스 파일 시스템과 Azure Blob 저장소 간에 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="9db89-377">그러나 Azure Data Factory의 복사 작업을 사용하면 데이터를 원본에서 [지원되는 원본 및 싱크](data-factory-data-movement-activities.md#supported-data-stores-and-formats)에 나열된 싱크 중 하나로 *직접* 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="9db89-378">예제: 온-프레미스 파일 시스템에서 Azure Blob Storage로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="9db89-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="9db89-379">이 샘플에서는 온-프레미스 파일 시스템에서 Azure Blob 저장소로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="9db89-380">샘플에 포함된 Data Factory 엔터티는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="9db89-381">[OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="9db89-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="9db89-382">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="9db89-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="9db89-383">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="9db89-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="9db89-384">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="9db89-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9db89-385">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9db89-386">여기서는 매시간 시계열 데이터를 온-프레미스 파일 시스템에서 Azure Blob 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="9db89-387">샘플에 사용된 JSON 속성은 샘플 뒤에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="9db89-388">첫 단계로 [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)의 지침에 따라 데이터 관리 게이트웨이를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="9db89-389">**온-프레미스 파일 서버 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9db89-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="9db89-390">**userid** 및 **password** 속성을 사용하는 대신 **encryptedCredential** 속성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="9db89-391">이 연결 서비스에 대한 자세한 내용은 [파일 서버 연결 서비스](#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="9db89-392">**Azure 저장소 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9db89-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="9db89-393">**온-프레미스 파일 시스템 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9db89-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="9db89-394">데이터는 매시간 새 파일에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="9db89-395">folderPath 및 fileName 속성은 조각의 시작 시간에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="9db89-396">`"external": "true"`로 설정하면 데이터 집합이 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="9db89-397">**Azure Blob 저장소 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9db89-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="9db89-398">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="9db89-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9db89-399">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9db89-400">폴더 경로는 시작 시간의 년, 월, 일 및 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="9db89-401">**파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="9db89-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="9db89-402">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="9db89-403">파이프라인 JSON 정의에서 **source** 형식은 **FileSystemSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="9db89-404">예제: Azure SQL Database에서 온-프레미스 파일 시스템으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="9db89-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="9db89-405">다음 샘플은 다음과 같은 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-405">The following sample shows:</span></span>

* <span data-ttu-id="9db89-406">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="9db89-407">[OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="9db89-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="9db89-408">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9db89-409">[FileShare](#dataset-properties) 형식의 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="9db89-410">[SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 및 [FileSystemSink](#copy-activity-properties)를 사용하는 복사 작업의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="9db89-411">이 샘플에서는 매시간 시계열 데이터를 Azure SQL 테이블에서 온-프레미스 파일 시스템으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="9db89-412">샘플에 사용된 JSON 속성은 샘플 뒤에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="9db89-413">**Azure SQL Database 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9db89-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="9db89-414">**온-프레미스 파일 서버 연결 서비스:**</span><span class="sxs-lookup"><span data-stu-id="9db89-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="9db89-415">**userid** 및 **password** 속성을 사용하는 대신 **encryptedCredential** 속성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="9db89-416">이 연결 서비스에 대한 자세한 내용은 [파일 시스템 연결 서비스](#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="9db89-417">**Azure SQL 입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9db89-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="9db89-418">이 샘플에서는 Azure SQL에서 "MyTable" 테이블을 만들었고 이 테이블에 "timestampcolumn"라는 시계열 데이터 열이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="9db89-419">``“external”: ”true”``로 설정하면 데이터 집합이 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="9db89-420">**온-프레미스 파일 시스템 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="9db89-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="9db89-421">데이터는 매시간 새 파일로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="9db89-422">Blob에 대한 folderPath 및 fileName은 조각의 시작 시간에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="9db89-423">**SQL 원본 및 파일 시스템 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="9db89-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="9db89-424">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="9db89-425">파이프라인 JSON 정의에서 **source** 형식은 **SqlSource**로 설정되고 **sink** 형식은 **FileSystemSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="9db89-426">**SqlReaderQuery** 속성에 지정된 SQL 쿼리는 복사할 과거 한 시간의 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="9db89-427">복사 작업 정의에서 원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db89-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="9db89-428">자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9db89-429">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="9db89-429">Performance and tuning</span></span>
 <span data-ttu-id="9db89-430">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 다양한 최적화 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9db89-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
