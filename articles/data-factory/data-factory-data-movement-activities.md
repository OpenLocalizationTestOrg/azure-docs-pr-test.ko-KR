---
title: "복사 작업을 사용 하 여 aaaMove 데이터 | Microsoft Docs"
description: "Data Factory 파이프라인에서 데이터를 이동하는 방법(클라우드 저장소 간/온-프레미스 저장소와 클라우드 저장소 간에 데이터 마이그레이션)에 대해 알아봅니다. 또한 복사 활동을 사용하는 방법을 살펴봅니다."
keywords: "데이터 복사, 데이터 이동, 데이터 마이그레이션, 데이터 전송"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a><span data-ttu-id="2a79e-105">복사 활동을 사용하여 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="2a79e-105">Move data by using Copy Activity</span></span>
## <a name="overview"></a><span data-ttu-id="2a79e-106">개요</span><span class="sxs-lookup"><span data-stu-id="2a79e-106">Overview</span></span>
<span data-ttu-id="2a79e-107">Azure Data Factory에서 온-프레미스와 클라우드 간 toocopy 데이터 복사 작업을 사용할 수 있습니다 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-107">In Azure Data Factory, you can use Copy Activity toocopy data between on-premises and cloud data stores.</span></span> <span data-ttu-id="2a79e-108">Hello 데이터 복사 된 후 추가 변환 하 고 수 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-108">After hello data is copied, it can be further transformed and analyzed.</span></span> <span data-ttu-id="2a79e-109">또한 business intelligence (BI) 및 응용 프로그램 소비에 대 한 복사 작업 toopublish 변환 및 분석 결과 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-109">You can also use Copy Activity toopublish transformation and analysis results for business intelligence (BI) and application consumption.</span></span>

![복사 활동의 역할](media/data-factory-data-movement-activities/copy-activity.png)

