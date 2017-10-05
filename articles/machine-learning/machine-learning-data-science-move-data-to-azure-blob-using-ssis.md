---
title: "SSIS 커넥터를 사용하여 Azure Blob Storage의 데이터 이동 | Microsoft Docs"
description: "SSIS 커넥터를 사용하여 Azure Blob 저장소의 데이터 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 575beaea5443919bd9728016bf100b43de8e4aab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-or-from-azure-blob-storage-using-ssis-connectors"></a><span data-ttu-id="5806d-103">SSIS 커넥터를 사용하여 Azure Blob Storage의 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="5806d-103">Move data to or from Azure Blob Storage using SSIS connectors</span></span>
<span data-ttu-id="5806d-104">[Azure용 SQL Server Integration Services 기능 팩](https://msdn.microsoft.com/library/mt146770.aspx) 에서는 Azure에 연결하고, Azure와 온-프레미스 데이터 원본 간에 데이터를 전송하며, Azure에 저장된 데이터를 처리하는 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-104">The [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components to connect to Azure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="5806d-105">고객은 온-프레미스 데이터를 클라우드로 이동한 후 Azure 서비스에서 데이터에 액세스하여 Azure 기술의 완전한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-105">Once customers have moved on-premises data into the cloud, they can access it from any Azure service to leverage the full power of the suite of Azure technologies.</span></span> <span data-ttu-id="5806d-106">예를 들어 Azure 기계 학습 또는 HDInsight 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span></span>

<span data-ttu-id="5806d-107">이는 일반적으로 [SQL](machine-learning-data-science-process-sql-walkthrough.md) 및 [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) 연습의 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-107">This is typically be the first step for the [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span></span>

<span data-ttu-id="5806d-108">SSIS를 사용하여 하이브리드 데이터 통합 시나리오에서 일반적인 비즈니스 요구 사항을 충족하는 정식 시나리오에 대한 자세한 내용은 [Azure용 SQL Server Integration Services 통합 팩으로 더 많은 작업 수행](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) 블로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-108">For a discussion of canonical scenarios that use SSIS to accomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span></span>

> [!NOTE]
> <span data-ttu-id="5806d-109">Azure Blob Storage에 대한 전체 소개 내용은 [Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-109">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5806d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5806d-110">Prerequisites</span></span>
<span data-ttu-id="5806d-111">이 문서에 설명된 작업을 수행하려면 Azure 구독이 있어야 하며 Azure 저장소 계정을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-111">To perform the tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span></span> <span data-ttu-id="5806d-112">데이터를 업로드하거나 다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-112">You must know your Azure storage account name and account key to upload or download data.</span></span>

* <span data-ttu-id="5806d-113">**Azure 구독**을 설정하려면 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-113">To set up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5806d-114">**저장소 계정** 을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="5806d-115">**SSIS 커넥터**를 사용하려면 다음을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-115">To use the **SSIS connectors**, you must download:</span></span>

* <span data-ttu-id="5806d-116">**SQL Server 2014 또는 2016 Standard 이상**: 설치 파일에 SQL Server Integration Services가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span></span>
* <span data-ttu-id="5806d-117">**Azure용 Microsoft SQL Server 2014 또는 2016 Integration Services 기능 팩**: [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) 및 [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) 페이지에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from the [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span></span>

> [!NOTE]
> <span data-ttu-id="5806d-118">SSIS는 SQL Server와 함께 설치되지만 Express 버전에는 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-118">SSIS is installed with SQL Server, but is not included in the Express version.</span></span> <span data-ttu-id="5806d-119">다양한 버전의 SQL Server에 포함된 응용 프로그램에 대한 자세한 내용은 [SQL Server 버전](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span></span>
> 
> 

<span data-ttu-id="5806d-120">SSIS에 대한 교육 자료는 [SSIS에 대한 실습 교육](http://www.microsoft.com/download/details.aspx?id=20766)</span><span class="sxs-lookup"><span data-stu-id="5806d-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span></span>

<span data-ttu-id="5806d-121">SISS를 사용하여 간단한 ETL(추출, 변환 및 로드) 패키지를 빌드하는 방법에 대한 자세한 내용은 [SSIS 자습서: 간단한 ETL 패키지 만들기](https://msdn.microsoft.com/library/ms169917.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5806d-121">For information on how to get up-and-running using SISS to build simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span></span>

## <a name="download-nyc-taxi-dataset"></a><span data-ttu-id="5806d-122">NYC Taxi 데이터 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="5806d-122">Download NYC Taxi dataset</span></span>
<span data-ttu-id="5806d-123">여기에 설명된 예제에서는 공개적으로 제공되는 데이터 집합인 [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-123">The example described here use a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="5806d-124">이 데이터 집합은 2013년 뉴욕 시의 1억 7,300만 건에 달하는 택시 승차 기록으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-124">The dataset consists of about 173 million taxi rides in NYC in the year 2013.</span></span> <span data-ttu-id="5806d-125">데이터는 여정 정보 데이터와 요금 데이터의 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-125">There are two types of data: trip details data and fare data.</span></span> <span data-ttu-id="5806d-126">월별로 하나의 파일씩 총 24개의 파일이 있으며, 각 파일은 압축되지 않은 크기가 약 2GB입니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="5806d-127">Azure Blob 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="5806d-127">Upload data to Azure blob storage</span></span>
<span data-ttu-id="5806d-128">SSIS 기능 팩을 사용하여 온-프레미스에서 Azure blob 저장소로 데이터를 이동하려면 여기에 표시된 대로 [**Azure Blob 업로드 작업**](https://msdn.microsoft.com/library/mt146776.aspx)의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-128">To move data using the SSIS feature pack from on-premises to Azure blob storage, we use an instance of the [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span></span>

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

<span data-ttu-id="5806d-130">작업에 사용되는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-130">The parameters that the task uses are described here:</span></span>

| <span data-ttu-id="5806d-131">필드</span><span class="sxs-lookup"><span data-stu-id="5806d-131">Field</span></span> | <span data-ttu-id="5806d-132">설명</span><span class="sxs-lookup"><span data-stu-id="5806d-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5806d-133">**AzureStorageConnection**</span><span class="sxs-lookup"><span data-stu-id="5806d-133">**AzureStorageConnection**</span></span> |<span data-ttu-id="5806d-134">기존 Azure 저장소 연결 관리자를 지정하거나, blob 파일이 호스트되는 위치를 가리키는 Azure 저장소 계정을 참조하는 새 Azure 저장소 연결 관리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers to an Azure storage account that points to where the blob files are hosted.</span></span> |
| <span data-ttu-id="5806d-135">**BlobContainer**</span><span class="sxs-lookup"><span data-stu-id="5806d-135">**BlobContainer**</span></span> |<span data-ttu-id="5806d-136">업로드된 파일을 blob로 유지할 blob 컨테이너의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-136">Specifies the name of the blob container that hold the uploaded files as blobs.</span></span> |
| <span data-ttu-id="5806d-137">**BlobDirectory**</span><span class="sxs-lookup"><span data-stu-id="5806d-137">**BlobDirectory**</span></span> |<span data-ttu-id="5806d-138">업로드된 파일을 블록 blob로 저장할 blob 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-138">Specifies the blob directory where the uploaded file is stored as a block blob.</span></span> <span data-ttu-id="5806d-139">blob 디렉터리는 가상 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-139">The blob directory is a virtual hierarchical structure.</span></span> <span data-ttu-id="5806d-140">blob가 이미 있는 경우 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-140">If the blob already exists, it ia replaced.</span></span> |
| <span data-ttu-id="5806d-141">**LocalDirectory**</span><span class="sxs-lookup"><span data-stu-id="5806d-141">**LocalDirectory**</span></span> |<span data-ttu-id="5806d-142">업로드할 파일이 포함된 로컬 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-142">Specifies the local directory that contains the files to be uploaded.</span></span> |
| <span data-ttu-id="5806d-143">**FileName**</span><span class="sxs-lookup"><span data-stu-id="5806d-143">**FileName**</span></span> |<span data-ttu-id="5806d-144">지정된 이름 패턴의 파일을 선택할 이름 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-144">Specifies a name filter to select files with the specified name pattern.</span></span> <span data-ttu-id="5806d-145">예를 들어 MySheet\*.xls\*는 MySheet001.xls 및 MySheetABC.xlsx와 같은 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span></span> |
| <span data-ttu-id="5806d-146">**TimeRangeFrom/TimeRangeTo**</span><span class="sxs-lookup"><span data-stu-id="5806d-146">**TimeRangeFrom/TimeRangeTo**</span></span> |<span data-ttu-id="5806d-147">시간 범위 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-147">Specifies a time range filter.</span></span> <span data-ttu-id="5806d-148">*TimeRangeFrom* 이후부터 *TimeRangeTo* 이전까지 수정된 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span></span> |

> [!NOTE]
> <span data-ttu-id="5806d-149">전송을 시도하기 전에 **AzureStorageConnection** 자격 증명이 올바르고 **BlobContainer**가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-149">The **AzureStorageConnection** credentials need to be correct and the **BlobContainer** must exist before the transfer is attempted.</span></span>
> 
> 

## <a name="download-data-from-azure-blob-storage"></a><span data-ttu-id="5806d-150">Azure Blob 저장소에서 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="5806d-150">Download data from Azure blob storage</span></span>
<span data-ttu-id="5806d-151">SSIS를 사용하여 Azure Blob 저장소에서 온-프레미스 저장소로 데이터를 다운로드하려면 [Azure Blob 업로드 작업](https://msdn.microsoft.com/library/mt146779.aspx)의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-151">To download data from Azure blob storage to on-premises storage with SSIS, use an instance of the [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span></span>

## <a name="more-advanced-ssis-azure-scenarios"></a><span data-ttu-id="5806d-152">고급 SSIS-Azure 시나리오</span><span class="sxs-lookup"><span data-stu-id="5806d-152">More advanced SSIS-Azure scenarios</span></span>
<span data-ttu-id="5806d-153">SSIS 기능 팩을 사용하면 패키징 작업을 통해 보다 복잡한 흐름을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-153">The SSIS feature pack allows for more complex flows to be handled by packaging tasks together.</span></span> <span data-ttu-id="5806d-154">예를 들어 blob 데이터를 HDInsight 클러스터에 직접 공급하여 해당 출력을 blob로 다시 다운로드한 다음 온-프레미스 저장소에 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-154">For example, the blob data could feed directly into an HDInsight cluster, whose output could be downloaded back to a blob and then to on-premises storage.</span></span> <span data-ttu-id="5806d-155">SSIS는 추가 SSIS 커넥터를 사용하여 HDInsight 클러스터에서 Hive 및 Pig 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span></span>

* <span data-ttu-id="5806d-156">SSIS를 사용하여 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하려면 [Azure HDInsight Hive 작업](https://msdn.microsoft.com/library/mt146771.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-156">To run a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span></span>
* <span data-ttu-id="5806d-157">SSIS를 사용하여 Azure HDInsight 클러스터에서 Pig 스크립트를 실행하려면 [Azure HDInsight Pig 작업](https://msdn.microsoft.com/library/mt146781.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5806d-157">To run a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span></span>

