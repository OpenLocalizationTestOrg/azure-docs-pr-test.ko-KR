---
title: "온-프레미스 HDFS에서 aaaMove 데이터 | Microsoft Docs"
description: "어떻게 toomove 데이터를 온-프레미스 Azure 데이터 팩터리를 사용 하 여 HDFS에 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="a7c1d-103">Azure Data Factory를 사용하여 온-프레미스 HDFS에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="a7c1d-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="a7c1d-104">이 문서에서는 toouse 온-프레미스 HDFS에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="a7c1d-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a7c1d-106">HDFS 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="a7c1d-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a7c1d-108">데이터 팩터리의 현재에서 온-프레미스 HDFS tooother 데이터 저장소만 이동 데이터를 지원 하지만 다른 데이터에서 데이터 이동에 대해 저장소 tooan 온-프레미스 HDFS 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c1d-109">복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="a7c1d-110">성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="a7c1d-111">연결 사용</span><span class="sxs-lookup"><span data-stu-id="a7c1d-111">Enabling connectivity</span></span>
<span data-ttu-id="a7c1d-112">데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 HDFS 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="a7c1d-113">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="a7c1d-114">Azure IaaS VM에서 호스팅되는 경우에 게이트웨이 tooconnect tooHDFS hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c1d-115">데이터 관리 게이트웨이에 너무 액세스할 수 있는지 hello를 확인**모든** hello [노드 서버 이름]: [노드 포트 이름을] 및 [데이터 노드 서버]: [데이터 노드 포트] hello Hadoop 클러스터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="a7c1d-116">기본 [이름 노드 포트]는 50070이며 기본 [데이터 노드 포트]는 50075입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="a7c1d-117">Hello에 게이트웨이 설치할 수 있지만 동일한 온-프레미스 컴퓨터 또는 Azure VM hello HDFS hello, 별도 컴퓨터/Azure IaaS VM에 hello 게이트웨이 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="a7c1d-118">별도의 컴퓨터에 게이트웨이가 있으면 리소스 경합이 줄어들고 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="a7c1d-119">별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 HDFS hello 사용 하 여 수 tooaccess hello 컴퓨터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a7c1d-120">시작</span><span class="sxs-lookup"><span data-stu-id="a7c1d-120">Getting started</span></span>
<span data-ttu-id="a7c1d-121">다른 도구/API를 사용하여 HDFS 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="a7c1d-122">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a7c1d-123">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="a7c1d-124">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a7c1d-125">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="a7c1d-126">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a7c1d-127">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a7c1d-128">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="a7c1d-129">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="a7c1d-130">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a7c1d-131">도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a7c1d-132">Data Factory 된 엔터티를 HDFS에 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: 온-프레미스 HDFS tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="a7c1d-133">다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooHDFS는 JSON 속성에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a7c1d-134">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-134">Linked service properties</span></span>
<span data-ttu-id="a7c1d-135">연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="a7c1d-136">형식의 연결 된 서비스를 만들면 **Hdfs** toolink는 온-프레미스 HDFS tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="a7c1d-137">다음 표에서 hello JSON 요소 특정 tooHDFS 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="a7c1d-138">속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-138">Property</span></span> | <span data-ttu-id="a7c1d-139">설명</span><span class="sxs-lookup"><span data-stu-id="a7c1d-139">Description</span></span> | <span data-ttu-id="a7c1d-140">필수</span><span class="sxs-lookup"><span data-stu-id="a7c1d-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7c1d-141">type</span><span class="sxs-lookup"><span data-stu-id="a7c1d-141">type</span></span> |<span data-ttu-id="a7c1d-142">hello type 속성 설정 해야 합니다: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="a7c1d-143">예</span><span class="sxs-lookup"><span data-stu-id="a7c1d-143">Yes</span></span> |
| <span data-ttu-id="a7c1d-144">Url</span><span class="sxs-lookup"><span data-stu-id="a7c1d-144">Url</span></span> |<span data-ttu-id="a7c1d-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="a7c1d-145">URL toohello HDFS</span></span> |<span data-ttu-id="a7c1d-146">예</span><span class="sxs-lookup"><span data-stu-id="a7c1d-146">Yes</span></span> |
| <span data-ttu-id="a7c1d-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a7c1d-147">authenticationType</span></span> |<span data-ttu-id="a7c1d-148">익명 또는 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="a7c1d-149">toouse **Kerberos 인증** HDFS 커넥터에 대 한 참조 너무[이 여기서](#use-kerberos-authentication-for-hdfs-connector) 온-프레미스 환경을 tooset 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="a7c1d-150">예</span><span class="sxs-lookup"><span data-stu-id="a7c1d-150">Yes</span></span> |
| <span data-ttu-id="a7c1d-151">userName</span><span class="sxs-lookup"><span data-stu-id="a7c1d-151">userName</span></span> |<span data-ttu-id="a7c1d-152">Windows 인증에 대한 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-152">Username for Windows authentication.</span></span> |<span data-ttu-id="a7c1d-153">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a7c1d-154">password</span><span class="sxs-lookup"><span data-stu-id="a7c1d-154">password</span></span> |<span data-ttu-id="a7c1d-155">Windows 인증에 대한 암호.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-155">Password for Windows authentication.</span></span> |<span data-ttu-id="a7c1d-156">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a7c1d-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a7c1d-157">gatewayName</span></span> |<span data-ttu-id="a7c1d-158">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello HDFS 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="a7c1d-159">예</span><span class="sxs-lookup"><span data-stu-id="a7c1d-159">Yes</span></span> |
| <span data-ttu-id="a7c1d-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a7c1d-160">encryptedCredential</span></span> |<span data-ttu-id="a7c1d-161">[새 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 액세스 자격 증명의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="a7c1d-162">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a7c1d-163">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a7c1d-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="a7c1d-164">Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a7c1d-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="a7c1d-165">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-165">Dataset properties</span></span>
<span data-ttu-id="a7c1d-166">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a7c1d-167">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="a7c1d-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a7c1d-168">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a7c1d-169">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **FileShare** hello 다음과 같은 속성에 (HDFS 데이터 집합 포함)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="a7c1d-170">속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-170">Property</span></span> | <span data-ttu-id="a7c1d-171">설명</span><span class="sxs-lookup"><span data-stu-id="a7c1d-171">Description</span></span> | <span data-ttu-id="a7c1d-172">필수</span><span class="sxs-lookup"><span data-stu-id="a7c1d-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7c1d-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="a7c1d-173">folderPath</span></span> |<span data-ttu-id="a7c1d-174">경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-174">Path toohello folder.</span></span> <span data-ttu-id="a7c1d-175">예: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="a7c1d-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="a7c1d-176">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="a7c1d-177">예: 폴더\하위 폴더의 경우 폴더\\\\하위 폴더를 지정하고 d:\samplefolder의 경우 d:\\\\samplefolder를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="a7c1d-178">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="a7c1d-179">예</span><span class="sxs-lookup"><span data-stu-id="a7c1d-179">Yes</span></span> |
| <span data-ttu-id="a7c1d-180">fileName</span><span class="sxs-lookup"><span data-stu-id="a7c1d-180">fileName</span></span> |<span data-ttu-id="a7c1d-181">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="a7c1d-182">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="a7c1d-183">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="a7c1d-184">Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="a7c1d-185">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-185">No</span></span> |
| <span data-ttu-id="a7c1d-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="a7c1d-186">partitionedBy</span></span> |<span data-ttu-id="a7c1d-187">partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="a7c1d-188">예를 들어 folderPath는 매시간 데이터에 대해 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="a7c1d-189">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-189">No</span></span> |
| <span data-ttu-id="a7c1d-190">format</span><span class="sxs-lookup"><span data-stu-id="a7c1d-190">format</span></span> | <span data-ttu-id="a7c1d-191">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a7c1d-192">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a7c1d-193">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a7c1d-194">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a7c1d-195">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-195">No</span></span> |
| <span data-ttu-id="a7c1d-196">압축</span><span class="sxs-lookup"><span data-stu-id="a7c1d-196">compression</span></span> | <span data-ttu-id="a7c1d-197">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a7c1d-198">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a7c1d-199">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a7c1d-200">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a7c1d-201">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="a7c1d-202">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="a7c1d-203">partionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="a7c1d-203">Using partionedBy property</span></span>
<span data-ttu-id="a7c1d-204">동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="a7c1d-205">시간 시계열 데이터 집합, 일정 및 분할에 대해 자세히 toolearn 참조 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="a7c1d-206">샘플 1:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="a7c1d-207">이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="a7c1d-208">hello SliceStart hello 조각의 toostart 시간을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="a7c1d-209">hello folderPath 각 조각에 대 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="a7c1d-210">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="a7c1d-211">샘플 2:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-211">Sample 2:</span></span>

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
<span data-ttu-id="a7c1d-212">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a7c1d-213">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-213">Copy activity properties</span></span>
<span data-ttu-id="a7c1d-214">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a7c1d-215">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a7c1d-216">반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a7c1d-217">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a7c1d-218">원본 유형인 경우 복사 작업에 대 한 **FileSystemSource** 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="a7c1d-219">**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="a7c1d-220">속성</span><span class="sxs-lookup"><span data-stu-id="a7c1d-220">Property</span></span> | <span data-ttu-id="a7c1d-221">설명</span><span class="sxs-lookup"><span data-stu-id="a7c1d-221">Description</span></span> | <span data-ttu-id="a7c1d-222">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="a7c1d-222">Allowed values</span></span> | <span data-ttu-id="a7c1d-223">필수</span><span class="sxs-lookup"><span data-stu-id="a7c1d-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7c1d-224">recursive</span><span class="sxs-lookup"><span data-stu-id="a7c1d-224">recursive</span></span> |<span data-ttu-id="a7c1d-225">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="a7c1d-226">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-226">True, False (default)</span></span> |<span data-ttu-id="a7c1d-227">아니요</span><span class="sxs-lookup"><span data-stu-id="a7c1d-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a7c1d-228">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="a7c1d-228">Supported file and compression formats</span></span>
<span data-ttu-id="a7c1d-229">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="a7c1d-230">JSON의 예: 온-프레미스 HDFS tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="a7c1d-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="a7c1d-231">이 샘플은 어떻게 온-프레미스 HDFS tooAzure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="a7c1d-232">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="a7c1d-233">hello 예제 Data Factory 엔터티에 따라 hello에 대 한 JSON 정의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="a7c1d-234">이러한 정의 toocreate HDFS tooAzure Blob 저장소에서에서 파이프라인 toocopy 데이터를 사용 하 여 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="a7c1d-235">[OnPremisesHdfs](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="a7c1d-236">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="a7c1d-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a7c1d-237">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="a7c1d-238">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a7c1d-239">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a7c1d-240">hello 샘플 데이터 복사 온-프레미스 HDFS tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="a7c1d-241">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a7c1d-242">첫 번째 단계로 hello 데이터 관리 게이트웨이를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="a7c1d-243">hello에 대 한 지침을 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a7c1d-244">**연결 된 서비스 HDFS:** 이 예제를 사용 하 여 hello Windows 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="a7c1d-245">사용할 수 있는 다른 유형의 인증은 [HDFS 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="a7c1d-246">**Azure 저장소 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="a7c1d-247">**HDFS 입력 데이터 집합:** 이 데이터 집합 참조 toohello HDFS 폴더 DataTransfer/UnitTest/합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="a7c1d-248">hello 파이프라인이 폴더 toohello 대상의 모든 hello 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="a7c1d-249">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="a7c1d-250">**Azure Blob 출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a7c1d-251">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="a7c1d-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a7c1d-252">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a7c1d-253">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a7c1d-254">**파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="a7c1d-255">복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a7c1d-256">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a7c1d-257">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="a7c1d-258">HDFS 커넥터에 Kerberos 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a7c1d-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="a7c1d-259">따라서 HDFS 커넥터에서 Kerberos 인증 toouse로 hello 온-프레미스 환경을 옵션 tooset 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="a7c1d-260">하나는 hello 케이스를 더 잘 맞게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="a7c1d-261">옵션 1: [게이트웨이 컴퓨터를 Kerberos 영역에 가입](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="a7c1d-262">옵션 2: [Windows 도메인과 Kerberos 영역 사이에 상호 트러스트를 사용하도록 설정](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="a7c1d-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="a7c1d-263"><a name="kerberos-join-realm"></a>옵션 1: 게이트웨이 컴퓨터를 Kerberos 영역에 가입</span><span class="sxs-lookup"><span data-stu-id="a7c1d-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a7c1d-264">요구 사항:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-264">Requirement:</span></span>

* <span data-ttu-id="a7c1d-265">hello 게이트웨이 컴퓨터 toojoin hello Kerberos 영역 하며 모든 Windows 도메인에 가입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a7c1d-266">어떻게 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-266">How tooconfigure:</span></span>

<span data-ttu-id="a7c1d-267">**게이트웨이 컴퓨터에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="a7c1d-268">Hello 실행 **Ksetup** 유틸리티 tooconfigure hello Kerberos KDC 서버 및 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="a7c1d-269">hello 컴퓨터 Kerberos 영역은 Windows 도메인에서 다른 작업 그룹의 구성원으로 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="a7c1d-270">Hello Kerberos 영역을 설정 하 고 다음과 같이 KDC 서버 추가 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="a7c1d-271">*REALM.COM*은 고유한 각 영역으로 필요에 맞게 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="a7c1d-272">**다시 시작** 2 이러한 명령을 실행 한 후 hello 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="a7c1d-273">사용 하 여 hello 구성을 확인 **Ksetup** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="a7c1d-274">hello 출력은 같은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="a7c1d-275">**Azure Data Factory에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a7c1d-276">사용 하 여 hello HDFS 커넥터 구성 **Windows 인증** Kerberos 보안 주체 이름 및 암호 tooconnect toohello HDFS 데이터 소스와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a7c1d-277">구성 세부 정보에서 [HDFS 연결된 서비스 속성](#linked-service-properties)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="a7c1d-278"><a name="kerberos-mutual-trust"></a>옵션 2: Windows 도메인과 Kerberos 영역 사이에 상호 트러스트를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a7c1d-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a7c1d-279">요구 사항:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-279">Requirement:</span></span>
*   <span data-ttu-id="a7c1d-280">hello 게이트웨이 컴퓨터에 Windows 도메인에 참가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="a7c1d-281">사용 권한 tooupdate hello 도메인 컨트롤러 설정 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a7c1d-282">어떻게 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="a7c1d-283">필요에 따라 사용자 고유의 각 영역과 도메인 컨트롤러와 자습서를 따라 hello에과 같습니다 및 AD.COM를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="a7c1d-284">**KDC 서버에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="a7c1d-285">hello KDC 구성을 편집 **krb5.conf** 파일 toolet KDC toohello 다음 구성 템플릿을 참조 하는 Windows 도메인을 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="a7c1d-286">기본적으로 hello 구성에 위치한 **/etc/krb5.conf**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="a7c1d-287">**다시 시작** KDC 서비스 구성 후 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="a7c1d-288">라는 보안 주체를 준비  **krbtgt/REALM.COM@AD.COM**  다음 명령을 hello로 KDC 서버에서:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="a7c1d-289">**hadoop.security.auth_to_local** HDFS 서비스 구성 파일에서 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="a7c1d-290">**도메인 컨트롤러에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="a7c1d-291">Hello 다음 실행 **Ksetup** tooadd 영역 항목 명령:</span><span class="sxs-lookup"><span data-stu-id="a7c1d-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="a7c1d-292">Windows 도메인 tooKerberos 영역 트러스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="a7c1d-293">[암호]는 hello 주체에 대 한 hello 암호  **krbtgt/REALM.COM@AD.COM** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="a7c1d-294">Kerberos에서 사용되는 암호화 알고리즘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="a7c1d-295">이동 tooServer 관리자 > 그룹 정책 관리 > 도메인 > 그룹 정책 개체 > 기본 또는 활성 도메인 정책 및 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="a7c1d-296">Hello에 **그룹 정책 관리 편집기** 팝업 창 이동 tooComputer 구성 > 정책 > Windows 설정 > 보안 설정 > 로컬 정책 > 보안 옵션을 구성 하 고 **네트워크 보안: Kerberos에 대해 허용 되는 암호화 유형 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="a7c1d-297">선택 hello 암호화 알고리즘을 toouse tooKDC를 연결 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="a7c1d-298">일반적으로 모든 hello 옵션 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-298">Commonly, you can simply select all hello options.</span></span>

        ![Kerberos의 암호화 유형 구성](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="a7c1d-300">사용 하 여 **Ksetup** 명령 toospecify hello 암호화 알고리즘 toobe hello에 사용 되는 특정 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="a7c1d-301">순서 toouse Kerberos 주체 Windows 도메인의 보안 주체 hello 도메인 계정 및 Kerberos 간의 hello 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="a7c1d-302">Hello 관리 도구를 시작 > **Active Directory 사용자 및 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="a7c1d-303">**보기** > **고급 기능**을 클릭하여 고급 기능을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="a7c1d-304">Hello 계정 toowhich toocreate 매핑의 tooview를 마우스 오른쪽 단추로 클릭 찾을 **이름 매핑** > 클릭 **Kerberos 이름** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="a7c1d-305">Hello 영역에서 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-305">Add a principal from hello realm.</span></span>

        ![보안 ID 매핑](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="a7c1d-307">**게이트웨이 컴퓨터에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-307">**On gateway machine:**</span></span>

* <span data-ttu-id="a7c1d-308">Hello 다음 실행 **Ksetup** tooadd 영역 항목 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="a7c1d-309">**Azure Data Factory에서:**</span><span class="sxs-lookup"><span data-stu-id="a7c1d-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a7c1d-310">사용 하 여 hello HDFS 커넥터 구성 **Windows 인증** 도메인 계정이 나 Kerberos 주체 tooconnect toohello HDFS 데이터 소스와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a7c1d-311">구성 세부 정보에서 [HDFS 연결된 서비스 속성](#linked-service-properties)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="a7c1d-312">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="a7c1d-313">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="a7c1d-313">Performance and Tuning</span></span>
<span data-ttu-id="a7c1d-314">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c1d-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