<span data-ttu-id="2a79e-111">복사 활동은 안전성, 안전성, 확장성이 뛰어나며 [전 세계에서 사용 가능한 서비스](#global)를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-111">Copy Activity is powered by a secure, reliable, scalable, and [globally available service](#global).</span></span> <span data-ttu-id="2a79e-112">이 문서는 Data Factory 및 복사 작업에서 데이터 이동에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-112">This article provides details on data movement in Data Factory and Copy Activity.</span></span>

<span data-ttu-id="2a79e-113">먼저 두 개의 클라우드 데이터 저장소 간, 그리고 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 이루어지는 데이터 마이그레이션 방식에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-113">First, let's see how data migration occurs between two cloud data stores, and between an on-premises data store and a cloud data store.</span></span>

> [!NOTE]
> <span data-ttu-id="2a79e-114">활동에 대 한 toolearn 일반적으로 참조 [이해 파이프라인 및 활동](data-factory-create-pipelines.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-114">toolearn about activities in general, see [Understanding pipelines and activities](data-factory-create-pipelines.md).</span></span>
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a><span data-ttu-id="2a79e-115">두 클라우드 데이터 저장소 간의 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2a79e-115">Copy data between two cloud data stores</span></span>
<span data-ttu-id="2a79e-116">소스와 싱크 데이터 저장소 hello 클라우드의 경우 복사 작업은 hello 소스 toohello 싱크에서 같은 단계 toocopy 데이터가 hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-116">When both source and sink data stores are in hello cloud, Copy Activity goes through hello following stages toocopy data from hello source toohello sink.</span></span> <span data-ttu-id="2a79e-117">복사 작업을 구동 하는 hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="2a79e-117">hello service that powers Copy Activity:</span></span>

1. <span data-ttu-id="2a79e-118">Hello 원본 데이터 저장소에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-118">Reads data from hello source data store.</span></span>
2. <span data-ttu-id="2a79e-119">직렬화/역직렬화, 압축/압축 해제, 열 매핑 및 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-119">Performs serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="2a79e-120">Hello 입력된 데이터 집합, 출력 데이터 집합 및 복사 작업의 hello 구성에 따라 이러한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-120">It does these operations based on hello configurations of hello input dataset, output dataset, and Copy Activity.</span></span>
3. <span data-ttu-id="2a79e-121">데이터 toohello 대상 데이터 저장소를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-121">Writes data toohello destination data store.</span></span>

<span data-ttu-id="2a79e-122">hello 서비스는 hello 최적의 지역 tooperform hello 데이터 이동을 자동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-122">hello service automatically chooses hello optimal region tooperform hello data movement.</span></span> <span data-ttu-id="2a79e-123">이 영역은 일반적으로 hello 한 가장 가까운 toohello 싱크 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-123">This region is usually hello one closest toohello sink data store.</span></span>

![클라우드 간 복사](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="2a79e-125">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2a79e-125">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="2a79e-126">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 toosecurely 이동 데이터가 온-프레미스 컴퓨터에 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-126">toosecurely move data between an on-premises data store and a cloud data store, install Data Management Gateway on your on-premises machine.</span></span> <span data-ttu-id="2a79e-127">데이터 관리 게이트웨이는 하이브리드 데이터 이동 및 처리를 수행할 수 있도록 하는 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-127">Data Management Gateway is an agent that enables hybrid data movement and processing.</span></span> <span data-ttu-id="2a79e-128">Hello hello 데이터 저장소에서 자체 하므로 동일한 컴퓨터 또는 저장 toohello 데이터 액세스를 가진 별도 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-128">You can install it on hello same machine as hello data store itself, or on a separate machine that has access toohello data store.</span></span>

<span data-ttu-id="2a79e-129">이 시나리오에서는 데이터 관리 게이트웨이 hello serialization/deserialization, 압축/압축 풀기, 열 매핑를 실행 하 고 형식 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-129">In this scenario, Data Management Gateway performs hello serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="2a79e-130">데이터는 hello Azure 데이터 팩터리 서비스를 통해 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-130">Data does not flow through hello Azure Data Factory service.</span></span> <span data-ttu-id="2a79e-131">대신, 데이터 관리 게이트웨이 hello 데이터 toohello 대상 저장소를 직접 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-131">Instead, Data Management Gateway directly writes hello data toohello destination store.</span></span>

![온-프레미스 및 클라우드 간 복사](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

<span data-ttu-id="2a79e-133">데이터 이동에 대한 소개와 연습은 [온-프레미스 및 클라우드 데이터 저장소 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-133">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) for an introduction and walkthrough.</span></span> <span data-ttu-id="2a79e-134">이 에이전트에 대한 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-134">See [Data Management Gateway](data-factory-data-management-gateway.md) for detailed information about this agent.</span></span>

<span data-ttu-id="2a79e-135">데이터를 이동할 수도 있습니다 / toosupported 데이터를 저장 하는 데이터 관리 게이트웨이 사용 하 여 Azure IaaS 가상 컴퓨터 (Vm)에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-135">You can also move data from/toosupported data stores that are hosted on Azure IaaS virtual machines (VMs) by using Data Management Gateway.</span></span> <span data-ttu-id="2a79e-136">이 경우에 데이터 관리 게이트웨이 설치할 수 있습니다 hello 데이터 저장소 자체에서 또는 저장 toohello 데이터 액세스를 가진 별도 VM에서 동일한 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-136">In this case, you can install Data Management Gateway on hello same VM as hello data store itself, or on a separate VM that has access toohello data store.</span></span>

## <a name="supported-data-stores-and-formats"></a><span data-ttu-id="2a79e-137">지원되는 데이터 저장소 및 형식</span><span class="sxs-lookup"><span data-stu-id="2a79e-137">Supported data stores and formats</span></span>
<span data-ttu-id="2a79e-138">복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-138">Copy Activity in Data Factory copies data from a source data store tooa sink data store.</span></span> <span data-ttu-id="2a79e-139">데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-139">Data Factory supports hello following data stores.</span></span> <span data-ttu-id="2a79e-140">데이터 소스에서 tooany 싱크를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-140">Data from any source can be written tooany sink.</span></span> <span data-ttu-id="2a79e-141">데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-141">Click a data store toolearn how toocopy data tooand from that store.</span></span>

> [!NOTE] 
> <span data-ttu-id="2a79e-142">Toomove 데이터 복사 작업을 지원 하지 않는 데이터 저장소에서 필요한 경우 사용 된 **사용자 지정 활동** 를 데이터 복사/이동 하기 위한 사용자 논리로 데이터 팩터리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-142">If you need toomove data to/from a data store that Copy Activity doesn't support, use a **custom activity** in Data Factory with your own logic for copying/moving data.</span></span> <span data-ttu-id="2a79e-143">사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-143">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="2a79e-144">데이터 저장소와 * 온-프레미스 될 수 있습니다 또는 Azure IaaS에서 고 tooinstall 있어야 하며 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 에-프레미스/Azure IaaS 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-144">Data stores with * can be on-premises or on Azure IaaS, and require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="supported-file-formats"></a><span data-ttu-id="2a79e-145">지원 파일 형식</span><span class="sxs-lookup"><span data-stu-id="2a79e-145">Supported file formats</span></span>
<span data-ttu-id="2a79e-146">복사 작업에도 사용할 수 있습니다**파일을 다음으로 복사-은** 두 파일 기반 데이터 저장소 간의 hello를 건너뛸 수 있습니다 [섹션 서식을](data-factory-create-datasets.md) 에 모두 hello 입력 및 출력 데이터 집합의 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-146">You can use Copy Activity too**copy files as-is** between two file-based data stores, you can skip hello [format section](data-factory-create-datasets.md) in both hello input and output dataset definitions.</span></span> <span data-ttu-id="2a79e-147">hello 데이터가 모든 직렬화/역직렬화 하지 않고 효율적으로 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-147">hello data is copied efficiently without any serialization/deserialization.</span></span>

<span data-ttu-id="2a79e-148">복사 활동도에서 읽고 씁니다 toofiles 지정 된 형식으로: **텍스트, JSON, Avro, ORC, 및 Parquet**, 및 압축 코덱 **GZip, Deflate, BZip2 및 ZipDeflate** 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-148">Copy Activity also reads from and writes toofiles in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span></span> <span data-ttu-id="2a79e-149">자세한 내용은 [지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-149">See [Supported file and compression formats](data-factory-supported-file-and-compression-formats.md) with details.</span></span>

<span data-ttu-id="2a79e-150">수행할 수는 예를 들어 hello 다음 활동을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-150">For example, you can do hello following copy activities:</span></span>

* <span data-ttu-id="2a79e-151">온-프레미스 SQL Server에서 데이터를 복사한 ORC 형식에서 tooAzure 데이터 레이크 저장소를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-151">Copy data in on-premises SQL Server and write tooAzure Data Lake Store in ORC format.</span></span>
* <span data-ttu-id="2a79e-152">온-프레미스 파일 시스템에서 텍스트 (CSV) 형식에서 파일을 복사 하 고 Avro 형식에서 tooAzure Blob를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-152">Copy files in text (CSV) format from on-premises File System and write tooAzure Blob in Avro format.</span></span>
* <span data-ttu-id="2a79e-153">온-프레미스 파일 시스템에서 압축 된 파일을 복사 하 고 압축을 푸는 다음 tooAzure 데이터 레이크 저장소를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-153">Copy zipped files from on-premises File System and decompress then land tooAzure Data Lake Store.</span></span>
* <span data-ttu-id="2a79e-154">Azure Blob에서 GZip 압축 된 텍스트 (CSV) 형식으로 데이터를 복사 하 고 tooAzure SQL 데이터베이스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-154">Copy data in GZip compressed text (CSV) format from Azure Blob and write tooAzure SQL Database.</span></span>

## <span data-ttu-id="2a79e-155"><a name="global"></a>전역적으로 사용 가능한 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="2a79e-155"><a name="global"></a>Globally available data movement</span></span>
<span data-ttu-id="2a79e-156">Azure 데이터 팩터리는 hello 미국 서 부, 미국 동부 및 북부 유럽 지역 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-156">Azure Data Factory is available only in hello West US, East US, and North Europe regions.</span></span> <span data-ttu-id="2a79e-157">그러나 복사 작업을 구동 하는 hello 서비스는 hello에서 전체적으로 사용할 수 있는 영역 및 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-157">However, hello service that powers Copy Activity is available globally in hello following regions and geographies.</span></span> <span data-ttu-id="2a79e-158">hello 전체적으로 사용 가능한 토폴로지는 일반적으로 지역 간 홉을 방지 하는 효율적인 데이터 이동이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-158">hello globally available topology ensures efficient data movement that usually avoids cross-region hops.</span></span> <span data-ttu-id="2a79e-159">지역별 Data Factory 및 데이터 이동 기능 사용 가능 여부는 [지역별 서비스](https://azure.microsoft.com/regions/#services) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-159">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span></span>

### <a name="copy-data-between-cloud-data-stores"></a><span data-ttu-id="2a79e-160">클라우드 데이터 저장소 간의 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2a79e-160">Copy data between cloud data stores</span></span>
<span data-ttu-id="2a79e-161">데이터 팩터리 서비스 배포를 사용 하 여 hello에 가장 가까운 toohello 싱크가 hello 영역의 hello 클라우드 데이터 저장소를 원본 및 싱크를 같은 지리 toomove hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-161">When both source and sink data stores are in hello cloud, Data Factory uses a service deployment in hello region that is closest toohello sink in hello same geography toomove hello data.</span></span> <span data-ttu-id="2a79e-162">Toohello 다음 매핑에 대 한 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2a79e-162">Refer toohello following table for mapping:</span></span>

| <span data-ttu-id="2a79e-163">Hello 대상 데이터 저장소의 지리적 위치</span><span class="sxs-lookup"><span data-stu-id="2a79e-163">Geography of hello destination data stores</span></span> | <span data-ttu-id="2a79e-164">Hello 대상 데이터 저장소의 지역</span><span class="sxs-lookup"><span data-stu-id="2a79e-164">Region of hello destination data store</span></span> | <span data-ttu-id="2a79e-165">데이터 이동에 사용되는 지역</span><span class="sxs-lookup"><span data-stu-id="2a79e-165">Region used for data movement</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2a79e-166">미국</span><span class="sxs-lookup"><span data-stu-id="2a79e-166">United States</span></span> | <span data-ttu-id="2a79e-167">미국 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-167">East US</span></span> | <span data-ttu-id="2a79e-168">미국 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-168">East US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-169">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="2a79e-169">East US 2</span></span> | <span data-ttu-id="2a79e-170">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="2a79e-170">East US 2</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-171">미국 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-171">Central US</span></span> | <span data-ttu-id="2a79e-172">미국 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-172">Central US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-173">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="2a79e-173">North Central US</span></span> | <span data-ttu-id="2a79e-174">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="2a79e-174">North Central US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-175">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-175">South Central US</span></span> | <span data-ttu-id="2a79e-176">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-176">South Central US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-177">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-177">West Central US</span></span> | <span data-ttu-id="2a79e-178">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-178">West Central US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-179">미국 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-179">West US</span></span> | <span data-ttu-id="2a79e-180">미국 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-180">West US</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-181">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="2a79e-181">West US 2</span></span> | <span data-ttu-id="2a79e-182">미국 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-182">West US</span></span> |
| <span data-ttu-id="2a79e-183">캐나다</span><span class="sxs-lookup"><span data-stu-id="2a79e-183">Canada</span></span> | <span data-ttu-id="2a79e-184">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-184">Canada East</span></span> | <span data-ttu-id="2a79e-185">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-185">Canada Central</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-186">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-186">Canada Central</span></span> | <span data-ttu-id="2a79e-187">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-187">Canada Central</span></span> |
| <span data-ttu-id="2a79e-188">브라질</span><span class="sxs-lookup"><span data-stu-id="2a79e-188">Brazil</span></span> | <span data-ttu-id="2a79e-189">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-189">Brazil South</span></span> | <span data-ttu-id="2a79e-190">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-190">Brazil South</span></span> |
| <span data-ttu-id="2a79e-191">유럽</span><span class="sxs-lookup"><span data-stu-id="2a79e-191">Europe</span></span> | <span data-ttu-id="2a79e-192">북유럽</span><span class="sxs-lookup"><span data-stu-id="2a79e-192">North Europe</span></span> | <span data-ttu-id="2a79e-193">북유럽</span><span class="sxs-lookup"><span data-stu-id="2a79e-193">North Europe</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-194">서유럽</span><span class="sxs-lookup"><span data-stu-id="2a79e-194">West Europe</span></span> | <span data-ttu-id="2a79e-195">서유럽</span><span class="sxs-lookup"><span data-stu-id="2a79e-195">West Europe</span></span> |
| <span data-ttu-id="2a79e-196">영국</span><span class="sxs-lookup"><span data-stu-id="2a79e-196">United Kingdom</span></span> | <span data-ttu-id="2a79e-197">영국 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-197">UK West</span></span> | <span data-ttu-id="2a79e-198">영국 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-198">UK South</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-199">영국 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-199">UK South</span></span> | <span data-ttu-id="2a79e-200">영국 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-200">UK South</span></span> |
| <span data-ttu-id="2a79e-201">아시아 태평양</span><span class="sxs-lookup"><span data-stu-id="2a79e-201">Asia Pacific</span></span> | <span data-ttu-id="2a79e-202">동남아시아</span><span class="sxs-lookup"><span data-stu-id="2a79e-202">Southeast Asia</span></span> | <span data-ttu-id="2a79e-203">동남아시아</span><span class="sxs-lookup"><span data-stu-id="2a79e-203">Southeast Asia</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-204">동아시아</span><span class="sxs-lookup"><span data-stu-id="2a79e-204">East Asia</span></span> | <span data-ttu-id="2a79e-205">동남아시아</span><span class="sxs-lookup"><span data-stu-id="2a79e-205">Southeast Asia</span></span> |
| <span data-ttu-id="2a79e-206">오스트레일리아</span><span class="sxs-lookup"><span data-stu-id="2a79e-206">Australia</span></span> | <span data-ttu-id="2a79e-207">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-207">Australia East</span></span> | <span data-ttu-id="2a79e-208">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-208">Australia East</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-209">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-209">Australia Southeast</span></span> | <span data-ttu-id="2a79e-210">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-210">Australia Southeast</span></span> |
| <span data-ttu-id="2a79e-211">일본</span><span class="sxs-lookup"><span data-stu-id="2a79e-211">Japan</span></span> | <span data-ttu-id="2a79e-212">일본 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-212">Japan East</span></span> | <span data-ttu-id="2a79e-213">일본 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-213">Japan East</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-214">일본 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-214">Japan West</span></span> | <span data-ttu-id="2a79e-215">일본 동부</span><span class="sxs-lookup"><span data-stu-id="2a79e-215">Japan East</span></span> |
| <span data-ttu-id="2a79e-216">인도</span><span class="sxs-lookup"><span data-stu-id="2a79e-216">India</span></span> | <span data-ttu-id="2a79e-217">인도 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-217">Central India</span></span> | <span data-ttu-id="2a79e-218">인도 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-218">Central India</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-219">인도 서부</span><span class="sxs-lookup"><span data-stu-id="2a79e-219">West India</span></span> | <span data-ttu-id="2a79e-220">인도 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-220">Central India</span></span> |
| &nbsp; | <span data-ttu-id="2a79e-221">인도 남부</span><span class="sxs-lookup"><span data-stu-id="2a79e-221">South India</span></span> | <span data-ttu-id="2a79e-222">인도 중부</span><span class="sxs-lookup"><span data-stu-id="2a79e-222">Central India</span></span> |

<span data-ttu-id="2a79e-223">또는 나타낼 수 있습니다 명시적으로 지정 하 여 tooperform hello 복사본을 사용 하는 데이터 팩터리 서비스 toobe의 hello 영역 `executionLocation` 복사 작업에서 속성 `typeProperties`합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-223">Alternatively, you can explicitly indicate hello region of Data Factory service toobe used tooperform hello copy by specifying `executionLocation` property under Copy Activity `typeProperties`.</span></span> <span data-ttu-id="2a79e-224">이 속성에 대한 지원되는 값은 위의 **데이터 이동에 사용되는 지역** 열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-224">Supported values for this property are listed in above **Region used for data movement** column.</span></span> <span data-ttu-id="2a79e-225">데이터를 거칩니다 해당 지역의 hello 유선으로 복사 하는 동안 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-225">Note your data goes through that region over hello wire during copy.</span></span> <span data-ttu-id="2a79e-226">예를 들어 Azure 간의 toocopy 저장 한국를 지정할 수 있습니다 `"executionLocation": "Japan East"` 일본 영역을 통해 tooroute (참조 [JSON 샘플](#by-using-json-scripts) 참조로).</span><span class="sxs-lookup"><span data-stu-id="2a79e-226">For example, toocopy between Azure stores in Korea, you can specify `"executionLocation": "Japan East"` tooroute through Japan region (see [sample JSON](#by-using-json-scripts) as reference).</span></span>

> [!NOTE]
> <span data-ttu-id="2a79e-227">Hello 대상 데이터 저장소의 hello 영역 앞의 목록에 없거나 또는 검색할 수 없는 경우, 기본적으로 복사 작업은 대체 지역을 통하지 않고 하지 않으면 실패 하는 경우 `executionLocation` 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-227">If hello region of hello destination data store is not in preceding list or undetectable, by default Copy Activity fails instead of going through an alternative region, unless `executionLocation` is specified.</span></span> <span data-ttu-id="2a79e-228">지원 되는 hello 지역 목록 시간에 따라 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-228">hello supported region list will be expanded over time.</span></span>
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="2a79e-229">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2a79e-229">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="2a79e-230">온-프레미스 또는 Azure Virtual Machines/IaaS와 클라우드 저장소 간에 데이터를 복사할 때 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 는 온-프레미스 컴퓨터 또는 Virtual Machines에서 데이터 이동을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-230">When data is being copied between on-premises (or Azure virtual machines/IaaS) and cloud stores, [Data Management Gateway](data-factory-data-management-gateway.md) performs data movement on an on-premises machine or virtual machine.</span></span> <span data-ttu-id="2a79e-231">hello를 사용 하지 않는 한 hello 데이터 hello 클라우드에서 hello 서비스를 통해 이동 하지 않는 [복사본을 스테이징](data-factory-copy-activity-performance.md#staged-copy) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-231">hello data does not flow through hello service in hello cloud, unless you use hello [staged copy](data-factory-copy-activity-performance.md#staged-copy) capability.</span></span> <span data-ttu-id="2a79e-232">이 경우 데이터 hello 싱크 데이터 저장소에 기록 되기 전에 Azure Blob 저장소를 준비 하는 hello 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-232">In this case, data flows through hello staging Azure Blob storage before it is written into hello sink data store.</span></span>

## <a name="create-a-pipeline-with-copy-activity"></a><span data-ttu-id="2a79e-233">복사 활동을 포함하는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="2a79e-233">Create a pipeline with Copy Activity</span></span>
<span data-ttu-id="2a79e-234">두 가지 방법을 통해 복사 활동을 포함하는 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-234">You can create a pipeline with Copy Activity in a couple of ways:</span></span>

### <a name="by-using-hello-copy-wizard"></a><span data-ttu-id="2a79e-235">Hello 복사 마법사를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2a79e-235">By using hello Copy Wizard</span></span>
<span data-ttu-id="2a79e-236">데이터 팩터리 복사 마법사 hello toocreate 파이프라인 복사 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-236">hello Data Factory Copy Wizard helps you toocreate a pipeline with Copy Activity.</span></span> <span data-ttu-id="2a79e-237">이 파이프라인에서 지원 되는 소스 toodestinations toocopy 데이터를 사용 하면 *JSON을 작성 하지 않고도* 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-237">This pipeline allows you toocopy data from supported sources toodestinations *without writing JSON* definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="2a79e-238">참조 [데이터 팩터리 복사 마법사](data-factory-copy-wizard.md) hello 마법사에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-238">See [Data Factory Copy Wizard](data-factory-copy-wizard.md) for details about hello wizard.</span></span>  

### <a name="by-using-json-scripts"></a><span data-ttu-id="2a79e-239">JSON 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="2a79e-239">By using JSON scripts</span></span>
<span data-ttu-id="2a79e-240">(사용 하 여 복사 작업)는 파이프라인에 대 한 hello Azure 포털, Visual Studio 또는 Azure PowerShell toocreate JSON 정의에서 데이터 팩터리 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-240">You can use Data Factory Editor in hello Azure portal, Visual Studio, or Azure PowerShell toocreate a JSON definition for a pipeline (by using Copy Activity).</span></span> <span data-ttu-id="2a79e-241">그런 다음 데이터 팩터리에서 toocreate hello 파이프라인 것 것을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-241">Then, you can deploy it toocreate hello pipeline in Data Factory.</span></span> <span data-ttu-id="2a79e-242">단계별 지침이 포함된 자습서는 [자습서: Azure Data Factory 파이프라인에서 복사 활동 사용](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-242">See [Tutorial: Use Copy Activity in an Azure Data Factory pipeline](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a tutorial with step-by-step instructions.</span></span>    

<span data-ttu-id="2a79e-243">이름, 설명, 입력/출력 테이블, 정책 등의 JSON 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-243">JSON properties (such as name, description, input and output tables, and policies) are available for all types of activities.</span></span> <span data-ttu-id="2a79e-244">Hello에서 사용할 수 있는 속성 `typeProperties` hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-244">Properties that are available in hello `typeProperties` section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="2a79e-245">복사 작업에 대 한 hello `typeProperties` 섹션 hello 유형의 원본에 따라 다르며 싱크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-245">For Copy Activity, hello `typeProperties` section varies depending on hello types of sources and sinks.</span></span> <span data-ttu-id="2a79e-246">Hello에는 원본/싱크 클릭 [원본 및 싱크를 지원](#supported-data-stores-and-formats) 해당 데이터 저장소에 대 한 복사 작업을 지원 합니다. 형식 속성에 대 한 섹션 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-246">Click a source/sink in hello [Supported sources and sinks](#supported-data-stores-and-formats) section toolearn about type properties that Copy Activity supports for that data store.</span></span>

<span data-ttu-id="2a79e-247">샘플 JSON 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-247">Here's a sample JSON definition:</span></span>

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
<span data-ttu-id="2a79e-248">hello에 정의 된 hello 일정 출력 데이터 집합 결정 hello 활동 실행 하는 경우 (예: **매일**와 빈도 **일**, 및 간격으로 **1**).</span><span class="sxs-lookup"><span data-stu-id="2a79e-248">hello schedule that is defined in hello output dataset determines when hello activity runs (for example: **daily**, frequency as **day**, and interval as **1**).</span></span> <span data-ttu-id="2a79e-249">hello 활동에서에서 데이터를 복사 된 입력된 데이터 집합 (**소스**) tooan 출력 데이터 집합 (**싱크**).</span><span class="sxs-lookup"><span data-stu-id="2a79e-249">hello activity copies data from an input dataset (**source**) tooan output dataset (**sink**).</span></span>

<span data-ttu-id="2a79e-250">둘 이상의 입력된 데이터 집합 tooCopy 활동을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-250">You can specify more than one input dataset tooCopy Activity.</span></span> <span data-ttu-id="2a79e-251">서로 hello 활동이 실행 되기 전에 사용 되는 tooverify hello 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-251">They are used tooverify hello dependencies before hello activity is run.</span></span> <span data-ttu-id="2a79e-252">그러나 hello 첫 번째 데이터 집합의 hello 데이터만 복사 toohello 대상 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-252">However, only hello data from hello first dataset is copied toohello destination dataset.</span></span> <span data-ttu-id="2a79e-253">자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-253">For more information, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>  

## <a name="performance-and-tuning"></a><span data-ttu-id="2a79e-254">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="2a79e-254">Performance and tuning</span></span>
<span data-ttu-id="2a79e-255">Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 설명 하는 Azure Data Factory에서 데이터 이동 (복사 작업)의 hello 성능에 영향을 주는 주요 요인입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-255">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md), which describes key factors that affect hello performance of data movement (Copy Activity) in Azure Data Factory.</span></span> <span data-ttu-id="2a79e-256">또한 내부 테스트 중에 성능을 관찰 된 hello를 나열 하 고 복사 작업의 다양 한 방법으로 toooptimize hello 성능에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-256">It also lists hello observed performance during internal testing and discusses various ways toooptimize hello performance of Copy Activity.</span></span>

## <a name="fault-tolerance"></a><span data-ttu-id="2a79e-257">내결함성</span><span class="sxs-lookup"><span data-stu-id="2a79e-257">Fault tolerance</span></span>
<span data-ttu-id="2a79e-258">데이터 및 반환 오류 복사 복사 작업은 중지 하는 기본적으로 원본 및 싱크; 간에 호환 되지 않는 데이터를 발견 하면 tooskip 및 로그 hello 호환 되지 않는 행과 복사본만 명시적으로 구성할 수도 있지만 이러한 호환 되는 데이터 toomake hello 복사가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-258">By default, copy activity will stop copying data and return failure when encounter incompatible data between source and sink; while you can explicitly configure tooskip and log hello incompatible rows and only copy those compatible data toomake hello copy succeeded.</span></span> <span data-ttu-id="2a79e-259">Hello 참조 [복사 활동 내결함성](data-factory-copy-activity-fault-tolerance.md) 자세한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="2a79e-259">See hello [Copy Activity fault tolerance](data-factory-copy-activity-fault-tolerance.md) on more details.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="2a79e-260">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2a79e-260">Security considerations</span></span>
<span data-ttu-id="2a79e-261">Hello 참조 [보안 고려 사항](data-factory-data-movement-security-considerations.md), Azure Data Factory에서 데이터 이동 서비스를 있는지 toosecure 데이터를 사용 하는 보안 인프라를 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-261">See hello [Security considerations](data-factory-data-movement-security-considerations.md), which describes security infrastructure that data movement services in Azure Data Factory use toosecure your data.</span></span>

## <a name="scheduling-and-sequential-copy"></a><span data-ttu-id="2a79e-262">예약 및 순차 복사</span><span class="sxs-lookup"><span data-stu-id="2a79e-262">Scheduling and sequential copy</span></span>
<span data-ttu-id="2a79e-263">Data Factory에서 예약 및 실행이 작동하는 방식에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a79e-263">See [Scheduling and execution](data-factory-scheduling-and-execution.md) for detailed information about how scheduling and execution works in Data Factory.</span></span> <span data-ttu-id="2a79e-264">것은 가능한 toorun 여러 복사 작업 차례로 정렬/순차적 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-264">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="2a79e-265">Hello 참조 [순차적으로 복사](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) 섹션.</span><span class="sxs-lookup"><span data-stu-id="2a79e-265">See hello [Copy sequentially](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) section.</span></span>

## <a name="type-conversions"></a><span data-ttu-id="2a79e-266">형식 변환</span><span class="sxs-lookup"><span data-stu-id="2a79e-266">Type conversions</span></span>
<span data-ttu-id="2a79e-267">다른 데이터 저장소에는 서로 다른 네이티브 형식 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-267">Different data stores have different native type systems.</span></span> <span data-ttu-id="2a79e-268">복사 작업에는 2 단계 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-268">Copy Activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="2a79e-269">네이티브 소스 형식 tooa.NET 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-269">Convert from native source types tooa .NET type.</span></span>
2. <span data-ttu-id="2a79e-270">.NET 형식 tooa 네이티브 싱크 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-270">Convert from a .NET type tooa native sink type.</span></span>

<span data-ttu-id="2a79e-271">데이터 저장소에 대 한 네이티브 형식 시스템 tooa.NET 유형에 서 hello 매핑 hello 각 데이터 저장소 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-271">hello mapping from a native type system tooa .NET type for a data store is in hello respective data store article.</span></span> <span data-ttu-id="2a79e-272">(Hello hello 특정 링크를 클릭 [데이터 저장소를 지원](#supported-data-stores) 테이블).</span><span class="sxs-lookup"><span data-stu-id="2a79e-272">(Click hello specific link in hello [Supported data stores](#supported-data-stores) table).</span></span> <span data-ttu-id="2a79e-273">복사 활동 hello 오른쪽 변환을 수행 되도록 테이블을 만드는 동안 이러한 매핑 toodetermine 적절 한 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-273">You can use these mappings toodetermine appropriate types while creating your tables, so that Copy Activity performs hello right conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a79e-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a79e-274">Next steps</span></span>
* <span data-ttu-id="2a79e-275">toolearn hello 더 복사 작업에 대 한 참조 [Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-275">toolearn about hello Copy Activity more, see [Copy data from Azure Blob storage tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="2a79e-276">온-프레미스 데이터 저장소 tooa 클라우드 데이터 저장소에서 데이터를 이동 하는 방법에 대 한 toolearn 참조 [온-프레미스 toocloud 데이터 저장소에서 데이터를 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a79e-276">toolearn about moving data from an on-premises data store tooa cloud data store, see [Move data from on-premises toocloud data stores](data-factory-move-data-between-onprem-and-cloud.md).</span></span>
