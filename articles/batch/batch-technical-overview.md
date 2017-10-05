---
title: "Azure Batch는 클라우드에서 대규모 병렬 컴퓨팅 솔루션을 실행합니다. | Microsoft Docs"
description: "대규모 병렬 및 HPC 워크로드의 경우 Azure 배치 서비스를 사용하는 방법에 대해 알아봅니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3bda4859e7ce45f5f7b8df6167e6e9d2cedd5c62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a><span data-ttu-id="40f5f-103">Batch를 사용하여 본질적인 병렬 워크로드 실행</span><span class="sxs-lookup"><span data-stu-id="40f5f-103">Run intrinsically parallel workloads with Batch</span></span>

<span data-ttu-id="40f5f-104">Azure 배치는 클라우드에서 대규모 병렬 및 HPC(고성능 컴퓨팅) 응용 프로그램을 효율적으로 실행하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-104">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="40f5f-105">Azure 배치는 가상 컴퓨터의 관리되는 컬렉션에서 실행되는 계산 집약적 작업을 예약하고, 작업 요구에 맞게 계산 리소스의 규모를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-105">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="40f5f-106">Azure 배치를 사용하면 Azure 계산 리소스를 쉽게 정의하여 응용 프로그램을 병렬로 규모에 맞게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-106">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="40f5f-107">HPC 클러스터, 개별 가상 컴퓨터, 가상 네트워크 또는 복잡한 작업 및 태스크 예약 인프라를 수동으로 만들거나 구성하거나 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-107">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="40f5f-108">Azure 배치는 이러한 태스크를 자동화하거나 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-108">Azure Batch automates or simplifies these tasks for you.</span></span>

## <a name="use-cases-for-batch"></a><span data-ttu-id="40f5f-109">배치에 대한 사용 사례</span><span class="sxs-lookup"><span data-stu-id="40f5f-109">Use cases for Batch</span></span>
<span data-ttu-id="40f5f-110">배치는 대용량의 비슷한 태스크를 실행하여 원하는 결과를 얻을 수 있는 *배치 처리* 또는 *배치 컴퓨팅*을 위해 관리되는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-110">Batch is a managed Azure service that is used for *batch processing* or *batch computing*--running a large volume of similar tasks for a desired result.</span></span> <span data-ttu-id="40f5f-111">배치 컴퓨팅은 대량의 데이터를 정기적으로 처리, 변환 및 분석하는 조직에서 가장 일반적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-111">Batch computing is most commonly used by organizations that regularly process, transform, and analyze large volumes of data.</span></span>

<span data-ttu-id="40f5f-112">배치는 본질적으로 병렬("처치 곤란 병렬"이라고도 함) 응용 프로그램 및 워크로드에서 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-112">Batch works well with intrinsically parallel (also known as "embarrassingly parallel") applications and workloads.</span></span> <span data-ttu-id="40f5f-113">본질적으로 병렬 워크로드는 여러 컴퓨터에서 동시에 작업을 수행하는 여러 태스크로 쉽게 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-113">Intrinsically parallel workloads are those that are easily split into multiple tasks that perform work simultaneously on many computers.</span></span>

![병렬 태스크][1]<br/>

<span data-ttu-id="40f5f-115">일반적으로 이 기술을 사용하여 처리되는 워크로드의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-115">Some examples of workloads that are commonly processed using this technique are:</span></span>

* <span data-ttu-id="40f5f-116">재무 위험 모델링</span><span class="sxs-lookup"><span data-stu-id="40f5f-116">Financial risk modeling</span></span>
* <span data-ttu-id="40f5f-117">기후 및 수문학 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="40f5f-117">Climate and hydrology data analysis</span></span>
* <span data-ttu-id="40f5f-118">이미지 렌더링, 분석 및 처리</span><span class="sxs-lookup"><span data-stu-id="40f5f-118">Image rendering, analysis, and processing</span></span>
* <span data-ttu-id="40f5f-119">미디어 인코딩 및 트랜스코딩</span><span class="sxs-lookup"><span data-stu-id="40f5f-119">Media encoding and transcoding</span></span>
* <span data-ttu-id="40f5f-120">유전자 서열 분석</span><span class="sxs-lookup"><span data-stu-id="40f5f-120">Genetic sequence analysis</span></span>
* <span data-ttu-id="40f5f-121">엔지니어링 스트레스 분석</span><span class="sxs-lookup"><span data-stu-id="40f5f-121">Engineering stress analysis</span></span>
* <span data-ttu-id="40f5f-122">소프트웨어 테스트</span><span class="sxs-lookup"><span data-stu-id="40f5f-122">Software testing</span></span>

