---
title: "자습서 - .NET용 Azure Batch 클라이언트 라이브러리 사용 | Microsoft Docs"
description: "Azure Batch의 기본 개념을 알아보고 .NET을 사용하여 간단한 솔루션을 빌드합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="a66c6-103">.NET용 Batch 클라이언트 라이브러리를 사용한 솔루션 빌드 시작</span><span class="sxs-lookup"><span data-stu-id="a66c6-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a66c6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a66c6-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="a66c6-105">Python</span><span class="sxs-lookup"><span data-stu-id="a66c6-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="a66c6-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a66c6-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="a66c6-107">이 문서에서는 C# 응용 프로그램 예제를 단계별로 설명하면서 [Azure Batch][azure_batch] 및 [Batch .NET][net_api] 라이브러리의 기본에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="a66c6-108">샘플 응용 프로그램에서 Batch 서비스를 활용하여 클라우드에서 병렬 워크로드를 처리하는 방법과 파일 준비 및 검색을 위해 [Azure Storage](../storage/common/storage-introduction.md)와 상호 작용하는 방식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="a66c6-109">일반적인 Batch 응용 프로그램 워크플로를 습득하고 작업, 태스크, 풀 및 계산 노드와 같은 Batch의 주요 구성 요소에 대해 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="a66c6-110">![Batch 솔루션 워크플로(기본)][11]</span><span class="sxs-lookup"><span data-stu-id="a66c6-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="a66c6-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a66c6-111">Prerequisites</span></span>
<span data-ttu-id="a66c6-112">이 문서에는 사용자에게 C# 및 Visual Studio에 대한 실용적인 지식이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="a66c6-113">또한 Azure와 Batch 및 Storage 서비스에 대해 아래 지정된 계정 생성 요구 사항을 충족할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="a66c6-114">계정</span><span class="sxs-lookup"><span data-stu-id="a66c6-114">Accounts</span></span>
* <span data-ttu-id="a66c6-115">**Azure 계정**: Azure 구독이 아직 없는 경우 [무료 Azure 계정][azure_free_account]을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="a66c6-116">**Batch 계정**: Azure 구독이 있으면 [Azure Batch 계정을 만듭니다](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a66c6-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="a66c6-117">**Storage 계정**: [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)의 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66c6-118">Batch는 현재 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)의 5단계 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)에서 설명한 대로 **범용** 저장소 계정 유형*만* 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="a66c6-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a66c6-119">Visual Studio</span></span>
<span data-ttu-id="a66c6-120">샘플 프로젝트를 빌드하려면 **Visual Studio 2015 이상**이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="a66c6-121">[Visual Studio 제품 개요][visual_studio]에서 Visual Studio의 무료 및 평가판 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="a66c6-122">*DotNetTutorial* 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="a66c6-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="a66c6-123">[DotNetTutorial][github_dotnettutorial] 샘플은 GitHub의 [azure-batch-samples][github_samples] 리포지토리에서 찾은 많은 Batch 코드 샘플 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="a66c6-124">리포지토리 홈 페이지에서 **복제 또는 다운로드 > ZIP 다운로드** 단추를 클릭하거나 [azure-batch-samples-master.zip][github_samples_zip] 직접 다운로드 링크를 클릭하여 모든 샘플을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="a66c6-125">ZIP 파일의 내용을 추출하면 다음 폴더에서 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="a66c6-126">Azure Batch 탐색기(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="a66c6-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="a66c6-127">[Azure Batch 탐색기][github_batchexplorer]는 GitHub의 [azure-batch-samples][github_samples] 리포지토리에 포함된 무료 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="a66c6-128">이 자습서를 완료하는 것이 필수는 아니지만 Batch 솔루션을 개발하고 디버깅하는 과정에서 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="a66c6-129">DotNetTutorial 샘플 프로젝트 개요</span><span class="sxs-lookup"><span data-stu-id="a66c6-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="a66c6-130">*DotNetTutorial* 코드 샘플은 두 프로젝트 **DotNetTutorial** 및 **TaskApplication**으로 구성된 Visual Studio 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="a66c6-131">**DotNetTutorial**은 계산 노드(가상 컴퓨터)에서 병렬 워크로드를 실행하기 위해 Batch 및 Storage 서비스와 상호 작용하는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="a66c6-132">DotNetTutorial은 로컬 워크스테이션에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="a66c6-133">**TaskApplication**은 실제 작업을 수행하기 위해 Azure의 계산 노드에서 실행하는 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="a66c6-134">이 예제에서 `TaskApplication.exe`는 Azure Storage에서 다운로드한 파일(입력 파일)의 텍스트를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="a66c6-135">그 후 입력 파일에 표시되는 맨 위 단어 세 개를 포함하는 텍스트 파일(출력 파일)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="a66c6-136">출력 파일을 만든 후에 TaskApplication이 Azure Storage에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="a66c6-137">이렇게 하면 클라이언트 응용 프로그램에서 다운로드가 가능해 집니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="a66c6-138">TaskApplication은 Batch 서비스의 여러 계산 노드에서 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="a66c6-139">다음 다이어그램은 클라이언트 응용 프로그램, *DotNetTutorial*, 태스크에서 실행하는 응용 프로그램, *TaskApplication*에서 수행되는 기본 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="a66c6-140">이러한 기본 워크플로는 Batch를 사용하여 만드는 많은 계산 솔루션의 일반적인 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="a66c6-141">Batch 서비스에서 사용 가능한 모든 기능을 보여 주지 않지만 거의 모든 Batch 시나리오는 이 워크플로의 일부를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="a66c6-142">![Batch 예제 워크플로][8]</span><span class="sxs-lookup"><span data-stu-id="a66c6-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="a66c6-143">**1단계.**</span><span class="sxs-lookup"><span data-stu-id="a66c6-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="a66c6-144">Azure Blob Storage에 **컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="a66c6-145">
[**2단계.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="a66c6-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="a66c6-146">컨테이너에 태스크 응용 프로그램 파일 및 입력 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="a66c6-147">
[**3단계.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="a66c6-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="a66c6-148">Batch **풀**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="a66c6-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="a66c6-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="a66c6-150">**StartTask** 풀은 노드가 풀에 연결되면 태스크 이진 파일(TaskApplication)을 노드에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="a66c6-151">
[**4단계.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="a66c6-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="a66c6-152">Batch **작업**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="a66c6-153">
[**5단계.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="a66c6-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="a66c6-154">작업에 **태스크**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="a66c6-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="a66c6-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="a66c6-156">태스크는 노드에서 실행되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="a66c6-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="a66c6-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="a66c6-158">각 태스크는 Azure Storage에서 입력 데이터를 다운로드한 다음 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="a66c6-159">
[**6단계.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="a66c6-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="a66c6-160">태스크를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="a66c6-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="a66c6-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="a66c6-162">태스크가 완료되면 출력 데이터를 Azure Storage에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="a66c6-163">
[**7단계.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="a66c6-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="a66c6-164">Storage에서 태스크 출력을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-164">Download task output from Storage.</span></span>

<span data-ttu-id="a66c6-165">언급한 바와 같이, 모든 Batch 솔루션이 정확히 이러한 단계를 수행하는 것은 아니며, 훨씬 더 많은 단계를 포함할 수 있지만, *DotNetTutorial* 샘플 응용 프로그램은 Batch 솔루션에서 찾을 수 있는 일반적인 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="a66c6-166">*DotNetTutorial* 샘플 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="a66c6-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="a66c6-167">샘플을 성공적으로 실행할 수 있으려면, *DotNetTutorial* 프로젝트의 `Program.cs` 파일에 Batch 및 Storage 계정 자격 증명을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="a66c6-168">아직 수행하지 않은 경우 `DotNetTutorial.sln` 솔루션 파일을 두 번 클릭하여 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="a66c6-169">또는 **파일 > 열기 > 프로젝트/솔루션** 메뉴를 사용하여 Visual Studio 내에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="a66c6-170">*DotNetTutorial* 프로젝트 내에서 `Program.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="a66c6-171">파일의 위쪽에 지정된 대로 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="a66c6-172">위에서 설명한 대로 현재 Azure Storage에서 **범용** 저장소 계정에 대한 자격 증명을 지정해야 입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="a66c6-173">Batch 응용 프로그램은 **범용** 저장소 계정 내에서 Blob Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="a66c6-174">*Blob 저장소* 계정 유형을 선택하여 만든 Storage 계정에 대한 자격 증명을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="a66c6-175">[Azure Portal][azure_portal]의 각 서비스의 계정 블레이드 내에서 Batch 및 Storage 계정 자격 증명을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="a66c6-176">![포털에서 자격 증명 일괄 처리][9]
![포털의 Storage 자격 증명][10]</span><span class="sxs-lookup"><span data-stu-id="a66c6-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="a66c6-177">자격 증명으로 프로젝트를 업데이트했으므로 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="a66c6-178">메시지가 표시되면 모든 NuGet 패키지 복원을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="a66c6-179">NuGet 패키지가 자동으로 복원되지 않거나 패키지 복원 실패와 관련된 오류가 표시되는 경우 [NuGet 패키지 관리자][nuget_packagemgr]가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="a66c6-180">그런 다음 누락된 패키지의 다운로드를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="a66c6-181">패키지 다운로드를 활성화하려면 [빌드하는 동안 패키지 복원 활성화][nuget_restore]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="a66c6-182">다음 섹션에서는 샘플 응용 프로그램을 Batch 서비스에서 워크로드를 처리하기 위해 수행하는 단계로 세분화하고 이러한 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="a66c6-183">샘플에 있는 코드의 모든 줄이 설명되어 있지 않으므로 이 문서의 나머지 부분에서 작업하는 동안 Visual Studio에서 공개 솔루션을 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="a66c6-184">*DotNetTutorial* 프로젝트의 `Program.cs` 파일에서 `MainAsync` 메서드의 맨 위로 이동하여 단계1부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="a66c6-185">아래 각 단계 후 `MainAsync`에서 메서드 호출의 진행을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="a66c6-186">1단계: Storage 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="a66c6-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="a66c6-187">![Azure Storage에 컨테이너 만들기][1]
</span><span class="sxs-lookup"><span data-stu-id="a66c6-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="a66c6-188">Batch에는 Azure Storage와의 상호 작용을 위해 기본 제공되는 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="a66c6-189">Storage 계정 내의 컨테이너는 Batch 계정에서 실행되는 태스크에 필요한 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="a66c6-190">컨테이너는 태스크가 생성하는 출력 데이터를 저장할 공간도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="a66c6-191">*DotNetTutorial* 클라이언트 응용 프로그램이 실행하는 첫 번째 작업은 [Azure Blob Storage](../storage/common/storage-introduction.md)에 세 개의 컨테이너를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="a66c6-192">**응용 프로그램**: 이 컨테이너는 태스크가 실행하는 응용 프로그램은 물론 DLL과 같은 모든 종속 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="a66c6-193">**입력**: 태스크가 *입력* 컨테이너에서 처리할 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="a66c6-194">**출력**: 태스크가 입력 파일의 처리를 완료하면 그 결과를 *출력* 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="a66c6-195">Storage 계정과 상호 작용하고 컨테이너를 만들기 위해 [.NET용 Azure Storage 클라이언트 라이브러리][net_api_storage]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="a66c6-196">[CloudStorageAccount][net_cloudstorageaccount]로 계정에 대한 참조를 만들고, 그 참조에서 [CloudBlobClient][net_cloudblobclient]를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="a66c6-197">응용 프로그램 전체적으로 `blobClient` 참조를 사용하여 매개 변수로 많은 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="a66c6-198">이 예는 위를 즉시 따르는 코드 블록에 있으며 여기에서 `CreateContainerIfNotExistAsync`를 호출하여 실제로 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="a66c6-199">컨테이너를 만든 후 이제 응용 프로그램은 작업에 의해 사용될 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="a66c6-200">[.NET에서 Blob Storage를 사용하는 방법](../storage/blobs/storage-dotnet-how-to-use-blobs.md)에서는 Azure Storage 컨테이너 및 Blob을 사용한 작업의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="a66c6-201">Batch 작업 시작 단계 읽기 목록의 거의 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="a66c6-202">2단계: 작업 응용 프로그램 및 데이터 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a66c6-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="a66c6-203">![컨테이너에 작업 응용 프로그램 및 입력(데이터) 파일 업로드][2]
</span><span class="sxs-lookup"><span data-stu-id="a66c6-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="a66c6-204">파일 업로드 작업에서 *DotNetTutorial*은 먼저 로컬 컴퓨터에 있는 **응용 프로그램**의 컬렉션 및 **입력** 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="a66c6-205">그런 다음 이전 단계에서 만든 컨테이너에 이러한 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="a66c6-206">업로드 프로세스에 관련된 `Program.cs` 에는 두 가지 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="a66c6-207">`UploadFilesToContainerAsync`: 이 메서드는 [ResourceFile][net_resourcefile] 개체(아래 설명 참조)의 컬렉션을 반환하고 내부적으로 `UploadFileToContainerAsync`을 호출하여 *filePaths* 매개 변수에 전달된 각 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="a66c6-208">`UploadFileToContainerAsync`: 실제로 파일 업로드를 수행하고 [ResourceFile][net_resourcefile] 개체를 만드는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="a66c6-209">파일 업로드 후 파일에 대한 SAS(공유 액세스 서명)을 가져오고 이를 나타내는 ResourceFile 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="a66c6-210">공유 액세스 서명도 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="a66c6-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="a66c6-211">ResourceFiles</span></span>
<span data-ttu-id="a66c6-212">[ResourceFile][net_resourcefile]은 해당 작업을 실행하기 전에 계산 노드에 다운로드되는 Azure Storage의 파일에 대한 URL로 Batch 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="a66c6-213">[ResourceFile.BlobSource][net_resourcefile_blobsource] 속성은 Azure Storage에 있는 파일의 전체 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="a66c6-214">URL에는 파일에 대한 보안 액세스를 제공하는 SAS(공유 액세스 서명)가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="a66c6-215">Batch .NET 내에서 대부분의 작업 형식은 다음을 포함하는 *ResourceFiles* 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="a66c6-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="a66c6-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="a66c6-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="a66c6-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="a66c6-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="a66c6-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="a66c6-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="a66c6-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="a66c6-220">DotNetTutorial 샘플 응용 프로그램은 JobPreparationTask 또는 JobReleaseTask 태스크 유형을 사용하지 않지만 [Azure Batch 계산 노드에서 작업 준비와 완료 태스크 실행](batch-job-prep-release.md)에서 이에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="a66c6-221">공유 액세스 서명(SAS)</span><span class="sxs-lookup"><span data-stu-id="a66c6-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="a66c6-222">공유 액세스 서명은 URL의 일부분으로 포함되는 경우 Azure Storage의 컨테이너 및 Blob에 대한 보안 액세스를 제공하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="a66c6-223">DotNetTutorial 응용 프로그램은 Blob 및 컨테이너 공유 액세스 서명 URL 모두를 사용하고 Storage 서비스에서 이러한 공유 액세스 서명 문자열을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="a66c6-224">**Blob 공유 액세스 서명**: DotNetTutorial에서 풀의 StartTask는 Storage에서 응용 프로그램 이진 및 입력 데이터 파일을 다운로드하는 경우 Blob 공유 액세스 서명을 사용합니다(아래 #3단계 참조).</span><span class="sxs-lookup"><span data-stu-id="a66c6-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="a66c6-225">DotNetTutorial의 `Program.cs`에서 `UploadFileToContainerAsync` 메서드는 각 Blob의 공유 액세스 서명을 가져오는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="a66c6-226">[CloudBlob.GetSharedAccessSignature][net_sas_blob]를 호출하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="a66c6-227">**컨테이너 공유 액세스 서명**: 각 태스크는 계산 노드에서 작업을 완료하면 해당 출력 파일을 Azure Storage의 *출력* 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="a66c6-228">이렇게 하려면 TaskApplication은 파일을 업로드하는 경우 경로의 일부로 컨테이너에 쓰기 액세스를 제공하는 컨테이너 공유 액세스 서명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="a66c6-229">컨테이너 공유 액세스 서명 가져오기는 BLOB 공유 액세스 서명을 가져올 때와 유사한 방식으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="a66c6-230">DotNetTutorial에서 이렇게 하기 위해 `GetContainerSasUrl` 도우미 메서드가 [CloudBlobContainer.GetSharedAccessSignature][net_sas_container]를 호출하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="a66c6-231">“6단계: 작업 모니터링"에서 TaskApplication이 컨테이너 공유 액세스 서명을 사용하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="a66c6-232">공유 액세스 서명에 대해 두 부분으로 이루어진 시리즈, [1부: 공유 액세스 서명(SAS) 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 및 [2부: Blob Storage를 통해 공유 액세스 서명(SAS) 만들기 및 사용](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)을 확인하여 Storage 계정의 데이터에 대한 보안 액세스 제공에 대한 자세한 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="a66c6-233">3단계: Batch 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="a66c6-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="a66c6-234">![Batch 풀 만들기][3]
</span><span class="sxs-lookup"><span data-stu-id="a66c6-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="a66c6-235">Batch **풀**은 Batch가 작업의 태스크를 실행하는 계산 노드(가상 컴퓨터)의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="a66c6-236">Azure Storage API를 사용하여 응용 프로그램 및 데이터 파일을 Storage 계정에 업로드하면 *DotNetTutorial*이 Batch .NET 라이브러리에서 제공한 API를 사용하여 Batch 서비스에 대한 호출을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="a66c6-237">이 코드는 먼저 [BatchClient][net_batchclient]를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="a66c6-238">그런 다음, 샘플이 `CreatePoolIfNotExistsAsync`에 대한 호출을 통해 Batch 계정에 계산 노드의 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="a66c6-239">`CreatePoolIfNotExistsAsync`는 [BatchClient.PoolOperations.CreatePool][net_pool_create] 메서드를 사용하여 Batch 서비스에 새로운 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="a66c6-240">[CreatePool][net_pool_create]을 사용하여 풀을 만들 때 계산 노드 수, [노드의 크기](../cloud-services/cloud-services-sizes-specs.md), 노드의 운영 체제와 같은 매개 변수를 몇 가지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="a66c6-241">*DotNetTutorial*에서 [CloudServiceConfiguration][net_cloudserviceconfiguration]을 사용하여 [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md)의 Windows Server 2012 R2를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="a66c6-242">풀에 대한 [VirtualMachineConfiguration][net_virtualmachineconfiguration]을 지정하여 Azure VM(Virtual Machines)인 계산 노드의 풀을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="a66c6-243">Windows 또는 [Linux 이미지](batch-linux-nodes.md)에서 VM 계산 노드의 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="a66c6-244">VM 이미지에 대한 소스는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="a66c6-245">[Azure Virtual Machines Marketplace][vm_marketplace]: 즉시 사용할 수 있는 Windows 및 Linux 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="a66c6-246">사용자가 준비하고 제공하는 사용자 지정 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="a66c6-247">사용자 지정 이미지에 대한 자세한 내용은 [Batch를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#pool)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66c6-248">Batch의 계산 리소스에 대한 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="a66c6-249">비용을 최소화하려면 샘플을 실행하기 전에 `targetDedicatedComputeNodes`를 1로 낮출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="a66c6-250">이러한 실제 노드 속성과 함께 풀에 대해 [StartTask][net_pool_starttask]를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="a66c6-251">StartTask는 해당 노드가 풀을 연결할 때 각 노드에서 실행하고 이 때마다 노드가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="a66c6-252">StartTask는 작업을 실행하기 전에 계산 노드에서 응용 프로그램을 설치하는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="a66c6-253">예를 들어 태스크에서 Python 스크립트를 사용하여 데이터를 처리하는 경우 계산 노드에서 Python을 설치하는 데 StartTask를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="a66c6-254">이 샘플 응용 프로그램에서 StartTask는 Storage([StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] 속성을 사용하여 지정됨)에서 다운로드하는 파일을 StartTask 작업 디렉터리에서 노드에서 실행되는 *모든* 태스크를 액세스할 수 있는 공유 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="a66c6-255">기본적으로 노드가 풀에 조인하면 `TaskApplication.exe` 및 해당 종속성이 각 노드의 공유 디렉터리에 복사되므로 노드에서 실행되는 모든 작업이 공유 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="a66c6-256">Azure Batch의 **응용 프로그램 패키지** 기능은 풀의 계산 노드로 응용 프로그램을 가져올 수 있는 또 다른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="a66c6-257">자세한 내용은 [Batch 응용 프로그램 패키지를 사용하여 계산 노드에 응용 프로그램 배포](batch-application-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="a66c6-258">위의 코드 조각에서 주목할 만한 것은 StartTask의 *CommandLine* 속성에서 두 개의 환경 변수(`%AZ_BATCH_TASK_WORKING_DIR%` 및 `%AZ_BATCH_NODE_SHARED_DIR%`) 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="a66c6-259">Batch 풀 내의 각 계산 노드는 Batch에 해당하는 몇 가지 환경 변수를 사용하여 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="a66c6-260">태스크에 의해 실행되는 모든 프로세스는 이러한 환경 변수에 대한 액세스를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="a66c6-261">태스크 작업 디렉터리에 대한 정보뿐만 아니라 Batch 풀의 계산 노드에 사용할 수 있는 환경 변수에 대한 자세한 내용은 [개발자를 위한 Batch 기능 개요](batch-api-basics.md)에서 [태스크에 대한 환경 설정](batch-api-basics.md#environment-settings-for-tasks) 및 [파일 및 디렉터리](batch-api-basics.md#files-and-directories) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="a66c6-262">4단계: Batch 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="a66c6-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="a66c6-263">![Batch 작업 만들기][4]</span><span class="sxs-lookup"><span data-stu-id="a66c6-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="a66c6-264">Batch **작업**은 태스크의 컬렉션이며 계산 노드의 풀과 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="a66c6-265">작업의 태스크는 연결된 풀의 계산 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="a66c6-266">워크로드와 관련된 태스크를 구성하고 추적하는 것뿐만 아니라, 작업(더 나아가, 태스크)에 대한 최대 실행 시간은 물론 Batch 계정 내 다른 작업 대비 작업 우선 순위와 같은 제약 조건을 부과하는 데도 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="a66c6-267">하지만 이 예제에서 작업은 3단계에서 만든 풀에만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="a66c6-268">추가적으로 구성되는 다른 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-268">No additional properties are configured.</span></span>

<span data-ttu-id="a66c6-269">모든 Batch 작업은 특정 풀에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="a66c6-270">연결은 작업의 태스크가 실행되는 노드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="a66c6-271">이것은 아래 코드 조각에 표시된 것처럼 [CloudJob.PoolInformation][net_job_poolinfo] 속성을 사용하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="a66c6-272">이제 작업이 만들어졌으므로 작업은 작업 수행에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="a66c6-273">5단계: 작업에 태스크 추가</span><span class="sxs-lookup"><span data-stu-id="a66c6-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="a66c6-274">![작업에 태스크 추가][5]</span><span class="sxs-lookup"><span data-stu-id="a66c6-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="a66c6-275">
*(1) 태스크가 작업에 추가됨, (2) 태스크가 노드에서 실행되도록 예약됨, (3) 태스크가 처리할 데이터 파일을 다운로드함*</span><span class="sxs-lookup"><span data-stu-id="a66c6-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="a66c6-276">Batch **태스크**는 계산 노드에서 실행되는 개별 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="a66c6-277">작업에는 명령줄이 있으며 해당 명령줄에서 지정한 스크립트 또는 실행 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="a66c6-278">실제로 작업을 수행하려면 태스크가 작업에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="a66c6-279">각 [CloudTask][net_task]는 명령줄 속성 및 명령줄이 자동으로 실행되기 전에 태스크가 노드에 다운로드하는 [ResourceFiles][net_task_resourcefiles](풀의 StartTask와 마찬가지로)를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="a66c6-280">*DotNetTutorial* 샘플 프로젝트에서 각 태스크는 파일을 하나만 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="a66c6-281">따라서 ResourceFiles 컬렉션은 단일 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="a66c6-282">`%AZ_BATCH_NODE_SHARED_DIR%` 같은 환경 변수에 액세스하거나 노드의 `PATH`에서 찾을 수 없는 응용 프로그램을 실행하는 경우, 태스크 명령줄에 `cmd /c`를 접두사로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="a66c6-283">이렇게 하면 명령 인터프린터를 명시적으로 실행하고 명령을 수행한 후에 종료하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="a66c6-284">이 요구 사항은 태스크가 노드의 `PATH`(예: *robocopy.exe* 또는 *powershell.exe*)에서 응용 프로그램을 실행하고 환경 변수가 사용되지 않는 경우 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="a66c6-285">위의 코드 조각의 `foreach` 루프 내에서 태스크에 대한 명령줄이 *TaskApplication.exe*에 전달되는 세 개의 명령줄 인수로 구성되어 있는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="a66c6-286">**첫 번째 인수**는 처리할 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="a66c6-287">노드에 있는 것과 같은 파일에 대한 로컬 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="a66c6-288">위의 `UploadFileToContainerAsync`에 ResourceFile 개체를 처음으로 만드는 경우 이 속성(ResourceFile 생성자에 대한 매개 변수로)에 대해 파일 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="a66c6-289">따라서 *TaskApplication.exe*와 동일한 디렉터리에서 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="a66c6-290">**두 번째 인수**는 상위 *N* 단어를 출력 파일에 써야 한다는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="a66c6-291">샘플에서 상위 세 개 단어를 출력 파일에 쓸 수 있도록 하드 코드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="a66c6-292">**세 번째 인수**는 Azure Storage의 **출력** 컨테이너에 쓰기 액세스를 제공하는 공유 액세스 서명(SAS)입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="a66c6-293">*TaskApplication.exe*는 Azure Storage에 출력 파일을 업로드할 때 공유 액세스 서명 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="a66c6-294">TaskApplication 프로젝트의 `Program.cs` 파일에 포함된 `UploadFileToContainer` 메서드에서 이를 위한 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="a66c6-295">6단계: 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="a66c6-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="a66c6-296">![작업 모니터링][6]</span><span class="sxs-lookup"><span data-stu-id="a66c6-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="a66c6-297">
*클라이언트 응용 프로그램이 (1) 태스크의 완료 및 성공 상태를 모니터링하고 (2) 태스크는 결과 데이터를 Azure Storage에 업로드합니다.*</span><span class="sxs-lookup"><span data-stu-id="a66c6-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="a66c6-298">태스크가 작업에 추가되면 작업에 연결된 풀 내에서 계산 노드에서 실행되도록 자동으로 큐에 대기 및 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="a66c6-299">지정한 설정에 따라 Batch는 대기, 예약, 다시 시도하는 모든 작업 및 기타 담당 작업 관리 업무를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="a66c6-300">태스크 실행을 모니터링하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="a66c6-301">DotNetTutorial은 완료 및 태스크 실패 또는 성공 상태에 대해서만 보고하는 간단한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="a66c6-302">DotNetTutorial의 `Program.cs`에 있는 `MonitorTasks` 메서드 내에 설명의 근거가 되는 세 가지 Batch .NET 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="a66c6-303">표시된 순서에 따라 아래 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="a66c6-304">**ODATADetailLevel**: 목록 작업에서 [ODATADetailLevel][net_odatadetaillevel] 지정(작업의 태스크 목록을 가져오는 것과 같은)은 Batch 응용 프로그램 성능을 보장하는 데 반드시 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="a66c6-305">Batch 응용 프로그램 내에서 상태 모니터링을 수행하려는 경우 [효율적인 Azure Batch 서비스 쿼리](batch-efficient-list-queries.md)를 읽기 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="a66c6-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor]는 태스크 상태를 모니터링하기 위한 도우미 유틸리티를 사용하여 Batch .NET 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="a66c6-307">`MonitorTasks`에서 *DotNetTutorial*은 제한 시간 내에서 모든 태스크가 [TaskState.Completed][net_taskstate]에 도달할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="a66c6-308">그 후 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="a66c6-309">**TerminateJobAsync**: [JobOperations.TerminateJobAsync][net_joboperations_terminatejob]로 작업 종료(또는 JobOperations.TerminateJob 차단)는 해당 작업을 완료로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="a66c6-310">Batch 솔루션에서 [JobReleaseTask][net_jobreltask]를 사용하는 경우 반드시 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="a66c6-311">이것은 특수한 유형의 태스크이며, [작업 준비 및 완료 태스크](batch-job-prep-release.md)에 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="a66c6-312">*DotNetTutorial*에서 `Program.cs`의 `MonitorTasks` 메서드는 아래와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="a66c6-313">7단계: 작업 출력 다운로드</span><span class="sxs-lookup"><span data-stu-id="a66c6-313">Step 7: Download task output</span></span>
<span data-ttu-id="a66c6-314">![Storage에서 작업 출력 다운로드][7]</span><span class="sxs-lookup"><span data-stu-id="a66c6-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="a66c6-315">이제 작업이 완료되었으므로 태스크의 출력을 Azure Storage에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="a66c6-316">이 작업은 *DotNetTutorial*의 `Program.cs`에서 `DownloadBlobsFromContainerAsync`에 대한 호출로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="a66c6-317">*DotNetTutorial* 응용 프로그램에서 `DownloadBlobsFromContainerAsync`에 대한 호출은 파일을 `%TEMP%` 폴더에 다운로드해야 하는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="a66c6-318">이 출력 위치를 수정해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="a66c6-319">8단계: 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="a66c6-319">Step 8: Delete containers</span></span>
<span data-ttu-id="a66c6-320">Azure Storage에 있는 데이터에 대한 요금이 부과되므로 Batch 작업에 더 이상 필요 없는 모든 Blob을 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="a66c6-321">DotNetTutorial의 `Program.cs`에서 도우미 메서드 `DeleteContainerAsync`에 대한 세 번의 호출로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="a66c6-322">메서드 자체는 단순히 컨테이너에 대한 참조를 가져온 다음 [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="a66c6-323">9단계: 작업 및 풀 삭제</span><span class="sxs-lookup"><span data-stu-id="a66c6-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="a66c6-324">마지막 단계로, DotNetTutorial 응용 프로그램에서 만든 작업 및 풀을 삭제하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="a66c6-325">작업 및 태스크 자체에 대한 요금이 부과되지 않지만 계산 노드에 대한 요금이 청구 *됩니다*.</span><span class="sxs-lookup"><span data-stu-id="a66c6-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="a66c6-326">따라서 노드를 필요할 때만 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="a66c6-327">사용하지 않는 풀을 삭제하는 것이 유지 관리 프로세스의 일부가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="a66c6-328">BatchClient의 [JobOperations][net_joboperations] 및 [PoolOperations][net_pooloperations]에는 사용자가 삭제를 확인하는 경우 호출되는 것에 해당하는 삭제 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="a66c6-329">계산 리소스에 대해 요금이 부과되고 사용하지 않는 풀 삭제는 비용을 최소화한다는 점을 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="a66c6-330">풀 삭제는 해당 풀 내의 모든 계산 노드를 삭제하고 노드의 모든 데이터는 풀이 삭제되면 복구할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="a66c6-331">*DotNetTutorial* 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="a66c6-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="a66c6-332">샘플 응용 프로그램을 실행하는 경우 콘솔 출력은 다음과 유사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="a66c6-333">실행 중에 풀의 계산 노드가 시작되는 동안 `Awaiting task completion, timeout in 00:30:00...`에서 일시 중지가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="a66c6-334">[Azure Portal][azure_portal]을 사용하여 실행 중 및 실행 후에 풀, 계산 노드, 작업 및 태스크를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="a66c6-335">[Azure portal][azure_portal] 또는 [Azure Storage 탐색기][storage_explorers]를 사용하여 응용 프로그램에서 만든 Storage 리소스(컨테이너 및 Blob)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="a66c6-336">기본 구성에서 응용 프로그램을 실행하는 경우 일반적인 실행 시간은 **약 5분** 입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="a66c6-337">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a66c6-337">Next steps</span></span>
<span data-ttu-id="a66c6-338">다른 계산 시나리오를 실험하려면 *DotNetTutorial* 및 *TaskApplication*을 자유롭게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="a66c6-339">예를 들어, 포털에서 장기 실행 태스크를 시뮬레이션하고 이를 모니터링하려면 [Thread.Sleep][net_thread_sleep] 등을 사용하여 *TaskApplication*에 실행 지연을 추가해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="a66c6-340">더 많은 태스크를 추가하거나 계산 노드 수를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="a66c6-341">실행 시간을 줄이기 위해 기존 풀의 사용을 검사 및 허용하도록 논리를 추가합니다(*힌트*: [azure-batch-samples][github_samples]의 [Microsoft.Azure.Batch.Samples.Common][github_samples_common] 프로젝트에서 `ArticleHelpers.cs`을 확인).</span><span class="sxs-lookup"><span data-stu-id="a66c6-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="a66c6-342">이제 Batch 솔루션의 기본 워크플로에 익숙하다면 Batch 서비스의 추가 기능을 살펴볼 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="a66c6-343">이 서비스를 처음 사용하는 경우 [Azure Batch 기능 개요](batch-api-basics.md) 문서를 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="a66c6-344">[Batch 학습 경로][batch_learning_path]의 **개발 세부 정보** 아래에서 다른 Batch 개발 문서를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="a66c6-345">[TopNWords][github_topnwords] 샘플의 Batch를 사용하여 "상위 n개 단어" 워크로드 처리의 다른 구현을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a66c6-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="a66c6-346">라이브러리의 최신 변경 사항은 Batch .NET [릴리스 정보](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a66c6-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Azure Storage에 컨테이너 만들기"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "컨테이너에 작업 응용 프로그램 및 입력(데이터) 파일 업로드"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch 풀 만들기"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch 작업 만들기"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "작업에 태스크 추가"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "작업 모니터링"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Storage에서 작업 출력 다운로드"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch 솔루션 워크플로(전체 다이어그램)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "포털의 Batch 자격 증명"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "포털의 Storage 자격 증명"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch 솔루션 워크플로(최소 다이어그램)"
