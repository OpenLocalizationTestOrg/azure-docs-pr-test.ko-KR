---
title: "복사 작업을 사용하여 데이터 이동 | Microsoft 문서"
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
ms.openlocfilehash: 0cefbe1303de1cfa46cc4b771c0cd3aa7819597c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-by-using-copy-activity"></a><span data-ttu-id="6481e-105">복사 활동을 사용하여 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="6481e-105">Move data by using Copy Activity</span></span>
## <a name="overview"></a><span data-ttu-id="6481e-106">개요</span><span class="sxs-lookup"><span data-stu-id="6481e-106">Overview</span></span>
<span data-ttu-id="6481e-107">Azure Data Factory에서는 복사 작업을 사용해 온-프레미스 및 클라우드 데이터 저장소 간에 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-107">In Azure Data Factory, you can use Copy Activity to copy data between on-premises and cloud data stores.</span></span> <span data-ttu-id="6481e-108">복사한 데이터는 추가로 변환하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-108">After the data is copied, it can be further transformed and analyzed.</span></span> <span data-ttu-id="6481e-109">복사 활동을 통해 BI(비즈니스 인텔리전스) 및 응용 프로그램에서 사용할 수 있도록 변환 및 분석 결과를 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-109">You can also use Copy Activity to publish transformation and analysis results for business intelligence (BI) and application consumption.</span></span>

![복사 활동의 역할](media/data-factory-data-movement-activities/copy-activity.png)

