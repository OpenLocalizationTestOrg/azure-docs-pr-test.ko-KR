---
title: "데이터 팩터리 및 배치를 사용하여 대규모 데이터 집합 처리 | Microsoft Docs"
description: "Azure 배치의 병렬 처리 기능을 사용하여 Azure Data Factory 파이프라인에서 대용량 데이터를 처리하는 방법을 설명합니다."
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
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="c63de-103">데이터 팩터리 및 배치를 사용하여 대규모 데이터 집합 처리</span><span class="sxs-lookup"><span data-stu-id="c63de-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="c63de-104">이 문서에서는 예약된 자동 방식으로 대규모 데이터 집합을 이동 및 처리하는 샘플 솔루션의 아키텍처에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="c63de-105">또한 Azure Data Factory 및 Azure 배치를 사용하여 솔루션을 구현하는 종합적인 연습 과정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="c63de-106">이 문서는 전체 샘플 솔루션의 연습을 포함하기 때문에 일반적인 문서보다 깁니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="c63de-107">배치 및 Data Factory를 처음 사용하는 경우 이러한 서비스 및 작동 방식에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="c63de-108">서비스에 대한 정보가 있으며 솔루션을 디자인/설계하는 경우 문서의 [아키텍처 섹션](#architecture-of-sample-solution)을 집중적으로 살펴보고, 프로토타입 또는 솔루션을 개발하는 경우는 [연습](#implementation-of-sample-solution)의 단계별 지침을 진행해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="c63de-109">이 콘텐츠 및 사용 방법에 대한 사용자의 의견을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="c63de-110">첫째, 클라우드에서 대용량 데이터 집합을 처리할 때 Data Factory 및 배치 서비스가 어떻게 도움을 줄 수 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="c63de-111">Azure 배치를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="c63de-111">Why Azure Batch?</span></span>
<span data-ttu-id="c63de-112">Azure 배치를 통해 클라우드에서 효율적으로 대규모 병렬 및 HPC(고성능 컴퓨팅) 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="c63de-113">가상 컴퓨터의 관리된 컬렉션에서 실행되는 계산 집약적인 작업을 예약하는 플랫폼 서비스이며 작업의 요구를 충족하도록 계산 리소스의 규모를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="c63de-114">배치 서비스를 통해 응용 프로그램을 병렬로 규모에 따라 실행하도록 Azure 계산 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="c63de-115">요청 시 또는 예약된 작업을 실행할 수 있으며 HPC 클러스터, 개별 가상 컴퓨터, 가상 네트워크, 복잡한 작업 및 작업 스케줄러 인프라를 수동으로 만들거나 구성하거나 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="c63de-116">Azure 배치에 대해 잘 모를 경우 이 문서에 설명된 솔루션의 아키텍처/구현을 이해하는 데 도움이 되므로 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="c63de-117">Azure 배치의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="c63de-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="c63de-118">배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="c63de-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="c63de-119">(선택 사항) Azure 배치에 대해 자세히 알아보려면 [Azure 배치의 학습 경로](https://azure.microsoft.com/documentation/learning-paths/batch/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="c63de-120">Azure Data Factory를 사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="c63de-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="c63de-121">데이터 팩터리는 데이터의 이동과 변환을 조율하고 자동화하는 클라우드 기반의 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="c63de-122">Data Factory 서비스를 사용하여 온-프레미스 및 클라우드 데이터 저장소에서 중앙 집중식 데이터 저장소(예: Azure Blob 저장소)로 데이터를 이동하고 Azure HDInsight 및 Azure 기계 학습과 같은 서비스를 사용하여 데이터를 처리/변환하는 관리되는 데이터 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="c63de-123">또한 예약된 방식(시간별, 일별, 주별 등)으로 실행되도록 데이터 파이프라인을 예약하고 간편하게 관리하여 문제를 파악한 후 조치를 취할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="c63de-124">Azure Data Factory에 대해 잘 모를 경우 이 문서에 설명된 솔루션의 아키텍처/구현을 이해하는 데 도움이 되므로 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="c63de-125">Azure Data Factory 소개</span><span class="sxs-lookup"><span data-stu-id="c63de-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="c63de-126">첫 번째 데이터 파이프라인 작성</span><span class="sxs-lookup"><span data-stu-id="c63de-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="c63de-127">(선택 사항) Azure Data Factory에 대해 자세히 알아보려면 [Azure Data Factory의 학습 경로](https://azure.microsoft.com/documentation/learning-paths/data-factory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="c63de-128">Data Factory 및 배치</span><span class="sxs-lookup"><span data-stu-id="c63de-128">Data Factory and Batch together</span></span>
<span data-ttu-id="c63de-129">Data Factory에는 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사/이동하기 위한 복사 활동 및 Azure에서 Hadoop(HDInsight) 클러스터를 사용하여 데이터를 처리하는 하이브 활동과 같은 기본 제공 활동이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="c63de-130">지원되는 변환 활동 목록에 대해서는 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="c63de-131">또한 자체 논리에 따라 데이터를 이동 또는 처리하는 사용자 지정 .NET 활동을 만든 후 이러한 활동을 Azure HDInsight 클러스터 또는 Azure VM 배치 풀에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="c63de-132">Azure 배치를 사용할 경우 제공하는 수식에 따라 자동으로 크기가 조정되도록(워크로드에 따라 VM 추가 또는 제거) 풀을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="c63de-133">샘플 솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="c63de-133">Architecture of sample solution</span></span>
<span data-ttu-id="c63de-134">이 문서에 설명된 아키텍처는 단일 솔루션에 대한 것이지만 금융 서비스별 위험 모델링, 이미지 처리 및 렌더링, 유전자 분석 등과 같은 다양한 시나리오와 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="c63de-135">다이어그램은 1) 데이터 팩터리가 데이터 이동 및 처리를 오케스트레이션하는 방법 및 2) Azure 배치가 데이터를 병렬 방식으로 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="c63de-136">쉽게 참조할 수 있도록 다이어그램을 다운로드하고 인쇄합니다(11 x 17인치</span><span class="sxs-lookup"><span data-stu-id="c63de-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="c63de-137">또는 A3 크기). [Azure 배치 및 Data Factory를 사용하여 HPC 및 데이터 오케스트레이션](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="c63de-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="c63de-138">[![대규모 데이터 처리 다이어그램](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="c63de-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="c63de-139">다음 목록은 프로세스의 기본 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="c63de-140">솔루션에는 종단 간 솔루션을 구축하는 코드와 설명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="c63de-141">**계산 노드(VM)의 풀과 함께 Azure 배치를 구성합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="c63de-142">노드 수와 각 노드의 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="c63de-143">**Azure Data Factory 인스턴스를 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="c63de-144">**Data Factory 파이프라인에서 사용자 지정 .NET 작업을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="c63de-145">작업은 Azure 배치 풀에서 실행되는 사용자 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="c63de-146">**Azure storage에 Blob으로 대량의 입력 데이터를 저장합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="c63de-147">데이터는 논리 조각(일반적으로 시간으로)으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="c63de-148">**Data Factory는 보조 위치에 병렬로 처리되는 데이터를 복사합니다** .</span><span class="sxs-lookup"><span data-stu-id="c63de-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="c63de-149">**Data Factory는 배치에서 할당한 풀을 사용하여 사용자 지정 작업을 실행합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="c63de-150">데이터 팩터리는 작업을 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="c63de-151">각 작업은 데이터 조각을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="c63de-152">결과는 Azure 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="c63de-153">**Data Factory에서 응용 프로그램을 통해 배포하거나 다른 도구에서 추가 처리하기 위한 목적으로 최종 결과를 세 번째 위치로 이동합니다**.</span><span class="sxs-lookup"><span data-stu-id="c63de-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="c63de-154">샘플 솔루션의 구현</span><span class="sxs-lookup"><span data-stu-id="c63de-154">Implementation of sample solution</span></span>
<span data-ttu-id="c63de-155">샘플 솔루션은 의도적으로 간단하며, Data Factory 및 배치를 함께 사용하여 데이터 집합을 처리하는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="c63de-156">시계열에 구성된 입력 파일에서 일치하는 검색 단어("Microsoft")의 수를 계산하는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="c63de-157">출력 파일에 개수를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-157">It outputs the count to output files.</span></span>

<span data-ttu-id="c63de-158">**시간**: Azure, Data Factory 및 배치의 기본 사항에 익숙하고 아래 나열된 필수 구성 요소를 완료했다면 이 솔루션이 완료되는 데 1~2시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c63de-159">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c63de-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="c63de-160">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="c63de-160">Azure subscription</span></span>
<span data-ttu-id="c63de-161">Azure 구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c63de-162">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="c63de-163">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c63de-163">Azure storage account</span></span>
<span data-ttu-id="c63de-164">이 자습서에서는 데이터 저장을 위해 Azure 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="c63de-165">Azure 저장소 계정이 없는 경우 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="c63de-166">샘플 솔루션은 Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="c63de-167">Azure 배치 계정</span><span class="sxs-lookup"><span data-stu-id="c63de-167">Azure Batch account</span></span>
<span data-ttu-id="c63de-168">[Azure 포털](http://manage.windowsazure.com/)을 사용하여 Azure 배치 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="c63de-169">[Azure 배치 계정 만들기 및 관리](../batch/batch-account-create-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="c63de-170">Azure 배치 계정 이름 및 계정 키를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="c63de-171">[New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet을 사용하여 Azure 배치 계정을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="c63de-172">이 cmdlet 사용에 대한 자세한 지침은 [Azure 배치 PowerShell cmdlet 시작](../batch/batch-powershell-cmdlets-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="c63de-173">샘플 솔루션은 Azure 배치를 사용하여(간접적으로 Azure Data Factory 파이프라인을 통해) 가상 컴퓨터의 관리되는 컬렉션인 계산 노드의 풀에서 병렬 방식으로 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="c63de-174">VM(가상 컴퓨터)의 Azure 배치 풀</span><span class="sxs-lookup"><span data-stu-id="c63de-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="c63de-175">적어도 2개의 계산 노드로 **Azure 배치 풀**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="c63de-176">[Azure 포털](https://portal.azure.com)에서 왼쪽 메뉴의 **찾아보기**, **배치 계정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="c63de-177">Azure 배치 계정을 선택하여 **배치 계정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="c63de-178">**풀** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="c63de-179">**풀** 블레이드에서 도구 모음의 추가 단추를 클릭하여 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="c63de-180">풀에 대한 ID(**풀 ID**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="c63de-181">Data Factory 솔루션을 만들 때 필요하므로 **풀의 ID**를 메모해둡니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="c63de-182">운영 체제 제품군 설정에 **Windows Server 2012 R2** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="c63de-183">**노드 가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="c63de-184">**대상 전용** 설정 값으로 **2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="c63de-185">**노드당 최대 작업** 설정 값으로 **2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="c63de-186">**확인**을 클릭하여 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="c63de-187">Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="c63de-187">Azure Storage Explorer</span></span>
<span data-ttu-id="c63de-188">[Azure Storage 탐색기 6(도구)](https://azurestorageexplorer.codeplex.com/) 또는 [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer)(ClumsyLeaf 소프트웨어에서).</span><span class="sxs-lookup"><span data-stu-id="c63de-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="c63de-189">클라우드 호스티드 응용 프로그램의 로그를 포함한 Azure Storage 프로젝트의 데이터 검사 및 변경에 대해 이러한 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="c63de-190">개인 액세스로 **mycontainer**라는 컨테이너 만들기(익명 액세스 없음)</span><span class="sxs-lookup"><span data-stu-id="c63de-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="c63de-191">**CloudXplorer**를 사용 중인 경우 다음과 같은 구조의 폴더와 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="c63de-192">`Inputfolder` 및 `outputfolder`는 `mycontainer`에서 최상위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="c63de-193">`inputfolder`는 날짜-시간 스탬프(YYYY-MM-DD-HH)와 함께 하위 폴더를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="c63de-194">**Azure Storage 탐색기**를 사용 중인 경우 다음 단계에서 다음과 같은 이름이 지정된 파일을 업로드 해야 합니다: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` 등</span><span class="sxs-lookup"><span data-stu-id="c63de-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="c63de-195">이 단계는 자동으로 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="c63de-196">키워드 **Microsoft**가 있는 콘텐츠를 사용하여 컴퓨터에 텍스트 파일 **file.txt**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="c63de-197">예: "테스트 사용자 지정 작업 Microsoft 테스트 사용자 지정 작업 Microsoft”</span><span class="sxs-lookup"><span data-stu-id="c63de-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="c63de-198">Azure Blob 저장소의 다음 입력 폴더에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="c63de-199">**Azure 저장소 탐색기**를 사용 중인 경우 파일 **file.txt**를 **mycontainer**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="c63de-200">도구 모음의 **복사**를 클릭하여 Blob의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="c63de-201">**Blob 복사** 대화 상자에서 **대상 Blob 이름**을 `inputfolder/2015-11-16-00/file.txt`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="c63de-202">이 단계를 반복하여 `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` 등을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="c63de-203">이 작업은 자동으로 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="c63de-204">`customactivitycontainer`라는 다른 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="c63de-205">이 컨테이너에 사용자 지정 작업 zip 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="c63de-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c63de-206">Visual Studio</span></span>
<span data-ttu-id="c63de-207">Data Factory 솔루션에서 사용될 사용자 지정 배치 활동을 만들려면 Microsoft Visual Studio 2012 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="c63de-208">솔루션을 만들기 위한 대략적인 단계</span><span class="sxs-lookup"><span data-stu-id="c63de-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="c63de-209">데이터 처리 논리를 포함하는 사용자 지정 활동을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="c63de-210">사용자 지정 작업을 사용하는 Azure 데이터 팩터리 만들기:</span><span class="sxs-lookup"><span data-stu-id="c63de-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="c63de-211">사용자 지정 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-211">Create the custom activity</span></span>
<span data-ttu-id="c63de-212">데이터 팩터리 사용자 지정 작업은 이 샘플 솔루션의 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="c63de-213">샘플 솔루션은 Azure 배치를 사용하여 사용자 지정 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="c63de-214">사용자 지정 작업을 개발하고 Azure 데이터 팩터리 파이프라인에서 사용하는 기본 정보는 [Azure 데이터 팩터리 파이프라인에서 사용자 지정 작업 사용](data-factory-use-custom-activities.md) (영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="c63de-215">Azure Data Factory 파이프라인에서 사용할 .NET 사용자 지정 작업을 만들려면 **IDotNetActivity** 인터페이스를 구현하는 클래스와 함께 **.NET 클래스 라이브러리** 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="c63de-216">이 인터페이스는 **Execute**라는 하나의 메서드만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="c63de-217">해당 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="c63de-218">이 메서드에는 이해해야 하는 몇 가지 주요 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="c63de-219">이 메서드는 다음과 같은 네 개의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="c63de-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="c63de-220">**linkedServices**.</span></span> <span data-ttu-id="c63de-221">입/출력 데이터 원본(예: Azure Blob Storage)을 데이터 팩터리에 연결하는 연결된 서비스의 열거형 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="c63de-222">이 샘플에서는 입력 및 출력 모두에 사용되는 Azure 저장소 형식의 연결된 서비스가 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="c63de-223">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="c63de-223">**datasets**.</span></span> <span data-ttu-id="c63de-224">데이터 집합의 열거형 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="c63de-225">이 매개 변수를 사용하여 입력 및 출력 데이터 집합에 정의된 위치 및 스키마를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="c63de-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="c63de-226">**activity**.</span></span> <span data-ttu-id="c63de-227">이 매개 변수는 현재 계산 엔터티를 나타냅니다(이 경우, Azure 배치 서비스).</span><span class="sxs-lookup"><span data-stu-id="c63de-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="c63de-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="c63de-228">**logger**.</span></span> <span data-ttu-id="c63de-229">로거를 사용하면 파이프라인에 대한 "User" 로그로 노출할 디버그 주석을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="c63de-230">이 메서드는 나중에 사용자 지정 작업을 함께 연결하는 데 사용할 수 있는 사전을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="c63de-231">이 기능은 아직 구현되지 않았기 때문에, 메서드로부터 빈 사전이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="c63de-232">절차: 사용자 지정 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="c63de-233">Visual Studio에서 .NET 클래스 라이브러리 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="c63de-234">**Visual Studio 2012**/**2013/2015**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="c63de-235">**파일**을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="c63de-236">**템플릿**을 확장하고 **Visual C\#**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="c63de-237">이 연습에서는 C\#를 사용하지만 다른 .NET 언어를 사용하여 사용자 지정 작업을 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="c63de-238">오른쪽의 프로젝트 형식 목록에서 **클래스 라이브러리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="c63de-239">**이름**에 **MyDotNetActivity**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="c63de-240">**C:\\ADF**를 **위치**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="c63de-241">존재하지 않는 경우 폴더 **ADF**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="c63de-242">**확인**을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="c63de-243">**도구**를 클릭하고 **NuGet 패키지 관리자**를 가리킨 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="c63de-244">**패키지 관리자 콘솔**에서 다음 명령을 실행하여 **Microsoft.Azure.Management.DataFactories**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="c63de-245">**Azure 저장소** NuGet 패키지를 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="c63de-246">이 샘플에서 Blob 저장소 API를 사용하므로 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="c63de-247">다음 **using** 지시문을 프로젝트의 원본 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-247">Add the following **using** directives to the source file in the project.</span></span>

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
6. <span data-ttu-id="c63de-248">**namespace**의 이름을 **MyDotNetActivityNS**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="c63de-249">클래스 이름을 **MyDotNetActivity**로 변경하고 아래와 같이 **IDotNetActivity** 인터페이스에서 클래스를 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="c63de-250">**IDotNetActivity** 인터페이스의 **Execute** 메서드를 **MyDotNetActivity** 클래스에 구현(추가)하고 다음 샘플 코드를 메서드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="c63de-251">이 메서드에 사용되는 논리에 대한 설명은 [메서드 실행](#execute-method) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
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
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="c63de-252">클래스에 다음과 같은 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="c63de-253">이 메서드는 **Execute** 메서드로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="c63de-254">가장 중요한 점은 **Calculate** 메서드가 각 Blob을 반복하는 코드를 격리한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
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
    /// Gets the fileName value from the input/output dataset.
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
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
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
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="c63de-255">**GetFolderPath** 메서드는 데이터 집합이 가리키는 폴더로 경로를 반환하고 **GetFileName** 메서드는 데이터 집합이 가리키는 Blob/파일의 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="c63de-256">**Calculate** 메서드는 입력 파일(폴더에서 Blob)에서 **Microsoft** 키워드의 인스턴스 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="c63de-257">검색 용어("Microsoft")는 코드에 하드 코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="c63de-258">프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-258">Compile the project.</span></span> <span data-ttu-id="c63de-259">메뉴에서 **빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="c63de-260">**Windows 탐색기**를 시작하고 빌드 유형에 따라 **bin\\debug** 또는 **bin\\release** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="c63de-261">**\\bin\\Debug** 폴더의 이진을 모두 포함하는 **MyDotNetActivity.zip** Zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="c63de-262">오류가 발생할 경우 문제를 발생시킨 소스 코드의 줄 번호 같은 추가 정보를 받을 수 있도록 MyDotNetActivity.**pdb** 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="c63de-263">**ADFTutorialDataFactory**의 연결된 서비스 **StorageLinkedService**가 사용하는 Azure Blob 저장소의 Blob 컨테이너 `customactivitycontainer`에 Blob으로 **MyDotNetActivity.zip**을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="c63de-264">아직 없는 경우 `customactivitycontainer` Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="c63de-265">메서드 실행</span><span class="sxs-lookup"><span data-stu-id="c63de-265">Execute method</span></span>
<span data-ttu-id="c63de-266">이 섹션에서는 Execute 메서드에서 코드에 대한 자세한 내용과 참고 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="c63de-267">입력 컬렉션을 반복하는 멤버는 [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) 네임스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="c63de-268">Blob 컬렉션을 반복하려면 **BlobContinuationToken** 클래스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="c63de-269">본질적으로 루프를 종료하기 위한 메커니즘으로 토큰과 함께 do-while 루프를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="c63de-270">자세한 내용은 [.NET에서 Blob 저장소를 사용하는 방법](../storage/blobs/storage-dotnet-how-to-use-blobs.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c63de-271">기본 루프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
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
   <span data-ttu-id="c63de-272">자세한 내용은 [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) 메서드에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="c63de-273">Blob 집합을 진행하는 코드는 논리적으로 do-while 루프 안으로 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="c63de-274">**Execute** 메서드에서 do-while 루프는 **Calculate**라는 메서드로 Blob 목록을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="c63de-275">이 메서드는 **output** 이라는 문자열 변수를 반환하는데, 이는 세그먼트에서 모든 Blob을 반복한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="c63de-276">**Calculate** 메서드에 전달된 Blob에서 검색 용어(**Microsoft**) 발생 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="c63de-277">**Calculate** 메서드가 작업을 완료한 후에는 새 Blob에 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="c63de-278">따라서 처리된 모든 BLOB 집합에 대해 결과를 새 BLOB에 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="c63de-279">새 BLOB를 작성하려면 먼저 출력 데이터 집합을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="c63de-280">이 코드는 **GetFolderPath** 도우미 메서드도 호출하여 폴더 경로(저장소 컨테이너 이름)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="c63de-281">**GetFolderPath** 는 DataSet 개체를 AzureBlobDataSet로 캐스팅하며 여기에는 FolderPath라는 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="c63de-282">이 코드는 파일 이름(BLOB 이름)을 검색할 **GetFileName** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="c63de-283">이 코드는 폴더 경로를 가져오는 위의 코드와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="c63de-284">파일 이름은 URI 개체를 만들어 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="c63de-285">URI 생성자는 컨테이너 이름을 반환하는 **BlobEndpoint** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="c63de-286">출력 BLOB URI를 생성하기 위해 폴더 경로 및 파일 이름이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="c63de-287">파일 이름이 작성되었고 이제 **Calculate** 메서드에서 새 Blob으로 출력 문자열을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="c63de-288">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-288">Create the data factory</span></span>
<span data-ttu-id="c63de-289">[사용자 지정 작업 만들기](#create-the-custom-activity) 섹션에서 사용자 지정 작업을 만들고 이진과 함께 zip 파일을 업로드하고 PDB 파일을 Azure Blob 컨테이너에 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="c63de-290">이 섹션에서는 **사용자 지정 작업**을 사용하는 **파이프라인**으로 Azure **데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="c63de-291">사용자 지정 작업에 대한 입력 데이터 집합은 Blob 저장소에서 입력 폴더(`mycontainer\\inputfolder`)의 Blob(파일)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="c63de-292">이 작업에 대한 출력 데이터 집합은 Blob 저장소에서 출력 폴더(`mycontainer\\outputfolder`)의 출력 Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="c63de-293">입력 폴더에 있는 하나 이상의 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="c63de-294">예를 들어 각 폴더에 다음과 같은 콘텐츠로 하나의 파일(file.txt)을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="c63de-295">각 입력 폴더는 폴더에 2개 이상의 파일이 포함된 경우에도 Azure Data Factory의 조각에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="c63de-296">각 조각이 파이프라인으로 처리될 때 사용자 지정 작업은 해당 조각에 대한 입력 폴더에서 모든 BLOB를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="c63de-297">동일한 콘텐츠를 가진 5개의 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-297">You see five output files with the same content.</span></span> <span data-ttu-id="c63de-298">예를 들어 2015-11-16-00 폴더의 파일 처리에서 출력 파일은 다음 내용을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="c63de-299">동일한 콘텐츠를 가진 여러 개의 파일(file.txt, file2.txt, file3.txt)을 입력 폴더로 삭제하면 출력 파일에 다음 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="c63de-300">각 폴더(2015-11-16-00 등)는 폴더에 여러 개의 입력 파일이 있더라도 이 샘플에 있는 분할 영역에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="c63de-301">출력 파일은 이제 조각(2015-11-16-00)과 연결된 폴더의 각 입력 파일(Blob)에 하나씩 세 개의 줄을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="c63de-302">각 작업 실행에 대한 작업(task)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-302">A task is created for each activity run.</span></span> <span data-ttu-id="c63de-303">이 샘플에서는 파이프라인에 하나의 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="c63de-304">조각이 파이프라인에 의해 처리될 때 사용자 지정 작업은 조각을 처리하도록 Azure 배치에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="c63de-305">5개 조각(각 조각은 여러 Blob 또는 파일을 가질 수 있음)이 있으므로 Azure 배치에서 생성된 5개의 작업이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="c63de-306">작업이 일괄 처리에서 실행될 때 실제로 사용자 지정 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="c63de-307">다음 연습에서는 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="c63de-308">1단계: 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="c63de-309">[Azure 포털](https://portal.azure.com/)에 로그인한 후에 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="c63de-310">왼쪽 메뉴에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="c63de-311">**새** 블레이드에서 **데이터 + 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="c63de-312">**데이터 분석** 블레이드에서 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="c63de-313">**새 Data Factory** 블레이드에서 이름으로 **CustomActivityFactory**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="c63de-314">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="c63de-315">**"CustomActivityFactory" Data Factory 이름은 사용할 수 없습니다.**라는 오류 메시지가 표시되는 경우 Data Factory 이름을 변경하고(예: **yournameCustomActivityFactory**) 해당 Data Factory를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="c63de-316">**리소스 그룹 이름**을 클릭하여 기존 리소스 그룹을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="c63de-317">데이터 팩터리를 만들려는 구독 및 지역을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="c63de-318">**새 Data Factory** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="c63de-319">Azure 포털의 **대시보드**에 생성된 데이터 팩터리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="c63de-320">데이터 팩터리 만들기를 완료한 후에는 데이터 팩터리 페이지가 표시되며 여기에 데이터 팩터리의 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="c63de-321">2단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-321">Step 2: Create linked services</span></span>
<span data-ttu-id="c63de-322">연결된 서비스는 데이터 저장소 또는 계산 서비스를 Azure Data Factory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="c63de-323">이 단계에서는 **Azure Storage** 계정 및 **Azure 배치** 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c63de-324">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="c63de-325">**CustomActivityFactory**에 대한 **Data Factory** 블레이드에서 **작성 및 배포 타일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="c63de-326">데이터 팩터리 편집기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="c63de-327">명령 모음에서 **새 데이터 저장소**를 클릭하고 **Azure 저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="c63de-328">편집기에 Azure 저장소 연결된 서비스를 만들기 위한 JSON 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="c63de-329">**계정 이름**을 Azure 저장소 계정 이름으로 변경하고 **계정 키**를 Azure 저장소 계정의 액세스 키로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="c63de-330">저장소 액세스 키를 확보하는 방법을 알아보려면 [저장소 액세스 키 보기, 복사 및 다시 생성](../storage/common/storage-create-storage-account.md#manage-your-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="c63de-331">명령 모음에서 **배포** 를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="c63de-332">Azure 배치 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="c63de-333">이 단계에서는 데이터 팩터리 사용자 지정 작업을 실행하는 데 사용될 **Azure 배치** 계정에 대한 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="c63de-334">명령 모음에서 **새 계산**을 클릭하고 **Azure Batch**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="c63de-335">편집기에 Azure 배치 연결된 서비스를 만들기 위한 JSON 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="c63de-336">JSON 스크립트에서:</span><span class="sxs-lookup"><span data-stu-id="c63de-336">In the JSON script:</span></span>

   1. <span data-ttu-id="c63de-337">**계정 이름**을 Azure 배치 계정의 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="c63de-338">**액세스 키**를 Azure 배치 계정의 액세스 키로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="c63de-339">**poolName** 속성에 대한 풀 ID를 입력합니다**.**</span><span class="sxs-lookup"><span data-stu-id="c63de-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="c63de-340">이 속성의 경우 풀 이름 또는 풀 ID 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="c63de-341">**batchUri** JSON 속성에 대한 배치 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="c63de-342">**Azure 배치 계정 블레이드**의 **URL**은 \<accountname\>.\<region\>.batch.azure.com 형식을 사용합니다. **batchUri** JSON 속성의 경우 URL에서 **"accountname."을 제거**한 다음</span><span class="sxs-lookup"><span data-stu-id="c63de-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="c63de-343">해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-343">from the URL.</span></span> <span data-ttu-id="c63de-344">예: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="c63de-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="c63de-345">**poolName** 속성의 경우 풀 이름 대신 풀 ID를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c63de-346">데이터 팩터리 서비스는 HDInsight에 대해서와 마찬가지로 Azure Batch에 대한 주문형 옵션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="c63de-347">Azure Data Factory에서는 사용자 고유의 Azure Batch 풀만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="c63de-348">**linkedServiceName** 속성에 대해 **StorageLinkedService**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="c63de-349">이 연결된 서비스는 이전 단계에서 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="c63de-350">이 저장소는 파일 및 로그에 대한 준비 영역으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="c63de-351">명령 모음에서 **배포**를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="c63de-352">3단계: 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-352">Step 3: Create datasets</span></span>
<span data-ttu-id="c63de-353">이 단계에서는 입력 및 출력 데이터를 나타낼 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="c63de-354">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-354">Create input dataset</span></span>
1. <span data-ttu-id="c63de-355">Data Factory의 **편집기**에서 도구 모음의 **새 데이터 집합** 단추를 클릭하고 드롭다운 메뉴에서 **Azure Blob 저장소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="c63de-356">오른쪽 창의 JSON을 다음 JSON 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="c63de-357">이 연습에서는 시작 시간: 2015-11-16T00:00:00Z 및 종료 시간: 2015-11-16T05:00:00Z로 나중에 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="c63de-358">**매시간** 데이터를 생성하도록 예약되어 있어 5개의 입/출력 조각이 있습니다(**00**:00:00 -\> **05**:00:00 범위).</span><span class="sxs-lookup"><span data-stu-id="c63de-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="c63de-359">입력 데이터 집합의 **빈도** 및 **간격**은 **Hour** 및 **1**로 설정되며 이는 입력 조각이 매시간 제공됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="c63de-360">다음은 각 조각에 대한 시작 시간이며 위의 JSON 코드 조각에서 **SliceStart** 시스템 변수로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="c63de-361">**조각**</span><span class="sxs-lookup"><span data-stu-id="c63de-361">**Slice**</span></span> | <span data-ttu-id="c63de-362">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="c63de-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="c63de-363">1</span><span class="sxs-lookup"><span data-stu-id="c63de-363">1</span></span>         | <span data-ttu-id="c63de-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="c63de-365">2</span><span class="sxs-lookup"><span data-stu-id="c63de-365">2</span></span>         | <span data-ttu-id="c63de-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="c63de-367">3</span><span class="sxs-lookup"><span data-stu-id="c63de-367">3</span></span>         | <span data-ttu-id="c63de-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="c63de-369">4</span><span class="sxs-lookup"><span data-stu-id="c63de-369">4</span></span>         | <span data-ttu-id="c63de-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="c63de-371">5</span><span class="sxs-lookup"><span data-stu-id="c63de-371">5</span></span>         | <span data-ttu-id="c63de-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="c63de-373">**folderPath**는 조각 시작 시간(**SliceStart**)의 연도, 월, 일 및 시간 부분을 사용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="c63de-374">따라서 입력 폴더가 조각에 매핑되는 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="c63de-375">**조각**</span><span class="sxs-lookup"><span data-stu-id="c63de-375">**Slice**</span></span> | <span data-ttu-id="c63de-376">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="c63de-376">**Start time**</span></span>          | <span data-ttu-id="c63de-377">**입력 폴더**</span><span class="sxs-lookup"><span data-stu-id="c63de-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="c63de-378">1</span><span class="sxs-lookup"><span data-stu-id="c63de-378">1</span></span>         | <span data-ttu-id="c63de-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c63de-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="c63de-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="c63de-381">2</span><span class="sxs-lookup"><span data-stu-id="c63de-381">2</span></span>         | <span data-ttu-id="c63de-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c63de-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="c63de-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="c63de-384">3</span><span class="sxs-lookup"><span data-stu-id="c63de-384">3</span></span>         | <span data-ttu-id="c63de-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c63de-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="c63de-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="c63de-387">4</span><span class="sxs-lookup"><span data-stu-id="c63de-387">4</span></span>         | <span data-ttu-id="c63de-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c63de-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="c63de-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="c63de-390">5</span><span class="sxs-lookup"><span data-stu-id="c63de-390">5</span></span>         | <span data-ttu-id="c63de-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c63de-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="c63de-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="c63de-393">도구 모음에서 **배포**를 클릭하여 **InputDataset** 테이블을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="c63de-394">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c63de-394">Create output dataset</span></span>
<span data-ttu-id="c63de-395">이 단계에서는 출력 데이터를 나타내는 다른 AzureBlob 형식의 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="c63de-396">Data Factory의 **편집기**에서 도구 모음의 **새 데이터 집합** 단추를 클릭하고 드롭다운 메뉴에서 **Azure Blob 저장소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="c63de-397">오른쪽 창의 JSON을 다음 JSON 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="c63de-398">각 입력 조각에 대해 출력 BLOB/파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="c63de-399">각 조각에 대해 출력 파일의 이름을 지정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="c63de-400">`mycontainer\\outputfolder`라는 하나의 출력 폴더에 모든 출력 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="c63de-401">**조각**</span><span class="sxs-lookup"><span data-stu-id="c63de-401">**Slice**</span></span> | <span data-ttu-id="c63de-402">**시작 시간**</span><span class="sxs-lookup"><span data-stu-id="c63de-402">**Start time**</span></span>          | <span data-ttu-id="c63de-403">**출력 파일**</span><span class="sxs-lookup"><span data-stu-id="c63de-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="c63de-404">1</span><span class="sxs-lookup"><span data-stu-id="c63de-404">1</span></span>         | <span data-ttu-id="c63de-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c63de-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="c63de-407">2</span><span class="sxs-lookup"><span data-stu-id="c63de-407">2</span></span>         | <span data-ttu-id="c63de-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c63de-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="c63de-410">3</span><span class="sxs-lookup"><span data-stu-id="c63de-410">3</span></span>         | <span data-ttu-id="c63de-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c63de-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="c63de-413">4</span><span class="sxs-lookup"><span data-stu-id="c63de-413">4</span></span>         | <span data-ttu-id="c63de-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c63de-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="c63de-416">5</span><span class="sxs-lookup"><span data-stu-id="c63de-416">5</span></span>         | <span data-ttu-id="c63de-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c63de-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c63de-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="c63de-419">입력 폴더(예: 2015-11-16-00)에 있는 모든 파일은 시작 시간(2015-11-16-00)의 조각 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="c63de-420">이 조각을 처리할 때 사용자 지정 작업은 각 파일을 검색하고 검색 용어("Microsoft") 항목 수와 함께 출력 파일에 줄을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="c63de-421">폴더 2015-11-16-00에 세 개의 파일이 있는 경우 출력 파일(2015-11-16-00.txt)에 세 줄이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="c63de-422">도구 모음에서 **배포**를 클릭하여 **OutputDataset**을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="c63de-423">4단계: 사용자 지정 활동을 사용하여 파이프라인 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="c63de-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="c63de-424">이 단계에서는 이전에 만든 하나의 작업, 사용자 지정 작업을 사용하여 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c63de-425">**file.txt**를 Blob 컨테이너의 입력 폴더에 업로드하지 않은 경우 파이프라인을 만들기 전에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="c63de-426">**isPaused** 속성은 파이프라인 JSON에서 false로 설정되었으므로 파이프라인은 즉시 과거의 **시작** 날짜로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="c63de-427">데이터 팩터리 편집기의 명령 모음에서 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="c63de-428">명령이 표시되지 않으면 **... (줄임표)**을 클릭하여 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="c63de-429">오른쪽 창의 JSON을 다음 JSON 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-429">Replace the JSON in the right pane with the following JSON script:</span></span>

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
   <span data-ttu-id="c63de-430">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-430">Note the following points:</span></span>

   * <span data-ttu-id="c63de-431">파이프라인에는 **DotNetActivity** 유형의 작업 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="c63de-432">**AssemblyName**은 **MyDotNetActivity.dll** DLL 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="c63de-433">**EntryPoint**는 **MyDotNetActivityNS.MyDotNetActivity**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="c63de-434">기본적으로 코드에 있는 \<namespace\>.\<classname\>입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="c63de-435">**PackageLinkedService**가 사용자 지정 작업 zip 파일을 포함하는 Blob 저장소를 가리키는 **StorageLinkedService**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="c63de-436">입/출력 파일 및 사용자 지정 작업 zip 파일에 대해 서로 다른 Azure Storage 계정을 사용하는 경우 다른 Azure Storage 연결된 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="c63de-437">이 문서에서는 동일한 Azure 저장소 계정을 사용 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="c63de-438">**PackageFile**은 **customactivitycontainer/MyDotNetActivity.zip**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="c63de-439">\<containerforthezip\>/\<nameofthezip.zip\> 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="c63de-440">사용자 지정 작업은 입력으로 **InputDataset**, 출력으로 **OutputDataset**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="c63de-441">사용자 지정 활동의 **linkedServiceName** 속성은 **AzureBatchLinkedService**를 가리키며 Azure Data Factory에 사용자 지정 작업을 Azure 배치에서 실행해야 함을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="c63de-442">**동시성** 설정은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="c63de-443">Azure 배치 풀에서 2개 이상의 계산 노드를 가지더라도 1인 기본값을 사용하는 경우 조각은 차례로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="c63de-444">따라서 Azure 배치의 병렬 처리 기능을 활용하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="c63de-445">**동시성**을 더 높은 값, 예를 들어 2로 설정한 경우 2조각(Azure 배치에서 2개의 작업에 해당)은 동시에 처리될 수 있으며 이 경우 Azure 배치 풀의 두 VM이 활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="c63de-446">따라서 동시성 속성을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="c63de-447">기본적으로 VM에서 언제든지 하나의 작업(조각)이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="c63de-448">기본적으로 **VM당 최대 작업**이 Azure 배치 풀에 대해 1로 설정되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="c63de-449">필수 구성의 일부로 2로 설정된 이 속성으로 풀을 만들었으므로 두 개의 데이터 팩터리 조각이 VM에서 동시에 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="c63de-450">**isPaused** 속성은 기본적으로 false로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="c63de-451">이 예제에서는 조각이 이전에 시작되므로 파이프라인이 즉시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="c63de-452">파이프라인을 일시 중지하려면 이 속성을 true로 설정하고 다시 시작하려면 false로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="c63de-453">**start** 시간과 **end** 시간은 5시간 차이이며 파이프라인이 작동하면서 매시간 5개 조각이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="c63de-454">명령 모음에서 **배포**를 클릭하여 파이프라인을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="c63de-455">5단계: 파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="c63de-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="c63de-456">이 단계에서는 입력 폴더에 파일을 삭제하여 파이프라인을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="c63de-457">하나의 입력 폴더당 하나의 파일을 사용하여 파이프라인 테스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="c63de-458">Azure 포털의 Data Factory 블레이드에서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="c63de-459">다이어그램 뷰에서 **InputDataset** 입력 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="c63de-460">모든 5조각이 준비된 상태로 **InputDataset** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="c63de-461">각 조각에 대해 **SLICE START TIME** 및 **SLICE END TIME**입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="c63de-462">**다이어그램 뷰**에서 **OutputDataset**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="c63de-463">5개의 출력 조각이 이미 생성된 경우 준비 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="c63de-464">Azure 포털을 사용하여 **조각**과 연결된 **태스크**를 보고 각 조각이 실행된 VM을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="c63de-465">자세한 내용은 [Data Factory 및 배치 통합](#data-factory-and-batch-integration) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="c63de-466">Azure Blob 저장소에서 `mycontainer`의 `outputfolder`에 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="c63de-467">각 입력 조각에 대해 하나씩 5개의 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="c63de-468">각 출력 파일은 다음 출력과 유사한 콘텐츠를 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="c63de-469">다음 다이어그램에서는 데이터 팩터리 조각이 Azure 배치의 작업에 매핑하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="c63de-470">이 예제에서는 하나의 조각은 하나의 실행만 가집니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="c63de-471">이제 폴더의 여러 파일을 시도해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="c63de-472">파일 만들기: **2015-11-06-01** 폴더의 file.txt와 동일한 콘텐츠를 가진 **file2.txt**, **file3.txt**, **file4.txt** 및 **file5.txt**</span><span class="sxs-lookup"><span data-stu-id="c63de-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="c63de-473">출력 폴더에서 출력 파일 **2015-11-16-01.txt**를 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="c63de-474">이제 **OutputDataset** 블레이드에서 **11/16/2015 01:00:00 AM**으로 설정된 **SLICE START TIME**으로 조각을 오른쪽 단추로 클릭하고 **실행**을 클릭하여 조각을 다시 실행/다시 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="c63de-475">이제 조각에 하나의 파일 대신 5개의 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="c63de-476">조각이 실행되고 해당 상태가 **Ready** 상태가 된 후 Blob 저장소에 있는 `mycontainer`의 `outputfolder`에 있는 이 조각(**2015-11-16-01.txt**)에 대한 출력 파일의 콘텐츠를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="c63de-477">조각의 각 파일에 대한 줄이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="c63de-478">5개의 입력 파일을 시도하기 전에 출력 파일 2015-11-16-01.txt를 삭제하지 않은 경우 이전 조각 실행에서 한 줄이 표시되고 현재 조각 실행에서 5줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="c63de-479">기본적으로 콘텐츠는 이미 있는 경우 출력 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="c63de-480">Data Factory 및 배치 통합</span><span class="sxs-lookup"><span data-stu-id="c63de-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="c63de-481">Data Factory 서비스가 Azure Batch에 `adf-poolname:job-xxx`라는 이름으로 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - 배치 작업](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="c63de-483">조각의 각 작업 실행에 대한 작업(task)이 작업(job)에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="c63de-484">처리를 위해 준비된 10개 조각이 있는 경우 이 작업에 10개 작업(task)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="c63de-485">풀에 여러 계산 노드가 있는 경우 병렬로 실행 중인 두 개 이상의 조각을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="c63de-486">계산 노드당 최대 작업이 1보다 크게 설정된 경우에도 동일한 계산에 실행 중인 두 개 이상의 조각을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="c63de-487">이 예제에서는 5개 조각이 있으므로 Azure 배치에 5개의 작업이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="c63de-488">Azure Data Factory의 파이프라인 JSON에서 **동시성**을 **5**로, **2**개의 VM이 있는 Azure 배치 풀에서 **VM당 최대 태스크**를 **2**로 설정하여 태스크가 매우 빠르게 실행됩니다(태스크에 대한 시작 및 종료 시간 확인).</span><span class="sxs-lookup"><span data-stu-id="c63de-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="c63de-489">포털을 사용하여 배치 작업 및 **조각**과 연결된 작업을 보고 각 조각이 실행된 VM을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - 배치 작업 태스크](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="c63de-491">파이프라인 디버깅</span><span class="sxs-lookup"><span data-stu-id="c63de-491">Debug the pipeline</span></span>
<span data-ttu-id="c63de-492">디버깅은 몇 가지 기본적인 방법으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="c63de-493">입력 조각이 **Ready**로 설정되지 않은 경우 입력 폴더 구조가 올바르고 file.txt가 입력 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="c63de-494">사용자 지정 작업의 **Execute** 메서드에서 **IActivityLogger** 개체를 사용하여 문제 해결에 도움이 되는 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="c63de-495">기록된 메시지는 user\_0.log 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="c63de-496">**OutputDataset** 블레이드에서 조각에 대한 **데이터 조각** 블레이드를 보려면 해당 조각을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="c63de-497">해당 조각에 대한 **작업 실행** 이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="c63de-498">해당 조각에 대한 하나의 작업 실행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="c63de-499">명령 모음에서 **실행**을 클릭하면 동일한 조각에 대해 다른 작업 실행을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="c63de-500">작업 실행을 클릭하면 로그 파일 목록과 함께 **작업 실행 세부 정보** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="c63de-501">기록된 메시지는 **user\_0.log** 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="c63de-502">오류가 발생하면 파이프라인/작업 JSON에서 재시도 횟수가 3으로 설정되므로 세 개의 작업 실행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="c63de-503">작업 실행을 클릭하면 문제 해결을 위해 검토할 수 있는 로그 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="c63de-504">로그 파일 목록에서 **user-0.log**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="c63de-505">오른쪽 패널은 **IActivityLogger.Write** 메서드를 사용한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="c63de-506">또한 system-0.log에서 시스템 오류 메시지 및 예외를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="c63de-507">Zip 파일에 **PDB** 파일을 포함하여 오류 발생 시 오류 세부 정보에 **호출 스택**과 같은 정보가 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="c63de-508">사용자 지정 작업에 대한 zip 파일의 모든 파일은 하위 폴더가 없는 **최상위**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="c63de-509">**assemblyName**(MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile**(customactivitycontainer/MyDotNetActivity.zip) 및 **packageLinkedService**(zip 파일을 포함하는 Azure Blob 저장소를 가리켜야 함)가 올바른 값으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="c63de-510">오류를 해결했고 조각을 다시 처리하려면 **OutputDataset** 블레이드에서 조각을 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="c63de-511">`adfjobs`라는 **컨테이너**가 Azure Blob 저장소에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="c63de-512">이 컨테이너는 자동으로 삭제되지 않지만 솔루션 테스트 후 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="c63de-513">마찬가지로 데이터 팩터리 솔루션은 `adf-\<pool ID/name\>:job-0000000001`이라는 Azure 배치 **작업**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="c63de-514">원하는 경우 솔루션을 테스트한 후 이 작업을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="c63de-515">사용자 지정 작업은 패키지에서 **app.config** 파일을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="c63de-516">따라서 코드가 구성 파일에서 연결 문자열을 읽는 경우 런타임 시 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="c63de-517">Azure 배치를 사용할 경우 **Azure KeyVault**에 모든 암호를 저장하고, 인증서 기반 서비스 주체를 사용하여 KeyVault를 보호하고, 인증서를 Azure 배치 풀에 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="c63de-518">그러면 .NET 사용자 지정 활동은 런타임에 주요 자격 증명 모음의 암호에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="c63de-519">이 솔루션은 일반 솔루션이며 연결 문자열뿐 아니라 모든 유형의 암호로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="c63de-520">최상은 아니지만 좀 더 쉬운 해결 방법이 있습니다. 즉 연결 문자열 설정을 사용하여 **Azure SQL 연결 서비스**를 만들고, 이 서비스를 사용하는 데이터 집합을 만든 다음 사용자 지정 .NET 작업에 이 데이터 집합을 더미 입력 데이터 집합으로 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="c63de-521">그런 후 사용자 지정 활동 코드에서 연결된 서비스의 연결 문자열에 액세스할 수 있습니다. 그러면 런타임에 문제 없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="c63de-522">샘플 확장</span><span class="sxs-lookup"><span data-stu-id="c63de-522">Extend the sample</span></span>
<span data-ttu-id="c63de-523">Azure Data Factory 및 Azure 배치 기능에 대한 자세한 내용을 보려면 이 샘플을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="c63de-524">예를 들어 서로 다른 시간 범위에서 조각을 처리하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="c63de-525">`inputfolder`에 다음 하위 폴더 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09를 추가하고 해당 폴더에 입력 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="c63de-526">`2015-11-16T05:00:00Z`에서 `2015-11-16T10:00:00Z`(으)로 파이프라인에 대한 종료 시간을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="c63de-527">**다이어그램 보기**에서 **InputDataset**을 두 번 클릭하고 입력 조각이 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="c63de-528">**OuptutDataset**을 두 번 클릭하여 출력 조각의 상태를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="c63de-529">준비 상태에 있는 경우 출력 파일에 대한 출력 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="c63de-530">솔루션, 특히 Azure 배치에서 발생하는 처리의 성능에 미치는 영향을 이해하려면 **동시성** 설정을 증가 또는 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="c63de-531">(4단계: **동시성** 설정에 대한 파이프라인 만들기 및 실행을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="c63de-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="c63de-532">상위/하위 **VM당 최대 작업**을 가진 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="c63de-533">만든 새 풀을 사용하려면 데이터 팩터리 솔루션에서 Azure 배치 연결된 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="c63de-534">(4단계: **VM당 최대 작업** 설정에 대한 파이프라인 만들기 및 실행을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="c63de-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="c63de-535">**자동 크기 조정** 기능이 있는 Azure 배치 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="c63de-536">Azure Batch 풀에서 자동으로 계산 노드 크기를 조정하는 것은 응용 프로그램에서 사용하는 처리 능력을 동적으로 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="c63de-537">여기에 나오는 샘플 수식은 다음과 같은 동작을 구현합니다. 풀이 처음 만들어질 때는 VM 1개로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="c63de-538">$PendingTasks 메트릭은 실행되거나 큐에 대기 중인 활성 상태의 작업 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="c63de-539">이 수식은 지난 180초 동안에서 보류 중인 작업의 평균 수를 찾은 후 그에 따라 TargetDedicated를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="c63de-540">또한 TargetDedicated가 25개의 VM을 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="c63de-541">따라서 새 작업이 제출되면 풀이 자동으로 커지고, 작업이 완료되면 VM은 하나씩 사용 가능한 상태로 해제된 후 자동 크기 조정에 따라 해당 VM이 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="c63de-542">startingNumberOfVMs 및 maxNumberofVMs은 요구에 맞게 조정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="c63de-543">자동 크기 조정 수식:</span><span class="sxs-lookup"><span data-stu-id="c63de-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="c63de-544">자세한 내용은 [Azure 배치 풀에서 자동으로 계산 노드 크기 조정](../batch/batch-automatic-scaling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c63de-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="c63de-545">풀에 기본 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)이 사용되는 경우, 배치 서비스가 사용자 지정 작업을 실행하기 전에 VM을 준비하는 데 15~30분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="c63de-546">풀에 다른 autoScaleEvaluationInterval이 사용되는 경우, 배치 서비스는 autoScaleEvaluationInterval +10분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="c63de-547">샘플 솔루션에서 **Execute** 메서드는 출력 데이터 조각을 생성하도록 입력 데이터 조각을 처리하는 **Calculate** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="c63de-548">사용자 고유 메서드를 작성하여 입력 데이터를 처리하고 Execute 메서드의 Calculate 메서드 호출을 사용자 메서드에 호출로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="c63de-549">다음 단계: 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="c63de-549">Next steps: Consume the data</span></span>
<span data-ttu-id="c63de-550">데이터를 처리한 후 **Microsoft Power BI**와 같은 온라인 도구와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="c63de-551">다음은 Power BI 및 Azure에서 사용하는 방법을 이해하는 데 도움을 주는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="c63de-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="c63de-552">Power BI에서 데이터 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="c63de-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="c63de-553">Power BI Desktop 시작</span><span class="sxs-lookup"><span data-stu-id="c63de-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="c63de-554">Power BI에서 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="c63de-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="c63de-555">Azure 및 Power BI - 기본 개요</span><span class="sxs-lookup"><span data-stu-id="c63de-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="c63de-556">참조</span><span class="sxs-lookup"><span data-stu-id="c63de-556">References</span></span>
* [<span data-ttu-id="c63de-557">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="c63de-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="c63de-558">Azure Data Factory 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="c63de-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="c63de-559">Azure Data Factory 시작</span><span class="sxs-lookup"><span data-stu-id="c63de-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="c63de-560">Azure Data Factory 파이프라인에서 사용자 지정 작업 사용</span><span class="sxs-lookup"><span data-stu-id="c63de-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="c63de-561">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="c63de-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="c63de-562">Azure 배치의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="c63de-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="c63de-563">Azure 배치 기능 개요</span><span class="sxs-lookup"><span data-stu-id="c63de-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="c63de-564">Azure 포털에서 Azure 배치 계정 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="c63de-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="c63de-565">Azure 배치 라이브러리 .NET 시작</span><span class="sxs-lookup"><span data-stu-id="c63de-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
