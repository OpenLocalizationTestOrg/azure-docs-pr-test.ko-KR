---
title: "SSIS 커넥터를 사용 하 여 Azure Blob 저장소에서 데이터 tooor aaaMove | Microsoft Docs"
description: "SSIS 커넥터를 사용 하 여 Azure Blob 저장소에서 데이터 tooor를 이동 합니다."
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
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a><span data-ttu-id="6ac89-103">SSIS 커넥터를 사용 하 여 Azure Blob 저장소에서 데이터 tooor 이동</span><span class="sxs-lookup"><span data-stu-id="6ac89-103">Move data tooor from Azure Blob Storage using SSIS connectors</span></span>
<span data-ttu-id="6ac89-104">hello [Azure에 대 한 SQL Server Integration Services 기능 팩](https://msdn.microsoft.com/library/mt146770.aspx) 제공 구성 요소 tooconnect tooAzure, Azure 및 온-프레미스 데이터 원본 및 Azure에 저장 된 데이터 처리 간에 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-104">hello [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components tooconnect tooAzure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="6ac89-105">고객 hello 클라우드로 온-프레미스 데이터 이동, 모든 Azure 서비스 tooleverage hello 최대한 활용 hello Azure 기술 제품군에서에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-105">Once customers have moved on-premises data into hello cloud, they can access it from any Azure service tooleverage hello full power of hello suite of Azure technologies.</span></span> <span data-ttu-id="6ac89-106">예를 들어 Azure 기계 학습 또는 HDInsight 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span></span>

<span data-ttu-id="6ac89-107">이 일반적으로 hello에 대 한 hello 첫 번째 단계 일 [SQL](machine-learning-data-science-process-sql-walkthrough.md) 및 [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-107">This is typically be hello first step for hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span></span>

<span data-ttu-id="6ac89-108">SSIS tooaccomplish 비즈니스를 사용 하는 정식 시나리오에 대 한 내용은 하이브리드 데이터 통합 시나리오에서 일반적으로 필요한 참조 [이렇게 하면 Azure에 대 한 SQL Server Integration Services 기능 팩으로 더 많은](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) 블로그.</span><span class="sxs-lookup"><span data-stu-id="6ac89-108">For a discussion of canonical scenarios that use SSIS tooaccomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span></span>

> [!NOTE]
> <span data-ttu-id="6ac89-109">전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-109">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6ac89-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ac89-110">Prerequisites</span></span>
<span data-ttu-id="6ac89-111">tooperform hello 작업은이 문서에 설명 있어야 Azure 구독 및 Azure 저장소 계정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-111">tooperform hello tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span></span> <span data-ttu-id="6ac89-112">에 Azure 저장소 계정 이름 및 계정 키 tooupload 알고 있거나 데이터를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-112">You must know your Azure storage account name and account key tooupload or download data.</span></span>

* <span data-ttu-id="6ac89-113">tooset는 **Azure 구독**, 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-113">tooset up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6ac89-114">**저장소 계정** 을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ac89-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="6ac89-115">toouse hello **SSIS 커넥터**를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-115">toouse hello **SSIS connectors**, you must download:</span></span>

* <span data-ttu-id="6ac89-116">**SQL Server 2014 또는 2016 Standard 이상**: 설치 파일에 SQL Server Integration Services가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span></span>
* <span data-ttu-id="6ac89-117">**Microsoft SQL Server 2014 또는 Azure에 대 한 2016 Integration Services 기능 팩**: 여기에서 다운로드할 수 있습니다, 각각 hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) 및 [SQL Server 2016 통합 서비스](https://www.microsoft.com/download/details.aspx?id=49492) 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span></span>

> [!NOTE]
> <span data-ttu-id="6ac89-118">SSIS는 SQL Server, 함께 설치 되지만 hello Express 버전에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-118">SSIS is installed with SQL Server, but is not included in hello Express version.</span></span> <span data-ttu-id="6ac89-119">다양한 버전의 SQL Server에 포함된 응용 프로그램에 대한 자세한 내용은 [SQL Server 버전](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ac89-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span></span>
> 
> 

<span data-ttu-id="6ac89-120">SSIS에 대한 교육 자료는 [SSIS에 대한 실습 교육](http://www.microsoft.com/download/details.aspx?id=20766)</span><span class="sxs-lookup"><span data-stu-id="6ac89-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span></span>

<span data-ttu-id="6ac89-121">방법에 대 한 내용은 tooget 위쪽 실행 SISS toobuild 간단한 추출, 변환 및 로드 하는 ETL 패키지를 사용 하 여 참조 [SSIS 자습서: 간단한 ETL 패키지 만들기](https://msdn.microsoft.com/library/ms169917.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-121">For information on how tooget up-and-running using SISS toobuild simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span></span>

## <a name="download-nyc-taxi-dataset"></a><span data-ttu-id="6ac89-122">NYC Taxi 데이터 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ac89-122">Download NYC Taxi dataset</span></span>
<span data-ttu-id="6ac89-123">hello 설명 된 예제 여기 공개적으로 사용할 수 있는 데이터 집합 사용-hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-123">hello example described here use a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="6ac89-124">hello 2013 년에 약 173 백만 택시 타기 NYC의 hello 데이터 집합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-124">hello dataset consists of about 173 million taxi rides in NYC in hello year 2013.</span></span> <span data-ttu-id="6ac89-125">데이터는 여정 정보 데이터와 요금 데이터의 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-125">There are two types of data: trip details data and fare data.</span></span> <span data-ttu-id="6ac89-126">월별로 하나의 파일씩 총 24개의 파일이 있으며, 각 파일은 압축되지 않은 크기가 약 2GB입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="6ac89-127">데이터 tooAzure blob 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="6ac89-127">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="6ac89-128">hello SSIS를 사용 하 여 toomove 데이터 기능 팩에서 온-프레미스 tooAzure blob 저장소, hello의 인스턴스 사용 [ **Azure Blob 업로드 태스크**](https://msdn.microsoft.com/library/mt146776.aspx), 여기에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-128">toomove data using hello SSIS feature pack from on-premises tooAzure blob storage, we use an instance of hello [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span></span>

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

<span data-ttu-id="6ac89-130">hello 매개 변수를 사용 하 여 작업 hello 여기 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-130">hello parameters that hello task uses are described here:</span></span>

| <span data-ttu-id="6ac89-131">필드</span><span class="sxs-lookup"><span data-stu-id="6ac89-131">Field</span></span> | <span data-ttu-id="6ac89-132">설명</span><span class="sxs-lookup"><span data-stu-id="6ac89-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ac89-133">**AzureStorageConnection**</span><span class="sxs-lookup"><span data-stu-id="6ac89-133">**AzureStorageConnection**</span></span> |<span data-ttu-id="6ac89-134">호스팅되는 toowhere hello blob 파일을 가리키는 tooan Azure 저장소 계정을 참조 하는 하나 새 또는 기존 Azure 저장소 연결 관리자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers tooan Azure storage account that points toowhere hello blob files are hosted.</span></span> |
| <span data-ttu-id="6ac89-135">**BlobContainer**</span><span class="sxs-lookup"><span data-stu-id="6ac89-135">**BlobContainer**</span></span> |<span data-ttu-id="6ac89-136">Blob으로 업로드 하는 hello 파일을 보유 하는 hello blob 컨테이너의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-136">Specifies hello name of hello blob container that hold hello uploaded files as blobs.</span></span> |
| <span data-ttu-id="6ac89-137">**BlobDirectory**</span><span class="sxs-lookup"><span data-stu-id="6ac89-137">**BlobDirectory**</span></span> |<span data-ttu-id="6ac89-138">블록 blob으로 업로드 된 hello 파일이 저장 된 hello blob 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-138">Specifies hello blob directory where hello uploaded file is stored as a block blob.</span></span> <span data-ttu-id="6ac89-139">hello blob 디렉터리는 가상 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-139">hello blob directory is a virtual hierarchical structure.</span></span> <span data-ttu-id="6ac89-140">Hello blob가 이미 있는 경우 ia 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-140">If hello blob already exists, it ia replaced.</span></span> |
| <span data-ttu-id="6ac89-141">**LocalDirectory**</span><span class="sxs-lookup"><span data-stu-id="6ac89-141">**LocalDirectory**</span></span> |<span data-ttu-id="6ac89-142">Hello 파일 toobe 업로드를 포함 하는 hello 로컬 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-142">Specifies hello local directory that contains hello files toobe uploaded.</span></span> |
| <span data-ttu-id="6ac89-143">**FileName**</span><span class="sxs-lookup"><span data-stu-id="6ac89-143">**FileName**</span></span> |<span data-ttu-id="6ac89-144">지정 된 이름 패턴 hello 이름 필터 tooselect 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-144">Specifies a name filter tooselect files with hello specified name pattern.</span></span> <span data-ttu-id="6ac89-145">예를 들어 MySheet\*.xls\*는 MySheet001.xls 및 MySheetABC.xlsx와 같은 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span></span> |
| <span data-ttu-id="6ac89-146">**TimeRangeFrom/TimeRangeTo**</span><span class="sxs-lookup"><span data-stu-id="6ac89-146">**TimeRangeFrom/TimeRangeTo**</span></span> |<span data-ttu-id="6ac89-147">시간 범위 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-147">Specifies a time range filter.</span></span> <span data-ttu-id="6ac89-148">*TimeRangeFrom* 이후부터 *TimeRangeTo* 이전까지 수정된 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span></span> |

> [!NOTE]
> <span data-ttu-id="6ac89-149">hello **AzureStorageConnection** 올바른 toobe 및 hello 자격 증명 필요 **BlobContainer** hello 전송 시도 되기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-149">hello **AzureStorageConnection** credentials need toobe correct and hello **BlobContainer** must exist before hello transfer is attempted.</span></span>
> 
> 

## <a name="download-data-from-azure-blob-storage"></a><span data-ttu-id="6ac89-150">Azure Blob 저장소에서 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ac89-150">Download data from Azure blob storage</span></span>
<span data-ttu-id="6ac89-151">hello 인스턴스를 사용 하는 SSIS와 Azure blob 저장소 tooon 온-프레미스 저장소에서 toodownload 데이터 [Azure Blob 업로드 태스크](https://msdn.microsoft.com/library/mt146779.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-151">toodownload data from Azure blob storage tooon-premises storage with SSIS, use an instance of hello [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span></span>

## <a name="more-advanced-ssis-azure-scenarios"></a><span data-ttu-id="6ac89-152">고급 SSIS-Azure 시나리오</span><span class="sxs-lookup"><span data-stu-id="6ac89-152">More advanced SSIS-Azure scenarios</span></span>
<span data-ttu-id="6ac89-153">hello SSIS 기능 팩 함께 패키징 작업에 의해 처리 되는 더 복잡 한 흐름 toobe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-153">hello SSIS feature pack allows for more complex flows toobe handled by packaging tasks together.</span></span> <span data-ttu-id="6ac89-154">예를 들어 출력을 가진 백 tooa blob 및 tooon 온-프레미스 저장소 다운로드 될 수는 HDInsight 클러스터에 직접 hello blob 데이터 피드 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-154">For example, hello blob data could feed directly into an HDInsight cluster, whose output could be downloaded back tooa blob and then tooon-premises storage.</span></span> <span data-ttu-id="6ac89-155">SSIS는 추가 SSIS 커넥터를 사용하여 HDInsight 클러스터에서 Hive 및 Pig 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span></span>

* <span data-ttu-id="6ac89-156">Azure HDInsight의 Hive 스크립트 SSIS를 사용 하 여 포함 하는 클러스터 toorun [Azure HDInsight 하이브 태스크](https://msdn.microsoft.com/library/mt146771.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-156">toorun a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span></span>
* <span data-ttu-id="6ac89-157">SSIS를 사용 하 여 포함 하는 클러스터에서 Azure HDInsight Pig 스크립트 toorun [Azure HDInsight Pig 태스크](https://msdn.microsoft.com/library/mt146781.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac89-157">toorun a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span></span>