<span data-ttu-id="6481e-111">복사 활동은 안전성, 안전성, 확장성이 뛰어나며 [전 세계에서 사용 가능한 서비스](#global)를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-111">Copy Activity is powered by a secure, reliable, scalable, and [globally available service](#global).</span></span> <span data-ttu-id="6481e-112">이 문서는 Data Factory 및 복사 작업에서 데이터 이동에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-112">This article provides details on data movement in Data Factory and Copy Activity.</span></span>

<span data-ttu-id="6481e-113">먼저 두 개의 클라우드 데이터 저장소 간, 그리고 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 이루어지는 데이터 마이그레이션 방식에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-113">First, let's see how data migration occurs between two cloud data stores, and between an on-premises data store and a cloud data store.</span></span>

> [!NOTE]
> <span data-ttu-id="6481e-114">활동과 관련된 전반적인 정보를 살펴보려면 [파이프라인 및 활동 이해](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-114">To learn about activities in general, see [Understanding pipelines and activities](data-factory-create-pipelines.md).</span></span>
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a><span data-ttu-id="6481e-115">두 클라우드 데이터 저장소 간의 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6481e-115">Copy data between two cloud data stores</span></span>
<span data-ttu-id="6481e-116">소스 및 싱크 데이터 저장소가 모두 클라우드에 있는 경우 복사 활동은 다음 단계를 통해 소스에서 싱크로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-116">When both source and sink data stores are in the cloud, Copy Activity goes through the following stages to copy data from the source to the sink.</span></span> <span data-ttu-id="6481e-117">복사 활동을 제공하는 서비스가 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-117">The service that powers Copy Activity:</span></span>

1. <span data-ttu-id="6481e-118">소스 데이터 저장소에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-118">Reads data from the source data store.</span></span>
2. <span data-ttu-id="6481e-119">직렬화/역직렬화, 압축/압축 해제, 열 매핑 및 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-119">Performs serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="6481e-120">이러한 작업은 입력 데이터 집합, 출력 데이터 집합 및 복사 활동의 구성에 따라 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-120">It does these operations based on the configurations of the input dataset, output dataset, and Copy Activity.</span></span>
3. <span data-ttu-id="6481e-121">대상 데이터 저장소에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-121">Writes data to the destination data store.</span></span>

<span data-ttu-id="6481e-122">서비스는 데이터 이동을 수행할 최적의 지역을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-122">The service automatically chooses the optimal region to perform the data movement.</span></span> <span data-ttu-id="6481e-123">이 지역은 대개 싱크 데이터 저장소와 가장 가까운 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-123">This region is usually the one closest to the sink data store.</span></span>

![클라우드 간 복사](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="6481e-125">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6481e-125">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="6481e-126">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터를 안전하게 이동하려면 온-프레미스 컴퓨터에 데이터 관리 게이트웨이를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-126">To securely move data between an on-premises data store and a cloud data store, install Data Management Gateway on your on-premises machine.</span></span> <span data-ttu-id="6481e-127">데이터 관리 게이트웨이는 하이브리드 데이터 이동 및 처리를 수행할 수 있도록 하는 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-127">Data Management Gateway is an agent that enables hybrid data movement and processing.</span></span> <span data-ttu-id="6481e-128">게이트웨이는 데이터 저장소 자체와 같은 컴퓨터에 설치할 수도 있고, 데이터 저장소에 액세스할 수 있는 별도의 컴퓨터에 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-128">You can install it on the same machine as the data store itself, or on a separate machine that has access to the data store.</span></span>

<span data-ttu-id="6481e-129">이 시나리오에서는 데이터 관리 게이트웨이가 직렬화/역직렬화, 압축/압축 해제, 열 매핑 및 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-129">In this scenario, Data Management Gateway performs the serialization/deserialization, compression/decompression, column mapping, and type conversion.</span></span> <span data-ttu-id="6481e-130">데이터는 Azure Data Factory 서비스를 통과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-130">Data does not flow through the Azure Data Factory service.</span></span> <span data-ttu-id="6481e-131">대신 데이터 관리 게이트웨이가 데이터를 대상 저장소에 직접 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-131">Instead, Data Management Gateway directly writes the data to the destination store.</span></span>

![온-프레미스 및 클라우드 간 복사](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

<span data-ttu-id="6481e-133">데이터 이동에 대한 소개와 연습은 [온-프레미스 및 클라우드 데이터 저장소 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-133">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) for an introduction and walkthrough.</span></span> <span data-ttu-id="6481e-134">이 에이전트에 대한 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-134">See [Data Management Gateway](data-factory-data-management-gateway.md) for detailed information about this agent.</span></span>

<span data-ttu-id="6481e-135">데이터 관리 게이트웨이를 사용하여 Azure IaaS VM(Virtual Machines)에서 호스트되는 지원되는 데이터 저장소 간에 데이터를 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-135">You can also move data from/to supported data stores that are hosted on Azure IaaS virtual machines (VMs) by using Data Management Gateway.</span></span> <span data-ttu-id="6481e-136">이 경우 데이터 관리 게이트웨이는 데이터 저장소 자체와 같은 VM에 설치할 수도 있고, 데이터 저장소에 액세스할 수 있는 별도의 VM에 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-136">In this case, you can install Data Management Gateway on the same VM as the data store itself, or on a separate VM that has access to the data store.</span></span>

## <a name="supported-data-stores-and-formats"></a><span data-ttu-id="6481e-137">지원되는 데이터 저장소 및 형식</span><span class="sxs-lookup"><span data-stu-id="6481e-137">Supported data stores and formats</span></span>
<span data-ttu-id="6481e-138">데이터 팩터리의 복사 활동은 원본 데이터 저장소의 데이터를 싱크 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-138">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span></span> <span data-ttu-id="6481e-139">Data Factory는 다음과 같은 데이터 저장소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-139">Data Factory supports the following data stores.</span></span> <span data-ttu-id="6481e-140">모든 소스의 데이터를 모든 싱크에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-140">Data from any source can be written to any sink.</span></span> <span data-ttu-id="6481e-141">데이터 저장소를 클릭하면 해당 저장소에서/저장소로 데이터를 복사하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-141">Click a data store to learn how to copy data to and from that store.</span></span>

> [!NOTE] 
> <span data-ttu-id="6481e-142">복사 활동에서 지원되지 않는 데이터 저장소에서/데이터 저장소로 데이터를 이동해야 하는 경우 데이터 복사/이동을 위한 자체 논리가 포함된 **사용자 지정 활동** 을 Data Factory에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-142">If you need to move data to/from a data store that Copy Activity doesn't support, use a **custom activity** in Data Factory with your own logic for copying/moving data.</span></span> <span data-ttu-id="6481e-143">사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-143">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="6481e-144">*가 있는 데이터 저장소는 온-프레미스 또는 Azure IaaS에 있을 수 있으며 온-프레미스/Azure IaaS 컴퓨터에 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-144">Data stores with * can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

### <a name="supported-file-formats"></a><span data-ttu-id="6481e-145">지원 파일 형식</span><span class="sxs-lookup"><span data-stu-id="6481e-145">Supported file formats</span></span>
<span data-ttu-id="6481e-146">복사 활동을 사용해서 파일 기반 데이터 저장소 간에 **파일을 있는 그대로 복사**하고, 입력 및 출력 데이터 집합 정의 둘 다에서 [형식 섹션](data-factory-create-datasets.md)을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-146">You can use Copy Activity to **copy files as-is** between two file-based data stores, you can skip the [format section](data-factory-create-datasets.md) in both the input and output dataset definitions.</span></span> <span data-ttu-id="6481e-147">그러면 데이터가 직렬화/역직렬화되지 않고 효율적으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-147">The data is copied efficiently without any serialization/deserialization.</span></span>

<span data-ttu-id="6481e-148">복사 작업은 지정된 형식의 파일에서 읽고 씁니다. **텍스트, JSON, Avro, ORC 및 Parquet**, 압축 코덱 **GZip, Deflate, BZip2 및 ZipDeflate**가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-148">Copy Activity also reads from and writes to files in specified formats: **Text, JSON, Avro, ORC, and Parquet**, and compression codec **GZip, Deflate, BZip2, and ZipDeflate** are supported.</span></span> <span data-ttu-id="6481e-149">자세한 내용은 [지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-149">See [Supported file and compression formats](data-factory-supported-file-and-compression-formats.md) with details.</span></span>

<span data-ttu-id="6481e-150">예를 들어 다음 복사 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-150">For example, you can do the following copy activities:</span></span>

* <span data-ttu-id="6481e-151">온-프레미스 SQL Server에서 데이터를 복사하여 ORC 형식으로 Azure Data Lake Store에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-151">Copy data in on-premises SQL Server and write to Azure Data Lake Store in ORC format.</span></span>
* <span data-ttu-id="6481e-152">온-프레미스 파일 시스템에서 텍스트(CSV) 형식의 파일을 복사하여 Avro 형식으로 Azure Blob에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-152">Copy files in text (CSV) format from on-premises File System and write to Azure Blob in Avro format.</span></span>
* <span data-ttu-id="6481e-153">온-프레미스 파일 시스템에서 압축된 파일을 복사하고 압축을 푼 다음 Azure Data Lake Store에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-153">Copy zipped files from on-premises File System and decompress then land to Azure Data Lake Store.</span></span>
* <span data-ttu-id="6481e-154">Azure Blob에서 GZip 압축 텍스트(CSV) 형식의 데이터를 복사하여 Azure SQL Database에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-154">Copy data in GZip compressed text (CSV) format from Azure Blob and write to Azure SQL Database.</span></span>

## <span data-ttu-id="6481e-155"><a name="global"></a>전역적으로 사용 가능한 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="6481e-155"><a name="global"></a>Globally available data movement</span></span>
<span data-ttu-id="6481e-156">Azure Data Factory는 미국 서부, 미국 동부 및 북유럽 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-156">Azure Data Factory is available only in the West US, East US, and North Europe regions.</span></span> <span data-ttu-id="6481e-157">그러나 복사 작업을 지원하는 서비스는 다음과 같은 지역 및 지리에서 전역적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-157">However, the service that powers Copy Activity is available globally in the following regions and geographies.</span></span> <span data-ttu-id="6481e-158">전역적으로 사용 가능한 토폴로지에서는 대개 지역 간 홉이 없는 효율적인 데이터 이동이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-158">The globally available topology ensures efficient data movement that usually avoids cross-region hops.</span></span> <span data-ttu-id="6481e-159">지역별 Data Factory 및 데이터 이동 기능 사용 가능 여부는 [지역별 서비스](https://azure.microsoft.com/regions/#services) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-159">See [Services by region](https://azure.microsoft.com/regions/#services) for availability of Data Factory and Data Movement in a region.</span></span>

### <a name="copy-data-between-cloud-data-stores"></a><span data-ttu-id="6481e-160">클라우드 데이터 저장소 간의 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6481e-160">Copy data between cloud data stores</span></span>
<span data-ttu-id="6481e-161">원본 및 싱크 데이터 저장소가 모두 클라우드에 있는 경우, Data Factory는 데이터 이동을 수행하기 위해 동일한 지역의 싱크 위치에 가장 가까운 지역에서 서비스 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-161">When both source and sink data stores are in the cloud, Data Factory uses a service deployment in the region that is closest to the sink in the same geography to move the data.</span></span> <span data-ttu-id="6481e-162">매핑은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-162">Refer to the following table for mapping:</span></span>

| <span data-ttu-id="6481e-163">대상 데이터 저장소의 지리적 위치</span><span class="sxs-lookup"><span data-stu-id="6481e-163">Geography of the destination data stores</span></span> | <span data-ttu-id="6481e-164">대상 데이터 저장소의 지역</span><span class="sxs-lookup"><span data-stu-id="6481e-164">Region of the destination data store</span></span> | <span data-ttu-id="6481e-165">데이터 이동에 사용되는 지역</span><span class="sxs-lookup"><span data-stu-id="6481e-165">Region used for data movement</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6481e-166">미국</span><span class="sxs-lookup"><span data-stu-id="6481e-166">United States</span></span> | <span data-ttu-id="6481e-167">미국 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-167">East US</span></span> | <span data-ttu-id="6481e-168">미국 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-168">East US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-169">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="6481e-169">East US 2</span></span> | <span data-ttu-id="6481e-170">미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="6481e-170">East US 2</span></span> |
| &nbsp; | <span data-ttu-id="6481e-171">미국 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-171">Central US</span></span> | <span data-ttu-id="6481e-172">미국 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-172">Central US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-173">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="6481e-173">North Central US</span></span> | <span data-ttu-id="6481e-174">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="6481e-174">North Central US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-175">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="6481e-175">South Central US</span></span> | <span data-ttu-id="6481e-176">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="6481e-176">South Central US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-177">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="6481e-177">West Central US</span></span> | <span data-ttu-id="6481e-178">미국 중서부</span><span class="sxs-lookup"><span data-stu-id="6481e-178">West Central US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-179">미국 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-179">West US</span></span> | <span data-ttu-id="6481e-180">미국 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-180">West US</span></span> |
| &nbsp; | <span data-ttu-id="6481e-181">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="6481e-181">West US 2</span></span> | <span data-ttu-id="6481e-182">미국 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-182">West US</span></span> |
| <span data-ttu-id="6481e-183">캐나다</span><span class="sxs-lookup"><span data-stu-id="6481e-183">Canada</span></span> | <span data-ttu-id="6481e-184">캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-184">Canada East</span></span> | <span data-ttu-id="6481e-185">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-185">Canada Central</span></span> |
| &nbsp; | <span data-ttu-id="6481e-186">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-186">Canada Central</span></span> | <span data-ttu-id="6481e-187">캐나다 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-187">Canada Central</span></span> |
| <span data-ttu-id="6481e-188">브라질</span><span class="sxs-lookup"><span data-stu-id="6481e-188">Brazil</span></span> | <span data-ttu-id="6481e-189">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-189">Brazil South</span></span> | <span data-ttu-id="6481e-190">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-190">Brazil South</span></span> |
| <span data-ttu-id="6481e-191">유럽</span><span class="sxs-lookup"><span data-stu-id="6481e-191">Europe</span></span> | <span data-ttu-id="6481e-192">북유럽</span><span class="sxs-lookup"><span data-stu-id="6481e-192">North Europe</span></span> | <span data-ttu-id="6481e-193">북유럽</span><span class="sxs-lookup"><span data-stu-id="6481e-193">North Europe</span></span> |
| &nbsp; | <span data-ttu-id="6481e-194">서유럽</span><span class="sxs-lookup"><span data-stu-id="6481e-194">West Europe</span></span> | <span data-ttu-id="6481e-195">서유럽</span><span class="sxs-lookup"><span data-stu-id="6481e-195">West Europe</span></span> |
| <span data-ttu-id="6481e-196">영국</span><span class="sxs-lookup"><span data-stu-id="6481e-196">United Kingdom</span></span> | <span data-ttu-id="6481e-197">영국 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-197">UK West</span></span> | <span data-ttu-id="6481e-198">영국 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-198">UK South</span></span> |
| &nbsp; | <span data-ttu-id="6481e-199">영국 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-199">UK South</span></span> | <span data-ttu-id="6481e-200">영국 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-200">UK South</span></span> |
| <span data-ttu-id="6481e-201">아시아 태평양</span><span class="sxs-lookup"><span data-stu-id="6481e-201">Asia Pacific</span></span> | <span data-ttu-id="6481e-202">동남아시아</span><span class="sxs-lookup"><span data-stu-id="6481e-202">Southeast Asia</span></span> | <span data-ttu-id="6481e-203">동남아시아</span><span class="sxs-lookup"><span data-stu-id="6481e-203">Southeast Asia</span></span> |
| &nbsp; | <span data-ttu-id="6481e-204">동아시아</span><span class="sxs-lookup"><span data-stu-id="6481e-204">East Asia</span></span> | <span data-ttu-id="6481e-205">동남아시아</span><span class="sxs-lookup"><span data-stu-id="6481e-205">Southeast Asia</span></span> |
| <span data-ttu-id="6481e-206">오스트레일리아</span><span class="sxs-lookup"><span data-stu-id="6481e-206">Australia</span></span> | <span data-ttu-id="6481e-207">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-207">Australia East</span></span> | <span data-ttu-id="6481e-208">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-208">Australia East</span></span> |
| &nbsp; | <span data-ttu-id="6481e-209">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="6481e-209">Australia Southeast</span></span> | <span data-ttu-id="6481e-210">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="6481e-210">Australia Southeast</span></span> |
| <span data-ttu-id="6481e-211">일본</span><span class="sxs-lookup"><span data-stu-id="6481e-211">Japan</span></span> | <span data-ttu-id="6481e-212">일본 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-212">Japan East</span></span> | <span data-ttu-id="6481e-213">일본 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-213">Japan East</span></span> |
| &nbsp; | <span data-ttu-id="6481e-214">일본 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-214">Japan West</span></span> | <span data-ttu-id="6481e-215">일본 동부</span><span class="sxs-lookup"><span data-stu-id="6481e-215">Japan East</span></span> |
| <span data-ttu-id="6481e-216">인도</span><span class="sxs-lookup"><span data-stu-id="6481e-216">India</span></span> | <span data-ttu-id="6481e-217">인도 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-217">Central India</span></span> | <span data-ttu-id="6481e-218">인도 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-218">Central India</span></span> |
| &nbsp; | <span data-ttu-id="6481e-219">인도 서부</span><span class="sxs-lookup"><span data-stu-id="6481e-219">West India</span></span> | <span data-ttu-id="6481e-220">인도 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-220">Central India</span></span> |
| &nbsp; | <span data-ttu-id="6481e-221">인도 남부</span><span class="sxs-lookup"><span data-stu-id="6481e-221">South India</span></span> | <span data-ttu-id="6481e-222">인도 중부</span><span class="sxs-lookup"><span data-stu-id="6481e-222">Central India</span></span> |

<span data-ttu-id="6481e-223">또는 복사 작업 `typeProperties`에서 `executionLocation` 속성을 지정하여 복사를 수행하는 데 사용할 Data Factory 서비스의 지역을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-223">Alternatively, you can explicitly indicate the region of Data Factory service to be used to perform the copy by specifying `executionLocation` property under Copy Activity `typeProperties`.</span></span> <span data-ttu-id="6481e-224">이 속성에 대한 지원되는 값은 위의 **데이터 이동에 사용되는 지역** 열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-224">Supported values for this property are listed in above **Region used for data movement** column.</span></span> <span data-ttu-id="6481e-225">데이터는 복사 동안 유선을 통해 해당 하위 지역으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-225">Note your data goes through that region over the wire during copy.</span></span> <span data-ttu-id="6481e-226">예를 들어 영국의 Azure 저장소 간을 복사하려면 `"executionLocation": "Japan East"`를 지정하여 일본을 통해 라우팅되도록 할 수 있습니다([샘플 JSON](#by-using-json-scripts) 참조).</span><span class="sxs-lookup"><span data-stu-id="6481e-226">For example, to copy between Azure stores in Korea, you can specify `"executionLocation": "Japan East"` to route through Japan region (see [sample JSON](#by-using-json-scripts) as reference).</span></span>

> [!NOTE]
> <span data-ttu-id="6481e-227">대상 데이터 저장소의 지역이 위의 목록에 없거나 검색 가능하지 않을 경우 `executionLocation`을 지정하지 않을 경우 기본적으로 복사 작업이 대체 지역을 거치지 않고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-227">If the region of the destination data store is not in preceding list or undetectable, by default Copy Activity fails instead of going through an alternative region, unless `executionLocation` is specified.</span></span> <span data-ttu-id="6481e-228">지원되는 지역 목록은 시간이 지남에 따라 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-228">The supported region list will be expanded over time.</span></span>
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a><span data-ttu-id="6481e-229">온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="6481e-229">Copy data between an on-premises data store and a cloud data store</span></span>
<span data-ttu-id="6481e-230">온-프레미스 또는 Azure Virtual Machines/IaaS와 클라우드 저장소 간에 데이터를 복사할 때 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 는 온-프레미스 컴퓨터 또는 Virtual Machines에서 데이터 이동을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-230">When data is being copied between on-premises (or Azure virtual machines/IaaS) and cloud stores, [Data Management Gateway](data-factory-data-management-gateway.md) performs data movement on an on-premises machine or virtual machine.</span></span> <span data-ttu-id="6481e-231">[준비된 복사](data-factory-copy-activity-performance.md#staged-copy) 기능을 사용하는 경우가 아니면 이 데이터는 클라우드의 서비스를 통과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-231">The data does not flow through the service in the cloud, unless you use the [staged copy](data-factory-copy-activity-performance.md#staged-copy) capability.</span></span> <span data-ttu-id="6481e-232">이 경우 데이터는 스테이징 Azure Blob 저장소를 통과한 후 싱크 데이터 저장소에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-232">In this case, data flows through the staging Azure Blob storage before it is written into the sink data store.</span></span>

## <a name="create-a-pipeline-with-copy-activity"></a><span data-ttu-id="6481e-233">복사 활동을 포함하는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="6481e-233">Create a pipeline with Copy Activity</span></span>
<span data-ttu-id="6481e-234">두 가지 방법을 통해 복사 활동을 포함하는 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-234">You can create a pipeline with Copy Activity in a couple of ways:</span></span>

### <a name="by-using-the-copy-wizard"></a><span data-ttu-id="6481e-235">복사 마법사 사용</span><span class="sxs-lookup"><span data-stu-id="6481e-235">By using the Copy Wizard</span></span>
<span data-ttu-id="6481e-236">Data Factory 복사 마법사를 사용하면 복사 활동을 포함하는 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-236">The Data Factory Copy Wizard helps you to create a pipeline with Copy Activity.</span></span> <span data-ttu-id="6481e-237">이 파이프라인에서는 연결된 서비스, 데이터 집합 및 파이프라인에 대한 *JSON 정의를 작성하지 않고도* 지원되는 소스에서 대상으로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-237">This pipeline allows you to copy data from supported sources to destinations *without writing JSON* definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="6481e-238">마법사에 대한 자세한 내용은 [Data Factory 복사 마법사](data-factory-copy-wizard.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-238">See [Data Factory Copy Wizard](data-factory-copy-wizard.md) for details about the wizard.</span></span>  

### <a name="by-using-json-scripts"></a><span data-ttu-id="6481e-239">JSON 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="6481e-239">By using JSON scripts</span></span>
<span data-ttu-id="6481e-240">Azure 포털, Visual Studio 또는 Azure PowerShell에서 Data Factory Editor를 사용하여 복사 활동을 통해 파이프라인에 대한 JSON 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-240">You can use Data Factory Editor in the Azure portal, Visual Studio, or Azure PowerShell to create a JSON definition for a pipeline (by using Copy Activity).</span></span> <span data-ttu-id="6481e-241">그런 다음 해당 정의를 배포하여 Data Factory에서 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-241">Then, you can deploy it to create the pipeline in Data Factory.</span></span> <span data-ttu-id="6481e-242">단계별 지침이 포함된 자습서는 [자습서: Azure Data Factory 파이프라인에서 복사 활동 사용](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-242">See [Tutorial: Use Copy Activity in an Azure Data Factory pipeline](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a tutorial with step-by-step instructions.</span></span>    

<span data-ttu-id="6481e-243">이름, 설명, 입력/출력 테이블, 정책 등의 JSON 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-243">JSON properties (such as name, description, input and output tables, and policies) are available for all types of activities.</span></span> <span data-ttu-id="6481e-244">활동의 `typeProperties` 섹션에서 사용 가능한 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-244">Properties that are available in the `typeProperties` section of the activity vary with each activity type.</span></span>

<span data-ttu-id="6481e-245">복사 활동의 경우 `typeProperties` 섹션은 원본 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-245">For Copy Activity, the `typeProperties` section varies depending on the types of sources and sinks.</span></span> <span data-ttu-id="6481e-246">해당 데이터 저장소에 대한 복사 활동에서 지원하는 형식 속성에 대해 알아보려면 [지원되는 소스 및 싱크](#supported-data-stores-and-formats) 섹션에서 소스/싱크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-246">Click a source/sink in the [Supported sources and sinks](#supported-data-stores-and-formats) section to learn about type properties that Copy Activity supports for that data store.</span></span>

<span data-ttu-id="6481e-247">샘플 JSON 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-247">Here's a sample JSON definition:</span></span>

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob to Azure SQL table",
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
<span data-ttu-id="6481e-248">출력 데이터 집합에 정의된 일정은 작업 실행 시기를 결정합니다(예: **매일**, 빈도는 **요일** 및 간격은 **1**).</span><span class="sxs-lookup"><span data-stu-id="6481e-248">The schedule that is defined in the output dataset determines when the activity runs (for example: **daily**, frequency as **day**, and interval as **1**).</span></span> <span data-ttu-id="6481e-249">복사 작업에서는 입력 데이터 집합(**source**)에서 출력 데이터 집합(**sink**)으로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-249">The activity copies data from an input dataset (**source**) to an output dataset (**sink**).</span></span>

<span data-ttu-id="6481e-250">복사 활동에 대해 입력 데이터 집합을 둘 이상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-250">You can specify more than one input dataset to Copy Activity.</span></span> <span data-ttu-id="6481e-251">이러한 데이터 집합은 활동 실행 전에 종속성을 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-251">They are used to verify the dependencies before the activity is run.</span></span> <span data-ttu-id="6481e-252">그러나 첫 번째 데이터 집합의 데이터만 대상 데이터 집합으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-252">However, only the data from the first dataset is copied to the destination dataset.</span></span> <span data-ttu-id="6481e-253">자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-253">For more information, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>  

## <a name="performance-and-tuning"></a><span data-ttu-id="6481e-254">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="6481e-254">Performance and tuning</span></span>
<span data-ttu-id="6481e-255">Azure Data Factory의 데이터 이동(복사 활동) 성능에 영향을 주는 주요 요인에 대해 설명하는 [복사 작업 성능 및 튜닝 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-255">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md), which describes key factors that affect the performance of data movement (Copy Activity) in Azure Data Factory.</span></span> <span data-ttu-id="6481e-256">이 문서에서는 내부 테스트 중에 관찰되는 성능 관련 정보도 제공하며, 복사 활동의 성능을 최적화하는 여러 가지 방법에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-256">It also lists the observed performance during internal testing and discusses various ways to optimize the performance of Copy Activity.</span></span>

## <a name="fault-tolerance"></a><span data-ttu-id="6481e-257">내결함성</span><span class="sxs-lookup"><span data-stu-id="6481e-257">Fault tolerance</span></span>
<span data-ttu-id="6481e-258">기본적으로 복사 작업은 원본과 싱크 간에 호환되지 않는 데이터가 발견되면 데이터 복사를 중지하고 오류를 반환합니다. 물론 호환되지 않는 행을 건너뛰고 로깅한 후 호환되는 데이터만 복사하여 복사가 성공적으로 수행되도록 명시적으로 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-258">By default, copy activity will stop copying data and return failure when encounter incompatible data between source and sink; while you can explicitly configure to skip and log the incompatible rows and only copy those compatible data to make the copy succeeded.</span></span> <span data-ttu-id="6481e-259">자세한 내용은 [복사 활동 내결함성](data-factory-copy-activity-fault-tolerance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-259">See the [Copy Activity fault tolerance](data-factory-copy-activity-fault-tolerance.md) on more details.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="6481e-260">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6481e-260">Security considerations</span></span>
<span data-ttu-id="6481e-261">Azure Data Factory의 데이터 이동 서비스가 데이터를 보호하는 데 사용하는 기본 보안 인프라에 대해 설명하는 [보안 고려 사항](data-factory-data-movement-security-considerations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-261">See the [Security considerations](data-factory-data-movement-security-considerations.md), which describes security infrastructure that data movement services in Azure Data Factory use to secure your data.</span></span>

## <a name="scheduling-and-sequential-copy"></a><span data-ttu-id="6481e-262">예약 및 순차 복사</span><span class="sxs-lookup"><span data-stu-id="6481e-262">Scheduling and sequential copy</span></span>
<span data-ttu-id="6481e-263">Data Factory에서 예약 및 실행이 작동하는 방식에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-263">See [Scheduling and execution](data-factory-scheduling-and-execution.md) for detailed information about how scheduling and execution works in Data Factory.</span></span> <span data-ttu-id="6481e-264">순차/순서가 지정된 방식으로 하나씩 여러 복사 작업을 실행하는 것이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-264">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="6481e-265">[순차적으로 복사](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-265">See the [Copy sequentially](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) section.</span></span>

## <a name="type-conversions"></a><span data-ttu-id="6481e-266">형식 변환</span><span class="sxs-lookup"><span data-stu-id="6481e-266">Type conversions</span></span>
<span data-ttu-id="6481e-267">다른 데이터 저장소에는 서로 다른 네이티브 형식 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-267">Different data stores have different native type systems.</span></span> <span data-ttu-id="6481e-268">복사 활동에서는 다음과 같은 2단계 방식을 통해 소스 형식에서 싱크 형식으로의 자동 형식 변환을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-268">Copy Activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="6481e-269">네이티브 소스 형식에서 .NET 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="6481e-269">Convert from native source types to a .NET type.</span></span>
2. <span data-ttu-id="6481e-270">.NET 형식에서 네이티브 싱크 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="6481e-270">Convert from a .NET type to a native sink type.</span></span>

<span data-ttu-id="6481e-271">네이티브 형식 시스템에서 데이터 저장소용 .NET 형식으로의 매핑은 각 데이터 저장소 문서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-271">The mapping from a native type system to a .NET type for a data store is in the respective data store article.</span></span> <span data-ttu-id="6481e-272">이러한 매핑을 확인하려면 [지원되는 데이터 저장소](#supported-data-stores) 테이블에서 해당 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-272">(Click the specific link in the [Supported data stores](#supported-data-stores) table).</span></span> <span data-ttu-id="6481e-273">복사 활동에서 적절한 변환을 수행하도록 이러한 매핑을 사용하여 테이블을 만드는 동안 적절한 형식을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6481e-273">You can use these mappings to determine appropriate types while creating your tables, so that Copy Activity performs the right conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6481e-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6481e-274">Next steps</span></span>
* <span data-ttu-id="6481e-275">복사 작업에 대해 자세히 알아보려면 [Azure Blob 저장소에서 Azure SQL Database로 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-275">To learn about the Copy Activity more, see [Copy data from Azure Blob storage to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
* <span data-ttu-id="6481e-276">온-프레미스 데이터 저장소에서 클라우드 데이터 저장소로 데이터를 이동하는 방법에 대해 알아보려면 [온-프레미스에서 클라우드 데이터 저장소로 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6481e-276">To learn about moving data from an on-premises data store to a cloud data store, see [Move data from on-premises to cloud data stores](data-factory-move-data-between-onprem-and-cloud.md).</span></span>