<span data-ttu-id="40f5f-123">또한 배치는 끝에 감소 단계가 있는 병렬 계산 및 [MPI(메시지 전달 인터페이스)](batch-mpi.md) 응용 프로그램 등 보다 복잡한 HPC 워크로드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-123">Batch can also perform parallel calculations with a reduce step at the end, and execute more complex HPC workloads such as [Message Passing Interface (MPI)](batch-mpi.md) applications.</span></span>

<span data-ttu-id="40f5f-124">Azure에서 배치 및 다른 HPC 솔루션 간의 비교는 [배치 및 HPC 솔루션](batch-hpc-solutions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40f5f-124">For a comparison between Batch and other HPC solution options in Azure, see [Batch and HPC solutions](batch-hpc-solutions.md).</span></span>

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a><span data-ttu-id="40f5f-125">시나리오: 병렬 워크로드 규모 확장</span><span class="sxs-lookup"><span data-stu-id="40f5f-125">Scenario: Scale out a parallel workload</span></span>
<span data-ttu-id="40f5f-126">배치 서비스와 상호 작용하기 위해 배치 API를 사용하는 일반적인 솔루션에는 본질적으로 계산 노드 풀에서 병렬 작업(예: 3D 장면을 위한 이미지 렌더링)의 규모를 확장하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-126">A common solution that uses the Batch APIs to interact with the Batch service involves scaling out intrinsically parallel work--such as the rendering of images for 3D scenes--on a pool of compute nodes.</span></span> <span data-ttu-id="40f5f-127">이 계산 노드 풀은 작업을 렌더링하기 위해 수십, 수백 또는 수천 개의 코어를 제공하는 "렌더 팜"일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-127">This pool of compute nodes can be your "render farm" that provides tens, hundreds, or even thousands of cores to your rendering job, for example.</span></span>

<span data-ttu-id="40f5f-128">다음 다이어그램에서는 병렬 워크로드를 실행하기 위해 배치를 사용하는 클라이언트 응용 프로그램 또는 호스티드 서비스가 있는 일반적인 배치 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-128">The following diagram shows a common Batch workflow, with a client application or hosted service using Batch to run a parallel workload.</span></span>

![배치 솔루션 워크플로][2]

<span data-ttu-id="40f5f-130">이 일반적인 시나리오에서 응용 프로그램 또는 서비스는 다음 단계를 수행하여 Azure 배치에서 계산 워크로드를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-130">In this common scenario, your application or service processes a computational workload in Azure Batch by performing the following steps:</span></span>

1. <span data-ttu-id="40f5f-131">이러한 파일을 처리할 **입력 파일** 및 **응용 프로그램**을 Azure Storage 계정에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-131">Upload the **input files** and the **application** that will process those files to your Azure Storage account.</span></span> <span data-ttu-id="40f5f-132">입력 파일은 응용 프로그램이 처리할 모든 데이터가 될 수 있습니다(예: 금융 모델링 데이터 또는 트랜스코딩할 비디오 파일).</span><span class="sxs-lookup"><span data-stu-id="40f5f-132">The input files can be any data that your application will process, such as financial modeling data, or video files to be transcoded.</span></span> <span data-ttu-id="40f5f-133">응용 프로그램 파일은 데이터를 처리하는 데 사용되는 모든 응용 프로그램일 수 있습니다(3D 렌더링 응용 프로그램 또는 미디어 트랜스코더).</span><span class="sxs-lookup"><span data-stu-id="40f5f-133">The application files can be any application that is used for processing the data, such as a 3D rendering application or media transcoder.</span></span>
2. <span data-ttu-id="40f5f-134">배치 계정에 계산 노드의 배치 **풀**을 만듭니다. 이러한 계산 노드는 태스크를 실행할 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-134">Create a Batch **pool** of compute nodes in your Batch account--these nodes are the virtual machines that will execute your tasks.</span></span> <span data-ttu-id="40f5f-135">노드가 풀에 조인할 때 설치할 응용 프로그램의 Azure Storage에 있는 [노드 크기](../cloud-services/cloud-services-sizes-specs.md), 운영 체제 및 위치와 같은 속성을 지정합니다(1단계에서 업로드한 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="40f5f-135">You specify properties such as the [node size](../cloud-services/cloud-services-sizes-specs.md), their operating system, and the location in Azure Storage of the application to install when the nodes join the pool (the application that you uploaded in step #1).</span></span> <span data-ttu-id="40f5f-136">또한 작업에서 생성되는 워크로드에 대한 응답으로 풀에서 [자동으로 규모를 조정](batch-automatic-scaling.md)하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-136">You can also configure the pool to [automatically scale](batch-automatic-scaling.md) in response to the workload that your tasks generate.</span></span> <span data-ttu-id="40f5f-137">자동 크기 조정은 풀의 계산 노드 수를 동적으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-137">Auto-scaling dynamically adjusts the number of compute nodes in the pool.</span></span>
3. <span data-ttu-id="40f5f-138">배치 **작업** 을 만들어 계산 노드의 풀에서 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-138">Create a Batch **job** to run the workload on the pool of compute nodes.</span></span> <span data-ttu-id="40f5f-139">작업을 만들 때 배치 풀과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-139">When you create a job, you associate it with a Batch pool.</span></span>
4. <span data-ttu-id="40f5f-140">작업에 **태스크** 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-140">Add **tasks** to the job.</span></span> <span data-ttu-id="40f5f-141">작업에 태스크를 추가하는 경우 배치 서비스는 풀의 계산 노드에서 실행할 태스크를 자동으로 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-141">When you add tasks to a job, the Batch service automatically schedules the tasks for execution on the compute nodes in the pool.</span></span> <span data-ttu-id="40f5f-142">각 태스크는 입력 파일을 처리하기 위해 업로드한 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-142">Each task uses the application that you uploaded to process the input files.</span></span>
   
   * <span data-ttu-id="40f5f-143">4a.</span><span class="sxs-lookup"><span data-stu-id="40f5f-143">4a.</span></span> <span data-ttu-id="40f5f-144">태스크가 실행되기 전에 처리할 데이터(입력 파일)을 할당된 계산 노드에 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-144">Before a task executes, it can download the data (the input files) that it is to process to the compute node it is assigned to.</span></span> <span data-ttu-id="40f5f-145">해당 노드에 응용 프로그램이 아직 설치되지 않은 경우(2단계 참조) 대신, 여기서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-145">If the application has not already been installed on the node (see step #2), it can be downloaded here instead.</span></span> <span data-ttu-id="40f5f-146">다운로드가 완료되면 할당된 노드에서 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-146">When the downloads are complete, the tasks execute on their assigned nodes.</span></span>
5. <span data-ttu-id="40f5f-147">태스크가 실행됨에 따라 배치를 쿼리하여 작업 및 태스크의 진행 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-147">As the tasks run, you can query Batch to monitor the progress of the job and its tasks.</span></span> <span data-ttu-id="40f5f-148">클라이언트 응용 프로그램 또는 서비스는 HTTPS를 통해 배치 서비스와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-148">Your client application or service communicates with the Batch service over HTTPS.</span></span> <span data-ttu-id="40f5f-149">수천 개의 계산 노드에서 실행되는 수천 개의 태스크를 모니터링할 수 있으므로 [배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-149">Because you may be monitoring thousands of tasks running on thousands of compute nodes, be sure to [query the Batch service efficiently](batch-efficient-list-queries.md).</span></span>
6. <span data-ttu-id="40f5f-150">태스크가 완료되면 결과 데이터를 Azure 저장소에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-150">As the tasks complete, they can upload their result data to Azure Storage.</span></span> <span data-ttu-id="40f5f-151">또한 계산 노드의 파일 시스템에서 파일을 직접 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-151">You can also retrieve files directly from the file system on a compute node.</span></span>
7. <span data-ttu-id="40f5f-152">모니터링을 통해 작업의 태스크가 완료되었음을 감지하면 클라이언트 응용 프로그램 또는 서비스는 추가 처리 또는 평가를 위해 출력 데이터를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-152">When your monitoring detects that the tasks in your job have completed, your client application or service can download the output data for further processing or evaluation.</span></span>

<span data-ttu-id="40f5f-153">이 방법은 배치를 사용하는 한 가지 방법일 뿐이며 이 시나리오에서는 제공되는 기능 중 일부만 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-153">Keep in mind this is just one way to use Batch, and this scenario describes only a few of its available features.</span></span> <span data-ttu-id="40f5f-154">예를 들어, 각 계산 노드에서 [병렬로 여러 태스크](batch-parallel-node-tasks.md)를 실행할 수 있으며 [작업 준비 및 완료 태스크](batch-job-prep-release.md)를 사용하여 작업을 위한 노드를 준비하고 나중에 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-154">For example, you can execute [multiple tasks in parallel](batch-parallel-node-tasks.md) on each compute node, and you can use [job preparation and completion tasks](batch-job-prep-release.md) to prepare the nodes for your jobs, then clean up afterward.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40f5f-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40f5f-155">Next steps</span></span>
<span data-ttu-id="40f5f-156">지금까지 배치 서비스의 고급 개요를 살펴보았습니다. 이제 서비스를 좀더 자세히 살펴보고 계산 집약적인 병렬 워크로드를 처리하기 위해 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-156">Now that you have a high-level overview of the Batch service, it's time to dig deeper to learn how you can use it to process your compute-intensive parallel workloads.</span></span>

* <span data-ttu-id="40f5f-157">배치를 사용하려는 사용자를 위한 중요한 정보는 [개발자를 위한 배치 기능 개요](batch-api-basics.md)를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-157">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="40f5f-158">문서에는 배치 응용 프로그램을 빌드하는 동안 사용할 수 있는 풀, 노드, 작업 및 태스크와 같은 배치 서비스 리소스 및 여러 API 기능에 대한 자세한 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-158">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="40f5f-159">Batch 솔루션을 빌드하는 데 사용할 수 있는 [Batch API 및 도구](batch-apis-tools.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-159">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
* <span data-ttu-id="40f5f-160">[.NET용 Azure 배치 라이브러리 시작](batch-dotnet-get-started.md) 에서는 일반적인 배치 워크플로를 사용하여 간단한 워크로드를 실행하는 데 C# 및 배치 .NET 라이브러리를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-160">[Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md) to learn how to use C# and the Batch .NET library to execute a simple workload using a common Batch workflow.</span></span> <span data-ttu-id="40f5f-161">이 문서는 배치 서비스 사용 방법을 학습하는 과정의 첫 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-161">This article should be one of your first stops while learning how to use the Batch service.</span></span> <span data-ttu-id="40f5f-162">또한 [Python 버전](batch-python-tutorial.md) 자습서도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-162">There is also a [Python version](batch-python-tutorial.md) of the tutorial.</span></span>
* <span data-ttu-id="40f5f-163">[GitHub의 코드 샘플][github_samples]을 다운로드하여 샘플 워크로드를 예약하고 처리하기 위해 C# 및 Python가 배치와 상호 작용하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40f5f-163">Download the [code samples on GitHub][github_samples] to see how both C# and Python can interface with Batch to schedule and process sample workloads.</span></span>
* <span data-ttu-id="40f5f-164">배치로 작업할 때 사용할 수 있는 리소스를 알아보려면 [배치 학습 경로][learning_path]를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="40f5f-164">Check out the [Batch Learning Path][learning_path] to get an idea of the resources available to you as you learn to work with Batch.</span></span>


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
