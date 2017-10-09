---
title: "Data Factory와 일괄 처리를 사용 하 여 aaaProcess 대규모 데이터 집합 | Microsoft Docs"
description: "Azure 일괄 처리의 병렬 처리 기능을 사용 하 여 tooprocess 많은 양의 데이터를 Azure 데이터 팩터리 파이프라인 하는 방법을 설명 합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="bf022-103">데이터 팩터리 및 배치를 사용하여 대규모 데이터 집합 처리</span><span class="sxs-lookup"><span data-stu-id="bf022-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="bf022-104">이 문서에서는 예약된 자동 방식으로 대규모 데이터 집합을 이동 및 처리하는 샘플 솔루션의 아키텍처에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="bf022-105">또한 Azure 데이터 팩터리 및 Azure 일괄 처리를 사용 하는 종단 간 연습 tooimplement hello 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="bf022-106">이 문서는 전체 샘플 솔루션의 연습을 포함하기 때문에 일반적인 문서보다 깁니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="bf022-107">새 tooBatch 이며 경우 Data Factory 이러한 서비스에 알아볼 수 있습니다 및 함께 작동 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="bf022-108">Hello에만 집중할 수 hello 서비스에 대 한 정보를 알고 있으며는 디자인/아키텍처를 구성 하는 솔루션을 [아키텍처 섹션](#architecture-of-sample-solution) hello 문서 및 개발 하는 경우는 프로토타입 또는 솔루션의 수도 tootry hello에 대 한 단계별 지침 [연습](#implementation-of-sample-solution)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="bf022-109">이 콘텐츠 및 사용 방법에 대한 사용자의 의견을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="bf022-110">첫째, Data Factory와 일괄 처리 서비스 hello 클라우드에서 큰 데이터 집합 처리 및 도울 수 있는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="bf022-111">Azure 배치를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="bf022-111">Why Azure Batch?</span></span>
<span data-ttu-id="bf022-112">Azure 일괄 처리 사용 하면 효율적으로 hello 클라우드에서 대규모 병렬 및 고성능 HPC (컴퓨팅) 응용 toorun 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="bf022-113">가상 컴퓨터의 관리 되는 컬렉션에 toorun 계산 집약적인 작업을 예약 하는 플랫폼 서비스 이며 계산할 수 있습니다 자동으로 크기 조정 작업의 리소스 toomeet hello 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="bf022-114">일괄 처리 서비스 hello로 Azure 계산 리소스 tooexecute 응용 프로그램에서 병렬로 및 정의 규모에.</span><span class="sxs-lookup"><span data-stu-id="bf022-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="bf022-115">요청 시 또는 예약 된 실행 수 작업, toomanually 필요 하지 않은 생성, 구성 및 관리는 HPC 클러스터, 개별 가상 컴퓨터, 가상 네트워크 또는 복잡 한 작업 및 예약 인프라 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="bf022-116">Hello 문서 모르는 Azure 일괄 처리를 hello 아키텍처/이 문서에서 설명 하는 hello 솔루션의 구현으로 사용 하는 경우 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bf022-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="bf022-117">Azure 배치의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="bf022-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="bf022-118">배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="bf022-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="bf022-119">Azure 일괄 처리에 대해 자세히 (선택 사항) toolearn 참조 hello [Azure 일괄 처리에 대 한 학습 경로](https://azure.microsoft.com/documentation/learning-paths/batch/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="bf022-120">Azure Data Factory를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="bf022-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="bf022-121">데이터 팩터리는 오케스트레이션 하 고 데이터의 hello 이동 및 변환을 자동화 하는 클라우드 기반 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="bf022-122">Hello 데이터 팩터리 서비스를 사용 하 여 데이터 저장소 tooa 중앙 집중식된 데이터 저장소를 클라우드 및 온-프레미스에서 데이터를 이동 하는 관리 되는 데이터 파이프라인 만들 수 있습니다 (예: Azure Blob 저장소), 및 프로세스/Azure HDInsight 및 Azure와 같은 서비스를 사용 하 여 데이터 변환 기계 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="bf022-123">예약 된 방식으로 (매시간, 매일, 매주 등) 및 모니터에서 데이터 파이프라인 toorun 예약 및 눈 tooidentify 문제에서 관리할 하 고 수도 있습니다 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="bf022-124">Hello 문서 모르는 Azure 데이터 팩터리를 hello 아키텍처/이 문서에서 설명 하는 hello 솔루션의 구현으로 사용 하는 경우 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bf022-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="bf022-125">Azure Data Factory 소개</span><span class="sxs-lookup"><span data-stu-id="bf022-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="bf022-126">첫 번째 데이터 파이프라인 작성</span><span class="sxs-lookup"><span data-stu-id="bf022-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="bf022-127">(선택 사항) toolearn Azure Data Factory에 대 한 자세한 참조 hello [Azure Data Factory에 대 한 학습 경로](https://azure.microsoft.com/documentation/learning-paths/data-factory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="bf022-128">Data Factory 및 배치</span><span class="sxs-lookup"><span data-stu-id="bf022-128">Data Factory and Batch together</span></span>
<span data-ttu-id="bf022-129">데이터 팩터리 tooa 대상 데이터 저장소 및 Azure에서 Hadoop 클러스터 (HDInsight)를 사용 하 여 Hive 활동 tooprocess 데이터 원본 데이터에서 복사 작업 toocopy/이동 데이터 저장소와 같은 기본 제공 활동을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="bf022-130">지원되는 변환 활동 목록에 대해서는 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="bf022-131">또한 toomove 또는 프로세스 데이터를 사용자 논리로 있습니다 toocreate 사용자 지정.NET 작업을 허용 하 고 Vm의 Azure 배치 풀 또는 Azure HDInsight 클러스터에서 이러한 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="bf022-132">Azure 일괄 처리를 사용 하면 hello 풀 tooauto 단위를 구성할 수 있습니다 (추가 또는 Vm hello 작업에 따라 제거) 수식을 기반으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="bf022-133">샘플 솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="bf022-133">Architecture of sample solution</span></span>
<span data-ttu-id="bf022-134">간단한 솔루션에 대 한이 문서에서 설명 하는 hello 아키텍처는으로 없지만 위험 금융 서비스, 이미지 처리 및 렌더링 및 genomic 분석 하 여 모델링 하는 등의 관련 toocomplex 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="bf022-135">처리 및 Azure 일괄 처리 하는 2) 방법을 병렬 방식으로 데이터를 hello 및 hello 다이어그램 Data Factory에서 데이터 이동을 조정 하는 1) 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="bf022-136">다운로드 및 인쇄 hello 다이어그램 쉽게 참조할 (11 x 17 인치입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="bf022-137">또는 A3 크기). [Azure 배치 및 Data Factory를 사용하여 HPC 및 데이터 오케스트레이션](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="bf022-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="bf022-138">[![대규모 데이터 처리 다이어그램](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="bf022-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="bf022-139">hello 다음 목록에서는 hello hello 프로세스의 기본 단계.</span><span class="sxs-lookup"><span data-stu-id="bf022-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="bf022-140">hello 솔루션 코드와 설명이 toobuild hello 종단 간 솔루션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="bf022-141">**계산 노드(VM)의 풀과 함께 Azure 배치를 구성합니다**.</span><span class="sxs-lookup"><span data-stu-id="bf022-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="bf022-142">Hello 노드 수 및 각 노드의의 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="bf022-143">**Azure Data Factory 인스턴스를 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="bf022-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="bf022-144">**Hello 데이터 팩터리 파이프라인에서 사용자 지정.NET 작업을 만들려면**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="bf022-145">hello 작업은 hello Azure 배치 풀에서 실행 되는 사용자 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="bf022-146">**Azure storage에 Blob으로 대량의 입력 데이터를 저장합니다**.</span><span class="sxs-lookup"><span data-stu-id="bf022-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="bf022-147">데이터는 논리 조각(일반적으로 시간으로)으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="bf022-148">**동시에 처리 되는 데이터를 복사 하는 데이터 팩터리** toohello 보조 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="bf022-149">**일괄 처리에 의해 할당 된 hello 풀을 사용 하 여 hello 사용자 지정 활동을 실행 하는 데이터 팩터리**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="bf022-150">데이터 팩터리는 작업을 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="bf022-151">각 작업은 데이터 조각을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="bf022-152">hello 결과 Azure 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="bf022-153">**Hello 최종 결과 tooa 세 번째 위치를 이동 하는 데이터 팩터리**, 응용 프로그램을 통해 배포에 대 한 또는 다른 도구에서 처리 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="bf022-154">샘플 솔루션의 구현</span><span class="sxs-lookup"><span data-stu-id="bf022-154">Implementation of sample solution</span></span>
<span data-ttu-id="bf022-155">hello 샘플 솔루션에는 의도적으로 간단 하 tooshow 있습니다 어떻게 toouse Data Factory와 일괄 처리 함께 tooprocess 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="bf022-156">hello 솔루션은 단순히 시계열에 구성 하는 입력된 파일에서 일치 하는 검색 단어 ("Microsoft")의 hello 수를 셉니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="bf022-157">Hello count toooutput 파일을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="bf022-158">**시간**:이 솔루션은 1 ~ 2 시간 toocomplete Azure, Data Factory 및 일괄 처리의 기본 사항을 잘 알고 있다면가 아래 나열 된 완료 된 hello 필수 구성 요소를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bf022-159">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bf022-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="bf022-160">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="bf022-160">Azure subscription</span></span>
<span data-ttu-id="bf022-161">Azure 구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bf022-162">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="bf022-163">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="bf022-163">Azure storage account</span></span>
<span data-ttu-id="bf022-164">Azure 저장소 계정 '를 사용 하 여이 자습서에서 hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="bf022-165">Azure 저장소 계정이 없는 경우 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="bf022-166">blob 저장소를 사용 하는 hello 샘플 솔루션.</span><span class="sxs-lookup"><span data-stu-id="bf022-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="bf022-167">Azure 배치 계정</span><span class="sxs-lookup"><span data-stu-id="bf022-167">Azure Batch account</span></span>
<span data-ttu-id="bf022-168">Hello를 사용 하 여 Azure 배치 계정 만들기 [Azure 포털](http://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="bf022-169">[Azure 배치 계정 만들기 및 관리](../batch/batch-account-create-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="bf022-170">Note hello Azure 배치 계정 이름 및 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="bf022-171">사용할 수도 있습니다 [새로 AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate Azure 배치 계정 만들려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="bf022-172">이 cmdlet 사용에 대한 자세한 지침은 [Azure 배치 PowerShell cmdlet 시작](../batch/batch-powershell-cmdlets-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="bf022-173">hello 샘플 솔루션에 계산 노드 (가상 컴퓨터의 관리 되는 컬렉션)의 풀 병렬 방식에서 간접적으로 (Azure 데이터 팩터리 파이프라인)를 통해 Azure 배치 tooprocess 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="bf022-174">VM(가상 컴퓨터)의 Azure 배치 풀</span><span class="sxs-lookup"><span data-stu-id="bf022-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="bf022-175">적어도 2개의 계산 노드로 **Azure 배치 풀**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="bf022-176">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **찾아보기** 에서 왼쪽된 메뉴 hello 하 고 클릭 **일괄 처리 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="bf022-177">선택 하면 Azure 배치 계정 tooopen hello **일괄 처리 계정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="bf022-178">**풀** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="bf022-179">Hello에 **풀** 블레이드에서 hello 도구 모음 tooadd 풀에 추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="bf022-180">Hello 풀에 대 한 ID를 입력 (**풀 ID**).</span><span class="sxs-lookup"><span data-stu-id="bf022-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="bf022-181">참고 hello **hello 풀의 ID**; hello Data Factory 솔루션을 만들 때 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="bf022-182">지정 **Windows Server 2012 R2** hello 운영 체제 제품군 설정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="bf022-183">**노드 가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="bf022-184">입력 **2** hello에 대 한 값으로 **대상 전용** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="bf022-185">입력 **2** hello에 대 한 값으로 **노드당 최대 작업** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="bf022-186">클릭 **확인** toocreate hello 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="bf022-187">Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="bf022-187">Azure Storage Explorer</span></span>
<span data-ttu-id="bf022-188">[Azure Storage 탐색기 6(도구)](https://azurestorageexplorer.codeplex.com/) 또는 [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer)(ClumsyLeaf 소프트웨어에서).</span><span class="sxs-lookup"><span data-stu-id="bf022-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="bf022-189">이러한 도구를 사용 하 여 검사 하 고 클라우드에서 호스트 응용 프로그램의 hello 로그를 포함 하 여 Azure 저장소 프로젝트의 hello 데이터를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="bf022-190">개인 액세스로 **mycontainer**라는 컨테이너 만들기(익명 액세스 없음)</span><span class="sxs-lookup"><span data-stu-id="bf022-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="bf022-191">사용 중인 경우 **CloudXplorer**된 하위 폴더가 hello 다음 구조를 만들고 폴더:</span><span class="sxs-lookup"><span data-stu-id="bf022-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="bf022-192">`Inputfolder` 및 `outputfolder`는 `mycontainer`에서 최상위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="bf022-193">hello `inputfolder` 날짜 타임 스탬프 (YYYY-m M-DD-HH)와 함께 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="bf022-194">사용 중인 경우 **Azure 저장소 탐색기**, tooupload 파일 이름의 hello 다음 단계에서 필요: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` 등입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="bf022-195">이 단계는 자동으로 hello 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="bf022-196">텍스트 파일을 만들어 **file.txt** hello 키워드 있는 콘텐츠를 사용 하 여 컴퓨터에서 **Microsoft**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="bf022-197">예: "테스트 사용자 지정 작업 Microsoft 테스트 사용자 지정 작업 Microsoft”</span><span class="sxs-lookup"><span data-stu-id="bf022-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="bf022-198">Hello 파일 toohello 다음 입력된 폴더 Azure blob 저장소에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="bf022-199">사용 중인 경우 **Azure 저장소 탐색기**, hello 파일 업로드 **file.txt** 너무**mycontainer**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="bf022-200">클릭 **복사** hello 도구 모음 toocreate hello blob의 복사본에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="bf022-201">Hello에 **Blob 복사** 대화 상자에서 변경 hello **대상 blob 이름** 너무`inputfolder/2015-11-16-00/file.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="bf022-202">이 단계 toocreate 반복 `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` 등입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="bf022-203">이 작업은 자동으로 hello 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="bf022-204">`customactivitycontainer`라는 다른 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="bf022-205">Hello 사용자 지정 활동 zip 파일 toothis 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="bf022-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bf022-206">Visual Studio</span></span>
<span data-ttu-id="bf022-207">Microsoft Visual Studio 2012 또는 이후 toocreate hello 사용자 정의 일괄 처리 활동 toobe hello Data Factory 솔루션에서에서 사용 되는 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="bf022-208">상위 수준 단계 toocreate hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="bf022-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="bf022-209">Hello 데이터 처리 논리를 포함 하는 사용자 지정 활동을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="bf022-210">Hello 사용자 지정 활동을 사용 하는 Azure 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="bf022-211">Hello 사용자 지정 활동 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-211">Create hello custom activity</span></span>
<span data-ttu-id="bf022-212">hello Data Factory 사용자 지정 활동은이 샘플 솔루션의 hello 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="bf022-213">hello 샘플 솔루션 Azure 배치 toorun hello에 대 한 사용자 지정 활동을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="bf022-214">참조 [Azure 데이터 팩터리 파이프라인에서 사용자 지정 활동을 사용 하 여](data-factory-use-custom-activities.md) hello 기본 정보 toodevelop 사용자 지정 활동 및 사용에 대 한 Azure Data Factory에서 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="bf022-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="bf022-215">Azure 데이터 팩터리 파이프라인에서 사용할 수 있는.NET 사용자 지정 활동 toocreate 해야 toocreate는 **.NET 클래스 라이브러리** 를 구현 하는 클래스를 사용 하 여 프로젝트 **IDotNetActivity** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="bf022-216">이 인터페이스는 **Execute**라는 하나의 메서드만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="bf022-217">다음은 hello 메서드의 hello 서명이입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="bf022-218">hello 메서드에 toounderstand 해야 하는 몇 가지 주요 구성 요소는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="bf022-219">hello 메서드 4 개의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="bf022-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="bf022-220">**linkedServices**.</span></span> <span data-ttu-id="bf022-221">입/출력 데이터 원본을 연결 하는 연결 된 서비스의 열거형 목록 (예: Azure Blob 저장소) toohello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="bf022-222">이 샘플에서는 입력 및 출력 모두에 사용되는 Azure 저장소 형식의 연결된 서비스가 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="bf022-223">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="bf022-223">**datasets**.</span></span> <span data-ttu-id="bf022-224">데이터 집합의 열거형 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="bf022-225">이 매개 변수 tooget hello 위치 및 입력 및 출력 데이터 집합에 정의 된 스키마를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="bf022-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="bf022-226">**activity**.</span></span> <span data-ttu-id="bf022-227">이 매개 변수는 hello 현재 계산 엔터티를-이 경우 Azure 배치 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="bf022-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="bf022-228">**logger**.</span></span> <span data-ttu-id="bf022-229">hello로 거 작성할 수 있습니다 디버그 주석을 해당 화면에 대 한 로그 "User" hello로 hello 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="bf022-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="bf022-230">hello 메서드 hello 미래에 함께 사용 되는 toochain 사용자 지정 활동을 저장할 수 있는 사전을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="bf022-231">이 기능은 아직 구현 되지 않았습니다, 그리고 따라서 hello 메서드에서 빈 사전이 반환을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="bf022-232">프로시저: hello 사용자 지정 활동 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="bf022-233">Visual Studio에서 .NET 클래스 라이브러리 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="bf022-234">**Visual Studio 2012**/**2013/2015**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="bf022-235">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="bf022-236">**템플릿**을 확장하고 **Visual C\#**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="bf022-237">이 연습을 사용 하 여 C\#, 하지만 모든.NET 언어 toodevelop hello 사용자 지정 활동을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="bf022-238">선택 **클래스 라이브러리** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="bf022-239">입력 **MyDotNetActivity** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="bf022-240">선택 **c:\\ADF** hello에 대 한 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="bf022-241">Hello 폴더를 만들고 **ADF** 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="bf022-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="bf022-242">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="bf022-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="bf022-243">클릭 **도구**, 너무 가리킨**NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="bf022-244">Hello에 **패키지 관리자 콘솔**, 다음 명령 tooimport hello 실행 **Microsoft.Azure.Management.DataFactories**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="bf022-245">가져오기 hello **Azure 저장소** toohello 프로젝트에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="bf022-246">이 샘플의 hello Blob 저장소 API를 사용 하기 때문에이 패키지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="bf022-247">Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 지시문 toohello 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="bf022-248">Hello의 hello 이름 변경 **네임 스페이스** 너무**MyDotNetActivityNS**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="bf022-249">Hello 클래스의 hello 이름도 변경**MyDotNetActivity** hello에서 파생 되 고 **IDotNetActivity** 아래와 같이 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="bf022-250">구현 (추가) hello **Execute** hello 방식의 **IDotNetActivity** toohello 인터페이스 **MyDotNetActivity** 다음 샘플 코드 toohello 메서드에 클래스와 복사 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="bf022-251">Hello 참조 [메서드 실행](#execute-method) 섹션에 대 한 설명은이 메서드에 사용 되는 hello 논리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="bf022-252">Hello 다음 도우미 메서드 toohello 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="bf022-253">두이 메서드는 호출 하 여 hello **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf022-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="bf022-254">가장 중요 한 점은 hello **Calculate** 메서드 각 blob을 반복 하는 hello 코드를 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="bf022-255">hello **GetFolderPath** 메서드 반환 hello 경로 toohello 폴더 해당 hello dataset 포인트 tooand hello **GetFileName** 메서드 hello blob/파일을 가리키는 데이터 집합을 hello의 hello 이름을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="bf022-256">hello **Calculate** 메서드 hello 키워드의 인스턴스 수를 계산 **Microsoft** hello 입력 파일 (blob의 hello 폴더에 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="bf022-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="bf022-257">hello 검색 단어 ("Microsoft") hello 코드에 하드 코딩 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="bf022-258">Hello 프로젝트를 컴파일하십시오.</span><span class="sxs-lookup"><span data-stu-id="bf022-258">Compile hello project.</span></span> <span data-ttu-id="bf022-259">클릭 **빌드** hello 메뉴에서 **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="bf022-260">시작 **Windows 탐색기**, 너무 이동**bin\\디버그** 또는 **bin\\릴리스** 빌드의 hello 종류에 따라 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="bf022-261">Zip 파일을 만들 **MyDotNetActivity.zip** hello에서 모든 hello 이진 파일을 포함 하는  **\\bin\\디버그** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="bf022-262">Tooinclude hello MyDotNetActivity 할 수 있습니다. **pdb** 파일 오류 발생 시 hello 문제를 발생 시킨 hello 소스 코드의 줄 번호 등의 추가 정보를 받을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="bf022-263">업로드 **MyDotNetActivity.zip** blob toohello blob 컨테이너로: `customactivitycontainer` hello Azure에서에서 blob 저장소는 hello **StorageLinkedService** 연결 된 서비스 hello에  **ADFTutorialDataFactory** 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="bf022-264">Hello blob 컨테이너 만들기 `customactivitycontainer` 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="bf022-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="bf022-265">메서드 실행</span><span class="sxs-lookup"><span data-stu-id="bf022-265">Execute method</span></span>
<span data-ttu-id="bf022-266">이 섹션에서는 자세한 내용 및 Execute 메서드에서 hello에 hello 코드에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="bf022-267">hello 입력된 컬렉션을 반복 하는 것에 대 한 hello 멤버 hello에 부여 [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="bf022-268">Hello blob 컬렉션을 반복 하려면 hello를 사용 해야 **BlobContinuationToken** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="bf022-269">do를 사용 해야 하는 기본적으로-while 루프 hello 루프를 종료 하는 데 hello 메커니즘으로 hello 토큰으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="bf022-270">자세한 내용은 참조 [어떻게 toouse.NET에서 Blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bf022-271">기본 루프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="bf022-272">Hello에 대 한 hello 설명서를 참조 하십시오. [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) 메서드에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="bf022-273">hello 코드 hello 내에서 이동 논리적으로 hello blob 집합을 통해 작업에 대 한 수행-while 루프.</span><span class="sxs-lookup"><span data-stu-id="bf022-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="bf022-274">Hello에 **Execute** 메서드를 hello 수행-루프 blob 목록을 hello 라는 tooa 메서드를 전달 하는 동안 **Calculate**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="bf022-275">라는 문자열 변수를 반환 하는 hello 메서드 **출력** hello 결과 즉 hello 세그먼트의 모든 hello blob를 반복할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="bf022-276">Hello hello 검색 단어의 발생 수를 반환 (**Microsoft**) hello blob 전달 toohello **Calculate** 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf022-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="bf022-277">한 번 hello **Calculate** 메서드 hello 작업을 했기 것 써야 tooa 새 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="bf022-278">따라서 처리 하는 blob의 모든 집합에 대 한 hello 결과 함께 새 blob은 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="bf022-279">toowrite tooa 새 blob, 첫 번째 찾기 hello 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="bf022-280">hello 코드 도우미 메서드를 호출 또한: **GetFolderPath** tooretrieve hello 폴더 경로 (hello 저장소 컨테이너 이름).</span><span class="sxs-lookup"><span data-stu-id="bf022-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="bf022-281">hello **GetFolderPath** 캐스트 hello DataSet 개체 tooan AzureBlobDataSet FolderPath 라는 속성이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="bf022-282">hello 코드 호출 hello **GetFileName** 메서드 tooretrieve hello 파일 이름 (blob 이름).</span><span class="sxs-lookup"><span data-stu-id="bf022-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="bf022-283">hello 코드는 위의 코드 tooget hello 폴더 경로 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="bf022-284">hello 파일의 hello 이름 URI 개체를 만들어 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="bf022-285">hello URI 생성자 hello를 사용 하 여 **BlobEndpoint** 속성 tooreturn hello 컨테이너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="bf022-286">hello 폴더 경로 파일 이름은 tooconstruct hello 출력 blob URI에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="bf022-287">hello 파일의 이름을 hello를 기록 하 고 이제 hello에서 hello 출력 문자열을 작성할 수 **Calculate** 메서드 tooa 새 blob:</span><span class="sxs-lookup"><span data-stu-id="bf022-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="bf022-288">Hello 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-288">Create hello data factory</span></span>
<span data-ttu-id="bf022-289">Hello에 [hello 사용자 지정 활동을 만드는](#create-the-custom-activity) 사용자 지정 활동을 만든 섹션 및 이진 및 PDB hello zip 파일 업로드 된 hello 파일 tooan Azure blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="bf022-290">이 섹션에서는 Azure 만들게 **데이터 팩터리의** 와 **파이프라인** hello를 사용 하 여 **사용자 지정 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="bf022-291">hello 입력된 폴더에 hello blob (파일)를 나타내는 hello 사용자 지정 활동에 대 한 입력된 데이터 집합을 hello (`mycontainer\\inputfolder`) blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="bf022-292">hello hello 활동 나타냅니다 hello 출력 폴더에 출력 blob hello에 대 한 출력 데이터 집합 (`mycontainer\\outputfolder`) blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="bf022-293">Hello 입력된 폴더에 하나 이상의 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="bf022-294">예를 들어 각 hello 폴더에 콘텐츠를 다음 hello로 하나의 파일 (file.txt)를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="bf022-295">각 입력된 폴더 hello 폴더에 파일이 두 개 이상의 경우에 Azure 데이터 팩터리에서 조각 tooa 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="bf022-296">각 조각은 hello 파이프라인에서 처리 될 때 hello 사용자 지정 활동에 대 한 해당 조각의 hello 입력된 폴더의 모든 hello blob을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="bf022-297">5 개의 출력 파일의 hello로 동일한 콘텐츠는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-297">You see five output files with hello same content.</span></span> <span data-ttu-id="bf022-298">예를 들어 hello 2015-11-16-00 폴더에 hello 파일 처리에서 hello 출력 파일에 다음 콘텐츠는 hello 포함:</span><span class="sxs-lookup"><span data-stu-id="bf022-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="bf022-299">여러 파일 (file.txt, file2.txt, file3.txt)를 삭제할 경우 같은 콘텐츠에 toohello 입력된 폴더 hello로 hello hello 출력 파일의 내용을 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bf022-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="bf022-300">각 폴더 (2015-11-16-00, 등) hello 폴더에 여러 개의 입력된 파일 경우에 tooa 조각이이 샘플에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="bf022-301">hello 출력 파일에 3 개의 줄이 이제 hello 조각 (2015-11-16-00)와 연결 된 hello 폴더에서 각 입력된 파일 (blob)에 대해 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="bf022-302">각 작업 실행에 대한 작업(task)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-302">A task is created for each activity run.</span></span> <span data-ttu-id="bf022-303">이 샘플에 없는 경우 활동이 하나만 hello 파이프라인</span><span class="sxs-lookup"><span data-stu-id="bf022-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="bf022-304">분할 영역 hello 파이프라인에서 처리 될 때 Azure 배치 tooprocess hello 조각에서 hello 사용자 지정 활동 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="bf022-305">5개 조각(각 조각은 여러 Blob 또는 파일을 가질 수 있음)이 있으므로 Azure 배치에서 생성된 5개의 작업이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="bf022-306">일괄 처리에는 작업이 실행 되 면 때 실제로 hello 사용자 지정 활동을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="bf022-307">연습을 수행 하는 hello 추가 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="bf022-308">1 단계: hello 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="bf022-309">Toohello 로그인 한 후 [Azure 포털](https://portal.azure.com/), 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="bf022-310">클릭 **새로** hello 왼쪽된 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="bf022-311">클릭 **데이터 + 분석** hello에 **새로** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="bf022-312">클릭 **Data Factory** hello에 **데이터 분석** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="bf022-313">Hello에 **새 데이터 팩터리** 블레이드에서 입력 **CustomActivityFactory** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="bf022-314">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="bf022-315">Hello 오류가 나타나면: **"CustomActivityFactory" 데이터 팩터리 이름을 사용할 수 없으면**, hello 데이터 팩터리의 hello 이름 변경 (예를 들어 **yournameCustomActivityFactory**) 만들기를 시도 하십시오. 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="bf022-316">**리소스 그룹 이름**을 클릭하여 기존 리소스 그룹을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="bf022-317">Hello 올바른 구독 및 만든 hello 데이터 팩터리 toobe 영역을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="bf022-318">클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="bf022-319">Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="bf022-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="bf022-320">보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="bf022-321">2단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-321">Step 2: Create linked services</span></span>
<span data-ttu-id="bf022-322">연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="bf022-323">이 단계에서 연결할 프로그램 **Azure 저장소** 계정 및 **Azure 배치** 계정 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="bf022-324">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="bf022-325">Hello 클릭 **작성자 및 배포** hello 타일 **DATA FACTORY** 블레이드 **CustomActivityFactory**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="bf022-326">데이터 팩터리 편집기 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="bf022-327">클릭 **새 데이터 저장소** 명령 모음 hello 되 고 선택 **메트릭을 제공 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bf022-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="bf022-328">표시 되어야 hello Azure 저장소를 만들기 위한 JSON 스크립트 hello 편집기에서 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="bf022-329">대체 **계정 이름** hello Azure 저장소 계정 이름으로 및 **계정 키** hello Azure 저장소 계정 액세스 키가 hello 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="bf022-330">toolearn 어떻게 tooget 저장소 액세스 키가 참조 [보기, 복사 및 다시 생성 저장소 액세스 키](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="bf022-331">클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="bf022-332">Azure 배치 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="bf022-333">이 단계에 대 한 연결 된 서비스를 만들 사용자 **Azure 배치** 계정으로 사용 되는 toorun hello Data Factory에 대 한 사용자 지정 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="bf022-334">클릭 **새 계산** 명령 모음 hello 되 고 선택 **Azure 배치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bf022-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="bf022-335">표시 되어야 hello Azure 배치를 만들기 위한 JSON 스크립트 hello 편집기에서 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="bf022-336">JSON 스크립트 hello:</span><span class="sxs-lookup"><span data-stu-id="bf022-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="bf022-337">대체 **계정 이름** hello Azure 배치 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="bf022-338">대체 **선택 키** hello Azure 일괄 처리 계정 액세스 키가 hello 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="bf022-339">Hello에 대 한 hello 풀의 hello ID를 입력 **poolName** 속성**합니다.**</span><span class="sxs-lookup"><span data-stu-id="bf022-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="bf022-340">이 속성의 경우 풀 이름 또는 풀 ID 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="bf022-341">Hello 일괄 처리 hello에 대 한 URI를 입력 **batchUri** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="bf022-342">hello **URL** hello에서 **Azure 배치 계정 블레이드** 형식에 따라 hello에: \<accountname\>.\< 지역\>. batch.azure.com 합니다. Hello에 대 한 **batchUri** hello JSON에에서 속성을 필요한 너무**"accountname"를 제거 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bf022-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="bf022-343">hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-343">from hello URL.</span></span> <span data-ttu-id="bf022-344">예: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="bf022-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="bf022-345">Hello에 대 한 **poolName** 속성을 hello 풀의 hello 이름 대신 hello 풀의 hello ID를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bf022-346">HDInsight에 대해서와 마찬가지로 hello Data Factory 서비스가 Azure 일괄 처리에 대 한 주문형 옵션을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="bf022-347">Azure Data Factory에서는 사용자 고유의 Azure Batch 풀만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="bf022-348">지정 **StorageLinkedService** hello에 대 한 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="bf022-349">Hello 이전 단계에서이 연결 된 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="bf022-350">이 저장소는 파일 및 로그에 대한 준비 영역으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="bf022-351">클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="bf022-352">3단계: 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-352">Step 3: Create datasets</span></span>
<span data-ttu-id="bf022-353">이 단계에서는 toorepresent 입력 데이터 집합 만들기 및 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="bf022-354">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-354">Create input dataset</span></span>
1. <span data-ttu-id="bf022-355">Hello에 **편집기** hello Data Factory에 대 한 클릭 **새 데이터 집합** 단추를 클릭 한 hello 도구 모음 **Azure Blob 저장소** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="bf022-356">Hello를 JSON hello 오른쪽 창에서 다음 JSON 코드 조각은 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
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
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="bf022-357">이 연습에서는 시작 시간: 2015-11-16T00:00:00Z 및 종료 시간: 2015-11-16T05:00:00Z로 나중에 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="bf022-358">예약 된 tooproduce 데이터 **매시간**는 5 입/출력 분할 영역 (사이 **00**: 00:00-\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="bf022-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="bf022-359">hello **주파수** 및 **간격** hello 입력된 데이터 집합 너무 설정 되어**시간** 및 **1**, 즉, 해당 hello 조각 ´ ï ´ 입력 매시간 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="bf022-360">다음으로 표시 된 각 조각에 대 한 hello 시작 시간을은 **SliceStart** JSON 코드 조각은 위에 hello에 시스템 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="bf022-361">**조각**</span><span class="sxs-lookup"><span data-stu-id="bf022-361">**Slice**</span></span> | <span data-ttu-id="bf022-362">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="bf022-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="bf022-363">1</span><span class="sxs-lookup"><span data-stu-id="bf022-363">1</span></span>         | <span data-ttu-id="bf022-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="bf022-365">2</span><span class="sxs-lookup"><span data-stu-id="bf022-365">2</span></span>         | <span data-ttu-id="bf022-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="bf022-367">3</span><span class="sxs-lookup"><span data-stu-id="bf022-367">3</span></span>         | <span data-ttu-id="bf022-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="bf022-369">4</span><span class="sxs-lookup"><span data-stu-id="bf022-369">4</span></span>         | <span data-ttu-id="bf022-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="bf022-371">5</span><span class="sxs-lookup"><span data-stu-id="bf022-371">5</span></span>         | <span data-ttu-id="bf022-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="bf022-373">hello **folderPath** hello 조각 시작 시간의 연도, 월, 일 및 시간 부분을 hello를 사용 하 여 계산 됩니다 (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="bf022-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="bf022-374">따라서 여기는 방법 입력된 폴더는 매핑된 tooa 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="bf022-375">**조각**</span><span class="sxs-lookup"><span data-stu-id="bf022-375">**Slice**</span></span> | <span data-ttu-id="bf022-376">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="bf022-376">**Start time**</span></span>          | <span data-ttu-id="bf022-377">**입력 폴더**</span><span class="sxs-lookup"><span data-stu-id="bf022-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="bf022-378">1</span><span class="sxs-lookup"><span data-stu-id="bf022-378">1</span></span>         | <span data-ttu-id="bf022-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="bf022-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="bf022-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="bf022-381">2</span><span class="sxs-lookup"><span data-stu-id="bf022-381">2</span></span>         | <span data-ttu-id="bf022-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="bf022-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="bf022-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="bf022-384">3</span><span class="sxs-lookup"><span data-stu-id="bf022-384">3</span></span>         | <span data-ttu-id="bf022-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="bf022-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="bf022-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="bf022-387">4</span><span class="sxs-lookup"><span data-stu-id="bf022-387">4</span></span>         | <span data-ttu-id="bf022-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="bf022-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="bf022-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="bf022-390">5</span><span class="sxs-lookup"><span data-stu-id="bf022-390">5</span></span>         | <span data-ttu-id="bf022-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="bf022-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="bf022-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="bf022-393">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **InputDataset** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="bf022-394">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bf022-394">Create output dataset</span></span>
<span data-ttu-id="bf022-395">이 단계에서는 AzureBlob toorepresent hello 출력 데이터 형식이 다른 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="bf022-396">Hello에 **편집기** hello Data Factory에 대 한 클릭 **새 데이터 집합** 단추를 클릭 한 hello 도구 모음 **Azure Blob 저장소** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="bf022-397">Hello를 JSON hello 오른쪽 창에서 다음 JSON 코드 조각은 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
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

    <span data-ttu-id="bf022-398">각 입력 조각에 대해 출력 BLOB/파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="bf022-399">각 조각에 대해 출력 파일의 이름을 지정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="bf022-400">하나의 출력 폴더에 모든 hello 출력 파일이 생성 됩니다: `mycontainer\\outputfolder`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="bf022-401">**조각**</span><span class="sxs-lookup"><span data-stu-id="bf022-401">**Slice**</span></span> | <span data-ttu-id="bf022-402">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="bf022-402">**Start time**</span></span>          | <span data-ttu-id="bf022-403">**출력 파일**</span><span class="sxs-lookup"><span data-stu-id="bf022-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="bf022-404">1</span><span class="sxs-lookup"><span data-stu-id="bf022-404">1</span></span>         | <span data-ttu-id="bf022-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="bf022-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="bf022-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="bf022-407">2</span><span class="sxs-lookup"><span data-stu-id="bf022-407">2</span></span>         | <span data-ttu-id="bf022-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="bf022-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="bf022-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="bf022-410">3</span><span class="sxs-lookup"><span data-stu-id="bf022-410">3</span></span>         | <span data-ttu-id="bf022-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="bf022-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="bf022-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="bf022-413">4</span><span class="sxs-lookup"><span data-stu-id="bf022-413">4</span></span>         | <span data-ttu-id="bf022-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="bf022-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="bf022-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="bf022-416">5</span><span class="sxs-lookup"><span data-stu-id="bf022-416">5</span></span>         | <span data-ttu-id="bf022-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="bf022-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="bf022-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="bf022-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="bf022-419">입력된 폴더에 있는 파일을 hello 모든 기억 (예: 2015-11-16-00) hello 시작 시간으로 분할 영역에 속하는: 2015-11-16-00입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="bf022-420">이 조각이 처리 되 면 hello 사용자 지정 활동 각 파일을 통해 검색 하 고 hello 검색 단어 ("Microsoft")의 발생 수와 hello 출력 파일의 줄을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="bf022-421">Hello 출력 파일에 세 줄은 2015-11-16-00 hello 폴더에 세 개의 파일이 있으면: 2015-11-16-00.txt 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="bf022-422">클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="bf022-423">4 단계: 만들기 및 사용자 지정 활동을 사용 하 여 hello 파이프라인 실행</span><span class="sxs-lookup"><span data-stu-id="bf022-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="bf022-424">이 단계에서는 앞에서 만든 hello 사용자 지정 활동을 하나의 작업으로 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf022-425">Hello를 업로드 하지 않은 경우 **file.txt** tooinput 폴더 hello blob 컨테이너에서 hello 파이프라인 만들기 전에 이렇게 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="bf022-426">hello **isPaused** 속성이 toofalse hello 파이프라인 JSON의 hello 파이프라인 hello로 즉시 실행 되도록 **시작** hello 지난 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="bf022-427">데이터 팩터리 편집기 hello 클릭 **새 파이프라인** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="bf022-428">Hello 명령, 표시 되지 않으면 클릭 **중... (줄임표)**  toosee 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="bf022-429">Hello를 JSON hello 오른쪽 창에서 다음 JSON 스크립트 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="bf022-430">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="bf022-430">Note hello following points:</span></span>

   * <span data-ttu-id="bf022-431">Hello 파이프라인에 활동이 하나만 있고 형식의: **DotNetActivity**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="bf022-432">**AssemblyName** 설정 않으면 hello DLL의 toohello 이름이: **MyDotNetActivity.dll**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="bf022-433">**EntryPoint** 너무 설정**MyDotNetActivityNS.MyDotNetActivity**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="bf022-434">기본적으로 코드에 있는 \<namespace\>.\<classname\>입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="bf022-435">**PackageLinkedService** 너무 설정**StorageLinkedService** hello 사용자 지정 활동 zip 파일이 포함 된 toohello blob 저장소를 가리키는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="bf022-436">입/출력 파일과 hello 사용자 지정 활동 zip 파일에 대 한 서로 다른 Azure 저장소 계정을 사용 하는, 있으면 toocreate 다른 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="bf022-437">이 문서에서는 사용 한다고 가정 hello Azure 저장소 계정과 동일한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="bf022-438">**PackageFile** 너무 설정**customactivitycontainer/MyDotNetActivity.zip**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="bf022-439">Hello 형식: \<containerforthezip\>/\<nameofthezip.zip\>합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="bf022-440">hello 사용자 지정 활동은 **InputDataset** 입력으로 및 **OutputDataset** 출력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="bf022-441">hello **linkedServiceName** hello 사용자 지정 활동의 속성 가리키는 toohello **AzureBatchLinkedService**, toorun Azure 일괄 처리에 필요한 Azure Data Factory 해당 hello 사용자 지정 활동 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="bf022-442">hello **동시성** 설정은 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="bf022-443">Hello 조각이 처리 되는 1, 2 또는 이상의 hello Azure 배치 풀에서 노드를 계산 하는 경우에, hello 기본값을 사용 하는 경우 한 번에 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="bf022-444">따라서 하지 수행한의 Azure 일괄 처리의 hello 병렬 처리 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="bf022-445">설정한 경우 **동시성** tooa 값이 높을수록 예: 2 의미 조각이 두 개 (tootwo 작업 Azure 일괄 처리에 해당) hello에서 처리할 수 있습니다 동일한 시간, 두 가지 경우 모두 hello Vm에 Azure 배치 풀 사용 되는지에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="bf022-446">따라서 hello 동시성 속성을 적절 하 게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="bf022-447">기본적으로 VM에서 언제든지 하나의 작업(조각)이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="bf022-448">hello 이유는 기본적으로는 hello **VM 당 최대 작업** too1 Azure 배치 풀에 대 한 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="bf022-449">필수 구성 요소의 일부로 있습니다 풀을 사용 하 여 만들어지므로이 속성 집합 too2 두 데이터 팩터리 조각이 hello에 VM에서 실행 될 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="bf022-450">**isPaused** 속성이 toofalse 기본적으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="bf022-451">hello 파이프라인 hello 지난 hello 조각 시작 때문에이 예에서 즉시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="bf022-452">이 속성 tootrue toopause hello 파이프라인을 설정 하 고 뒤로 toofalse toorestart를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="bf022-453">hello **시작** 시간 및 **끝** 시간은 5 시간이 더 많이 떨어져 있으며 5 개 조각 hello 파이프라인에 의해 생성 된 하므로 분할 영역 매시간 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="bf022-454">클릭 **배포** hello 명령 모음 toodeploy hello 파이프라인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="bf022-455">5 단계: 테스트 hello 파이프라인</span><span class="sxs-lookup"><span data-stu-id="bf022-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="bf022-456">이 단계에서는 hello 입력된 폴더에 파일을 삭제 하 여 hello 파이프라인을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="bf022-457">입력된 한 폴더를 각각 hello 파이프라인 테스트부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="bf022-458">Data Factory 블레이드에서 hello hello Azure 포털에서에서 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="bf022-459">Hello 다이어그램 뷰에서 입력된 데이터 집합을 두 번 클릭: **InputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="bf022-460">Hello 표시 되어야 **InputDataset** 블 레이 5 모두 분리 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="bf022-461">공지 hello **조각 시작 시간** 및 **조각 종료 시간** 각 조각에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="bf022-462">Hello에 **다이어그램 보기**, 클릭 하 여 지금 **OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="bf022-463">Hello 5 개의 출력 조각만 이미 생성 되었습니다 중인 hello 준비 상태로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="bf022-464">사용 하 여 Azure 포털 tooview hello **작업** hello와 관련 된 **분할 영역** 각 조각에서 실행 하는 어떤 VM을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="bf022-465">자세한 내용은 [Data Factory 및 배치 통합](#data-factory-and-batch-integration) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="bf022-466">Hello hello 출력 파일이 표시 되어야 `outputfolder` 의 `mycontainer` Azure에서 blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="bf022-467">각 입력 조각에 대해 하나씩 5개의 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="bf022-468">Hello의 각 출력 파일 콘텐츠 비슷한 toohello 출력 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="bf022-469">hello 다음 다이어그램에서는 hello 데이터 팩터리 조각이 Azure 일괄 처리에서 tootasks 매핑하 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bf022-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="bf022-470">이 예제에서는 하나의 조각은 하나의 실행만 가집니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="bf022-471">이제 폴더의 여러 파일을 시도해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="bf022-472">파일을 만듭니다: **file2.txt**, **file3.txt**, **file4.txt**, 및 **file5.txt** 같은 hello 폴더에 file.txt 에서처럼 콘텐츠에 hello로: **2015-11-06-01**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="bf022-473">Hello 출력 폴더에 **삭제** hello 출력 파일: **2015-11-16-01.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="bf022-474">Hello에 이제 **OutputDataset** 블레이드에서 마우스 오른쪽 단추로 클릭 hello로 분할 영역 **조각 시작 시간** 도**2015 년 11 월 16 일 01시: 00 AM**를 클릭 하 고 **실행**toorerun/process 다시 hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="bf022-475">이제 hello 분할 영역에 하나의 파일 대신 5 개 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="bf022-476">Hello 조각을 실행 하 고 해당 상태는 후 **준비**,이 조각에 대 한 hello 출력 파일에 hello 내용을 확인 (**2015-11-16-01.txt**) hello에 `outputfolder` 의 `mycontainer` blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="bf022-477">Hello 조각의 각 파일에 대 한 줄이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="bf022-478">5 개의 입력된 파일과 함께 시도 하기 전에 hello 출력 파일 2015-11-16-01.txt를 삭제 하지 않은 경우 실행 hello 이전 조각에서 한 줄 및 5 줄을 실행 하는 hello 현재 조각에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="bf022-479">기본적으로 hello 콘텐츠 파일이 추가 된 toooutput 이미 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="bf022-480">Data Factory 및 배치 통합</span><span class="sxs-lookup"><span data-stu-id="bf022-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="bf022-481">데이터 팩터리 서비스 hello hello 이름의 Azure 일괄 처리에서 작업을 만듭니다: `adf-poolname:job-xxx`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - 배치 작업](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="bf022-483">작업 hello 작업에 조각의 각 활동 실행에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="bf022-484">분할 영역 준비 toobe 10 처리에 있는 경우 10 개의 작업 hello 작업에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="bf022-485">Hello 풀에 여러 계산 노드가 있는 경우 병렬로 실행 중인 둘 이상의 슬라이스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="bf022-486">당 최대 작업 수 hello 계산 노드가 너무 설정 > 1, 있을 수 이상 하나 조각화 hello에서 실행 중인 동일한 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="bf022-487">이 예제에서는 5개 조각이 있으므로 Azure 배치에 5개의 작업이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="bf022-488">Hello로 **동시성** 도**5** hello에서 JSON에 Azure 데이터 팩터리 파이프라인 및 **VM 당 최대 작업** 도**2** Azure 일괄 처리에서 와 풀 **2** Vm hello 작업 실행 빠른 (확인 작업에 대 한 시작 및 종료 시간).</span><span class="sxs-lookup"><span data-stu-id="bf022-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="bf022-489">Hello 포털 tooview hello 일괄 작업 및 hello와 관련 된 작업을 사용 하 여 **분할 영역** 각 조각에서 실행 하는 어떤 VM을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - 배치 작업 태스크](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="bf022-491">Hello 파이프라인을 디버깅</span><span class="sxs-lookup"><span data-stu-id="bf022-491">Debug hello pipeline</span></span>
<span data-ttu-id="bf022-492">디버깅은 몇 가지 기본적인 방법으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="bf022-493">Hello 입력된 조각이 너무 설정 되어 있지 않으면**준비**, hello 입력된 폴더 구조 올바르고 file.txt hello 입력된 폴더에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="bf022-494">Hello에 **Execute** 사용자 지정 활동을 사용 하 여 hello 방식의 **IActivityLogger** 때 도움이 되는 개체 toolog 정보 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="bf022-495">hello 사용자에 기록 하는 hello 메시지 표시\_0 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="bf022-496">Hello에 **OutputDataset** 블레이드에서 hello 조각 toosee hello 클릭 **데이터 조각을** 블레이드 해당 조각에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="bf022-497">해당 조각에 대한 **작업 실행** 이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="bf022-498">Hello 조각에 대 한 실행 하는 하나의 활동이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="bf022-499">클릭 하면 **실행** hello 명령 모음에서 다른 작업 hello에 대 한 실행을 시작할 수 있습니다 동일한 분할 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="bf022-500">Hello hello 작업 실행을 클릭할 때 표시 **작업 실행 세부 정보** 블레이드 로그 파일의 목록과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="bf022-501">Hello에 기록 된 메시지를 확인할 **사용자\_0 로그** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="bf022-502">오류가 발생 하면 hello 재시도 횟수는 hello 파이프라인/활동 JSON에서에서 too3 설정 되어 있으므로 세 가지 활동을 실행 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="bf022-503">Hello 작업 실행을 클릭 하면 tootroubleshoot hello 오류를 검토할 수 있도록 하는 hello 로그 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="bf022-504">로그 파일의 hello 목록에서 클릭 hello **사용자 0.log**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="bf022-505">Hello 오른쪽 패널에서 결과인 hello hello를 사용 하 여 **IActivityLogger.Write** 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf022-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="bf022-506">또한 system-0.log에서 시스템 오류 메시지 및 예외를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="bf022-507">Hello 포함 **PDB** hello 오류 세부 정보와 같은 정보를 포함할 수 있도록 hello zip 파일에 파일 **호출 스택을** 오류가 발생할 경우.</span><span class="sxs-lookup"><span data-stu-id="bf022-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="bf022-508">Hello에 hello 사용자 지정 활동 이어야 hello zip 파일의 파일을 hello 모든 **최상위** 와 하위 폴더 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="bf022-509">해당 hello 확인 **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) 및 **packageLinkedService** (해야 지점 toohello Azure blob 저장소 hello zip 파일이 포함 된) toocorrect 값 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="bf022-510">오류 및 원하는 tooreprocess hello 슬라이스를 수정한 경우 hello hello 조각 마우스 오른쪽 단추로 클릭 **OutputDataset** 블레이드에 대 한 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="bf022-511">`adfjobs`라는 **컨테이너**가 Azure Blob 저장소에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="bf022-512">이 컨테이너는 자동으로 삭제 되지 않지만 테스트 hello 솔루션을 완료 한 후 안전 하 게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="bf022-513">마찬가지로, Data Factory 솔루션 hello 만듭니다 Azure 배치 **작업** 라는: `adf-\<pool ID/name\>:job-0000000001`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="bf022-514">Hello 솔루션을 원하는 경우 테스트 한 후이 작업을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="bf022-515">사용자 지정 활동 hello hello를 사용 하지 않는 **app.config** 패키지에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="bf022-516">따라서 코드 hello 구성 파일에서 모든 연결 문자열에 읽기, 하는 경우 런타임 시 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="bf022-517">hello 모범 사례 toohold Azure 일괄 처리를 사용 하는 경우의 모든 암호는 **Azure KeyVault**인증서 기반 서비스 보안 주체 tooprotect hello keyvault를 사용 하 고 hello 인증서 tooAzure 배치 풀을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="bf022-518">.NET 사용자 지정 활동을 hello 다음 런타임에 KeyVault hello에서 비밀 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="bf022-519">이 솔루션에는 일반적인 템플릿을 이며 tooany 유형의 암호 뿐 아니라 연결 문자열을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="bf022-520">보다 쉽게 해결 (있지만 최상의 방법은 아님): 만들 수는 **Azure SQL 연결 된 서비스** 를 위해 연결 문자열 설정을 사용 하 여 hello 연결 된 서비스 및 더미 입력된 데이터 집합으로 체인 hello 데이터 집합을 데이터 집합 만들기 toohello 사용자 지정.NET 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="bf022-521">액세스 hello hello 사용자 지정 활동 코드에서 서비스의 연결 문자열을 연결 하 고 런타임 시 제대로 작동 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="bf022-522">Hello 샘플을 확장</span><span class="sxs-lookup"><span data-stu-id="bf022-522">Extend hello sample</span></span>
<span data-ttu-id="bf022-523">이 샘플 toolearn에 Azure 데이터 팩터리 및 Azure 일괄 처리 기능에 대해 자세히 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="bf022-524">예를 들어, 다른 시간 범위에서 tooprocess 조각 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="bf022-525">다음 하위 폴더에 hello hello 추가 `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08을 2015-11-16-09, 장소 입력 파일의 해당 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="bf022-526">hello 파이프라인에 대 한 hello 종료 시간을 변경 `2015-11-16T05:00:00Z` 너무`2015-11-16T10:00:00Z`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="bf022-527">Hello에 **다이어그램 보기**, hello를 두 번 클릭 **InputDataset**, hello 입력된 조각이 준비 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="bf022-528">두 번 클릭 **OuptutDataset** 출력 조각만의 toosee hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="bf022-529">준비 상태에 있더라도 hello 출력 파일에 대 한 hello 출력 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="bf022-530">Hello를 늘리거나 **동시성** 설정 toounderstand 솔루션의 hello 성능에 미치는 영향 특히 hello 처리 Azure 일괄 처리에서 발생 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="bf022-531">(4 단계를 참조: 만들고 hello에 대 한 자세한 hello 파이프라인 실행 **동시성** 설정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="bf022-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="bf022-532">상위/하위 **VM당 최대 작업**을 가진 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="bf022-533">toouse hello 새 풀을 만든 업데이트 hello hello Data Factory 솔루션에서 Azure 배치 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="bf022-534">(4 단계를 참조: 만들고 hello에 대 한 자세한 hello 파이프라인 실행 **VM 당 최대 작업** 설정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="bf022-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="bf022-535">**자동 크기 조정** 기능이 있는 Azure 배치 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="bf022-536">Hello 동적인 조절을 처리 응용 프로그램에서 사용 하는 능력은 Azure 배치 풀의 계산 노드를 자동으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="bf022-537">hello 수식 여기에 동작을 수행 하는 hello 달성: hello 풀 처음 만들어질 때 1 VM으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="bf022-538">$PendingTasks 메트릭을 실행 + 활성 (대기) hello 다양 한 작업 정의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="bf022-539">hello 수식은 지난 180 초 동안 hello에 보류 중인 작업의 hello 평균 숫자를 검색 하 고 TargetDedicated를 적절 하 게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="bf022-540">또한 TargetDedicated가 25개의 VM을 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="bf022-541">따라서 새 작업이 제출 되는 대로 풀에서 자동으로 증가 및 완료 작업으로 Vm 하나씩 무료 해지고 해당 Vm을 축소 하는 hello 자동 크기 조정.</span><span class="sxs-lookup"><span data-stu-id="bf022-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="bf022-542">startingNumberOfVMs 및 maxNumberofVMs 조정된 tooyour 요구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="bf022-543">자동 크기 조정 수식:</span><span class="sxs-lookup"><span data-stu-id="bf022-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="bf022-544">자세한 내용은 [Azure 배치 풀에서 자동으로 계산 노드 크기 조정](../batch/batch-automatic-scaling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf022-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="bf022-545">Hello 풀 hello 기본값을 사용 하는 경우 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello 일괄 처리 서비스는 hello 사용자 지정 활동을 실행 하기 전에 tooprepare hello VM 15-30 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="bf022-546">Hello 풀 다른 autoScaleEvaluationInterval를 사용 하는 경우 일괄 처리 서비스 hello autoScaleEvaluationInterval + 10 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="bf022-547">Hello 샘플 솔루션에 hello **Execute** 메서드 호출 hello **Calculate** 입력된 데이터 조각을 tooproduce 출력 데이터 조각을 처리 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf022-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="bf022-548">사용자 고유의 메서드 tooprocess 입력 데이터를 필터링 하 고 hello Calculate 메서드 호출 hello Execute 메서드에서를 호출 tooyour 메서드로 대체를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="bf022-549">다음 단계: hello 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="bf022-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="bf022-550">데이터를 처리한 후 **Microsoft Power BI**와 같은 온라인 도구와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf022-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="bf022-551">다음은 Power BI를 이해 하는 링크 toohelp 방법과 toouse Azure에서:</span><span class="sxs-lookup"><span data-stu-id="bf022-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="bf022-552">Power BI에서 데이터 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="bf022-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="bf022-553">Hello Power BI Desktop 시작</span><span class="sxs-lookup"><span data-stu-id="bf022-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="bf022-554">Power BI에서 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="bf022-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="bf022-555">Azure 및 Power BI - 기본 개요</span><span class="sxs-lookup"><span data-stu-id="bf022-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="bf022-556">참조</span><span class="sxs-lookup"><span data-stu-id="bf022-556">References</span></span>
* [<span data-ttu-id="bf022-557">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="bf022-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="bf022-558">데이터 팩터리 서비스 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf022-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="bf022-559">Azure Data Factory 시작</span><span class="sxs-lookup"><span data-stu-id="bf022-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="bf022-560">Azure Data Factory 파이프라인에서 사용자 지정 작업 사용</span><span class="sxs-lookup"><span data-stu-id="bf022-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="bf022-561">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="bf022-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="bf022-562">Azure 배치의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="bf022-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="bf022-563">Azure 배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="bf022-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="bf022-564">Hello Azure 포털에서에서 Azure 배치 계정 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="bf022-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="bf022-565">Azure 배치 라이브러리 .NET 시작</span><span class="sxs-lookup"><span data-stu-id="bf022-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
