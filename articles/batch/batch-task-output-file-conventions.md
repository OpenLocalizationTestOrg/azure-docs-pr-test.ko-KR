---
title: "for.NET-Azure 배치 aaaPersist 작업 및 태스크 출력 hello 파일 규칙 라이브러리와 함께 저장소 tooAzure | Microsoft Docs"
description: ".NET toopersist 일괄 처리 작업에 대 한 toouse Azure 일괄 처리 파일 규칙 라이브러리 및 작업 출력 tooAzure 저장소 및 보기 hello hello Azure 포털에서에서 출력을 지속 방법에 대해 알아봅니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="36162-103">작업을 유지 하 고.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 함께 데이터 tooAzure 저장소 작업</span><span class="sxs-lookup"><span data-stu-id="36162-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="36162-104">한 가지 방법은 toopersist 작업 데이터는 toouse hello [.NET 용 Azure 배치 파일 규칙 라이브러리][nuget_package]합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="36162-105">hello 파일 규칙 라이브러리 프로세스가 간소화 되어 hello 작업 출력을 저장할 경우의 데이터 tooAzure 저장소 및 검색 하기.</span><span class="sxs-lookup"><span data-stu-id="36162-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="36162-106">Hello 파일 규칙 라이브러리 태스크와 클라이언트 모두 코드에서 사용할 수 있습니다 &mdash; 유지 파일에 대 한 작업 코드 및 클라이언트 toolist 코드을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="36162-107">작업 코드에서 사용할 수도 업스트림 작업 라이브러리 tooretrieve hello 출력 hello와 같은 한 [종속성 작업](batch-task-dependencies.md) 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="36162-108">tooretrieve 출력 hello 파일 규칙 라이브러리를 사용 하 여 파일, 작업 또는 작업에 대 한 hello 파일 ID와 목적으로 나열 하 여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="36162-109">Tooknow hello 이름 또는 hello 파일의 위치가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="36162-110">예를 들어 지정된 된 태스크에 대 한 hello 파일 규칙 라이브러리 toolist 모든 중간 파일을 사용 하거나 지정된 된 작업에 대 한 미리 보기 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="36162-111">2017-05-01 버전 부터는 hello 일괄 처리 서비스 API 작업 및 가상 컴퓨터 구성 hello 사용 하 여 만든 풀에서 실행 되는 작업 관리자 작업에 대 한 유지 출력 데이터 tooAzure 저장소를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="36162-112">hello 일괄 처리 서비스 API 작업을 만들고 역할을 대체 toohello 파일 규칙 라이브러리는 hello 코드 내에서 출력 하는 간단한 방법을 toopersist를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="36162-113">작업을 실행 하는 tooupdate hello 응용 프로그램 필요 없이 일괄 처리 클라이언트 응용 프로그램 toopersist 출력을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="36162-114">자세한 내용은 참조 [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="36162-115">Hello 파일 규칙 라이브러리 toopersist 작업 출력을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="36162-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="36162-116">Azure 일괄 처리는 한 가지 방법은 더 toopersist 작업 출력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="36162-117">hello 파일 규칙은 가장 적합 한 toothese 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="36162-118">작업 hello 파일 규칙 라이브러리를 사용 하 여 toopersist 파일 실행 되 고 있는지 hello 응용 프로그램에 대 한 hello 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="36162-119">원하는 toostream 데이터 tooAzure 저장소 hello 작업 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="36162-120">Toopersist 데이터 hello 클라우드 서비스 구성 또는 hello 가상 컴퓨터 구성 중 하나를 사용 하 여 만든 풀에서 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="36162-121">클라이언트 응용 프로그램 또는 hello의 다른 작업이 요구 toolocate 작업 하 고 ID 또는 용도 따라 작업 출력 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="36162-122">Tooview 작업 출력을 hello Azure 포털에서에서 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="36162-123">시나리오와 다른 경우 위에 나열 된 다른 접근 방법이 tooconsider를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="36162-124">지속 작업 출력에 대 한 다른 옵션에 대 한 자세한 내용은 참조 하십시오. [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="36162-125">Hello 표준 일괄 처리 파일 규칙 이란?</span><span class="sxs-lookup"><span data-stu-id="36162-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="36162-126">hello [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) hello 대상 컨테이너와 blob 경로 toowhich 출력 파일이 작성 되는 이름 지정 체계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="36162-127">파일 지속형된 tooAzure toohello 표준 파일 규칙을 준수 하는 저장소 자동으로 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="36162-128">hello 포털 hello 명명 규칙을 인식 하며 따라서 tooit 준수 하는 파일을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="36162-129">.NET 용 hello 파일 규칙 라이브러리 이름을 저장소 컨테이너 및 태스크 출력 파일 toohello 표준 파일 규칙에 따라 자동으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="36162-130">또한 hello 파일 규칙 라이브러리 toojob ID, 작업 ID 또는 용도 따라 메서드 tooquery 출력 파일이 Azure 저장소에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="36162-131">.NET 이외의 다른 언어로 개발 하는 경우 직접 구현할 수 있습니다 hello 파일 규칙 표준 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="36162-132">자세한 내용은 참조 [hello 일괄 처리 파일 규칙 표준에 대 한](batch-task-output.md#about-the-batch-file-conventions-standard)합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="36162-133">Azure 저장소 계정 tooyour 일괄 처리 계정 연결</span><span class="sxs-lookup"><span data-stu-id="36162-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="36162-134">출력 데이터 tooAzure toopersist hello 파일 규칙 라이브러리를 사용 하 여 저장소를 먼저 연결 해야 Azure 저장소 계정 tooyour 일괄 처리 계정.</span><span class="sxs-lookup"><span data-stu-id="36162-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="36162-135">아직 수행 하지 않은 경우 일괄 처리 계정에는 저장소 계정 tooyour hello를 사용 하 여 연결 [Azure 포털](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="36162-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="36162-136">Hello Azure 포털에서에서 tooyour 일괄 처리 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="36162-137">**설정**에서 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="36162-138">배치 계정과 연결된 저장소 계정이 아직 없으면 **저장소 계정(없음)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="36162-139">구독에 대 한 hello 목록에서 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="36162-140">최상의 성능을 위해 hello에 해당 하는 Azure 저장소 계정을 사용 하 여 작업이 실행 되 고 있는 일괄 처리 계정 hello와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="36162-141">출력 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="36162-141">Persist output data</span></span>

<span data-ttu-id="36162-142">toopersist job 및 task hello 파일 규칙 라이브러리를 사용 하 여 데이터를 출력를 Azure 저장소의 컨테이너를 만든 다음 hello 출력 toohello 컨테이너를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="36162-143">사용 하 여 hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) 작업 코드 tooupload hello 작업 출력 toohello 컨테이너의 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="36162-144">Azure Storage의 컨테이너와 Blob 사용에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36162-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="36162-145">작업 및 작업에 대 한 모든 출력 라이브러리에 저장 된 hello 파일 규칙을 통해 지속 hello 동일한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="36162-146">많은 수의 작업을 시도 하는 경우 toopersist 파일에 hello 동일한 시간 [조절 제한 저장소](../storage/common/storage-performance-checklist.md#blobs) 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="36162-147">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="36162-147">Create storage container</span></span>

<span data-ttu-id="36162-148">toopersist 작업 출력 tooAzure 저장소를 먼저 호출 하 여 컨테이너를 만들 [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="36162-149">이 확장 메서드는 [CloudStorageAccount][net_cloudstorageaccount] 개체를 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="36162-150">명명 된 따라 toohello 파일 규칙 콘텐츠를 검색할 수 있도록 표준 hello hello 문서의 뒷부분에 설명 된 Azure 포털 및 hello 검색 메서드는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36162-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="36162-151">일반적으로 클라이언트 응용 프로그램의 hello 코드 toocreate 컨테이너에 넣으면 &mdash; hello 풀, 작업 및 작업을 만드는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="36162-152">태스크 출력 저장</span><span class="sxs-lookup"><span data-stu-id="36162-152">Store task outputs</span></span>

<span data-ttu-id="36162-153">작업 출력 toohello 컨테이너 hello를 사용 하 여 저장할 수는 Azure 저장소의 컨테이너를 준비 했으므로, 이제 [TaskOutputStorage] [ net_taskoutputstorage] hello 파일 규칙 라이브러리에 클래스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="36162-154">작업 코드에서 먼저 만듭니다는 [TaskOutputStorage] [ net_taskoutputstorage] 개체를 다음 hello 작업의 작업 완료 되 면 호출 hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] 메서드 toosave 해당 출력 tooAzure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="36162-155">hello `kind` hello의 매개 변수 [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) 메서드 분류 hello 파일을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="36162-156">미리 정의된 4개의 [TaskOutputKind][net_taskoutputkind] 형식, 즉 `TaskOutput`, `TaskPreview`, `TaskLog` 및 `TaskIntermediate.`가 있습니다. 사용자 정의 범주의 출력도 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="36162-157">이러한 출력 형식을 사용 하면 toospecify 어떤 유형의 출력 toolist 나중 hello에 대 한 일괄 처리를 쿼리할 때 지정된 된 태스크의 출력을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="36162-158">즉, 작업에 대 한 hello 출력 나열 하는 경우 hello 출력 형식 중 하나에 hello 목록을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="36162-159">예를 들어 "hello를 되돌리지 *미리 보기* 작업에 대 한 출력 *109*."</span><span class="sxs-lookup"><span data-stu-id="36162-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="36162-160">에 표시를 나열 하 고 출력을 검색에 대 한 자세한 [출력을 검색](#retrieve-output) hello 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="36162-161">hello 출력 종류 결정 hello Azure 포털 특정 파일 나타나는 한 위치: *TaskOutput*-분류 된 파일이 아래에 나타납니다 **작업 출력 파일**, 및 *TaskLog*파일이 아래에 나타납니다 **로그 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="36162-162">작업 출력 저장</span><span class="sxs-lookup"><span data-stu-id="36162-162">Store job outputs</span></span>

<span data-ttu-id="36162-163">또한 toostoring 태스크 출력에 연결 된 전체 작업 hello 출력 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="36162-164">예를 들어 영화 렌더링 작업의 hello 병합 작업에서는 작업 출력으로 완벽 하 게 렌더링 하는 hello 영화를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="36162-165">작업이 완료 된 클라이언트 응용 프로그램 나열 하 고 hello 출력 hello 작업에 대 한 검색할 수 및 않습니다 하지 필요 tooquery hello 개별 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="36162-166">Hello를 호출 하 여 작업 출력을 저장할 [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] 메서드를 hello 지정 [JobOutputKind] [ net_joboutputkind] 및 파일 이름:</span><span class="sxs-lookup"><span data-stu-id="36162-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="36162-167">Hello와 마찬가지로 **TaskOutputKind** 형식 hello를 사용 하면 작업 출력에 대 한 [JobOutputKind] [ net_joboutputkind] 형식 toocategorize 작업의 파일을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="36162-168">이 매개 변수는 특정 유형의 출력 (목록)에 대 한 쿼리를 toolater 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="36162-169">hello **JobOutputKind** 유형의 출력과 미리 보기 범주를 포함 하 고 사용자 지정 범주 만들기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="36162-170">태스크 로그 저장</span><span class="sxs-lookup"><span data-stu-id="36162-170">Store task logs</span></span>

<span data-ttu-id="36162-171">또한 toopersisting 파일 toodurable 저장소 작업 또는 작업 하는 경우 완료 되 면 toopersist 파일 작업의 hello 실행 중에 업데이트를 할 수 있습니다 &mdash; 로그 파일 또는 `stdout.txt` 및 `stderr.txt`, 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="36162-172">이 작업을 위해 hello Azure 일괄 처리 파일 규칙 라이브러리는 hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] 메서드.</span><span class="sxs-lookup"><span data-stu-id="36162-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="36162-173">와 [SaveTrackedAsync][net_savetrackedasync], (사용자가 지정한 간격) 마다 hello 노드에서 업데이트 tooa 파일을 추적 하 고 해당 업데이트 tooAzure 저장소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="36162-174">다음 코드 조각 hello를 사용 하 여 [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` hello hello 작업을 실행 하는 동안은 15 초 마다 Azure 저장소에서:</span><span class="sxs-lookup"><span data-stu-id="36162-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="36162-175">섹션을 주석 처리 된 hello `Code tooprocess data and produce output file(s)` 작업은 일반적으로 수행 하는 hello 코드에 대 한 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="36162-176">예를 들어 Azure Storage에서 데이터를 다운로드하고 변환 또는 계산을 수행하는 코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="36162-177">어떻게 이러한 코드에 래핑할 수 있습니다이 조각의 hello 중요 한 부분을 입증 하 고는 `using` 와 파일을 업데이트 하는 블록 tooperiodically [SaveTrackedAsync][net_savetrackedasync]합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="36162-178">hello 노드 에이전트는 hello 풀의 각 노드에서 실행 되 고 hello 노드와 hello 일괄 처리 서비스 간의 hello 명령 컨트롤 인터페이스를 제공 하는 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="36162-179">hello `Task.Delay` 콜이이 hello 끝에 필요한 `using` 노드 에이전트 hello 블록 tooensure 내용이 시간 tooflush hello 표준의 hello 노드에서 toohello stdout.txt 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="36162-180">이러한 지연 시간 없이 것은 가능한 toomiss hello 출력의 마지막 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="36162-181">이 지연 시간은 일부 파일에만 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="36162-182">사용 하는 추적 파일을 사용 하면 **SaveTrackedAsync**만 *추가* toohello 추적 된 파일 지속형된 tooAzure 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36162-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="36162-183">이 메서드를 사용 하 여 추적 회전 아닌 로그 파일에 대해서만 또는 toowith 작성 된 기타 파일 추가 작업 toohello hello 파일 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="36162-184">출력 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="36162-184">Retrieve output data</span></span>

<span data-ttu-id="36162-185">Hello Azure 일괄 처리 파일 규칙 라이브러리를 사용 하 여 지속형된 출력을 검색 하는 경우 이렇게 하면 작업 및 작업 중심 방식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="36162-186">Hello에 대 한 출력 작업 또는 작업 지정한 tooknow 필요 없이 해당 파일 이름 또는 Azure 저장소에 해당 경로 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="36162-187">대신 태스크별 또는 작업 ID별로 출력 파일을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="36162-188">hello 다음 코드 조각 반복 작업의 작업, hello 작업에 대 한 hello 출력 파일에 대 한 일부 정보 출력을 다음 저장소에서 해당 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="36162-189">Hello Azure 포털에서에서 출력 파일 보기</span><span class="sxs-lookup"><span data-stu-id="36162-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="36162-190">hello Azure 포털 작업 출력 파일 표시 하 고 로그는 지속형된 tooa hello를 사용 하 여 Azure 저장소 계정을 연결 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="36162-191">Hello, 선택한 언어에에서 직접이 규칙을 구현할 수 있습니다 또는.NET 응용 프로그램에서 hello 파일 규칙 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="36162-192">hello 포털에 출력 파일의 tooenable hello 디스플레이 hello 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="36162-193">[Azure 저장소 계정 연결](#requirement-linked-storage-account) tooyour 일괄 처리 계정.</span><span class="sxs-lookup"><span data-stu-id="36162-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="36162-194">출력을 유지할 때 toohello 미리 정의 된 저장 컨테이너 및 파일에 대 한 명명 규칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="36162-195">Hello 파일 규칙 라이브러리에서 이러한 규칙의 hello 정의 찾을 수 있습니다 [README][github_file_conventions_readme]합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="36162-196">Hello를 사용 하는 경우 [Azure 일괄 처리 파일 규칙] [ nuget_package] 라이브러리 toopersist 프로그램 출력을 파일 toohello 표준 파일 규칙에 따라 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36162-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="36162-197">toohello 작업에 관심이 있는 출력을 가진 클릭 한 다음 탐색, tooview 작업 출력 파일 및 hello Azure 포털 로그인 **Saved 출력 파일** 또는 **저장 된 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="36162-198">이 이미지는 hello **Saved 출력 파일** ID "007" hello, 작업에 대 한:</span><span class="sxs-lookup"><span data-stu-id="36162-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="36162-199">![태스크 출력 블레이드 hello Azure 포털에서][2]</span><span class="sxs-lookup"><span data-stu-id="36162-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="36162-200">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="36162-200">Code sample</span></span>

<span data-ttu-id="36162-201">hello [PersistOutputs] [ github_persistoutputs] 샘플 프로젝트를 사용 하면 hello 중 하나인 [Azure 배치 코드 샘플] [ github_samples] GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="36162-202">이 Visual Studio 솔루션 toouse hello Azure 일괄 처리 파일 규칙 라이브러리 toopersist 작업 toodurable 저장소를 출력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36162-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="36162-203">toorun hello 예제를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="36162-204">프로젝트 열기 hello **Visual Studio 2015 이상**합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="36162-205">일괄 처리 및 저장소 추가 **계정 자격 증명** 너무**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="36162-206">**빌드** (하지만 실행 하지 않는) hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="36162-207">메시지가 표시되면 모든 NuGet 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="36162-208">사용 하 여 hello Azure 포털 tooupload는 [응용 프로그램 패키지](batch-application-packages.md) 에 대 한 **PersistOutputsTask**합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="36162-209">Hello 포함 `PersistOutputsTask.exe` 및 해당 종속 어셈블리도 hello.zip 패키지 집합 hello 응용 프로그램 ID에에서 너무 "PersistOutputsTask" 및 hello 응용 프로그램 패키지 버전 "1.0" 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="36162-210">**시작** (실행된) hello **PersistOutputs** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="36162-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="36162-211">실행 중인 hello 샘플에 대 한 증명된 toochoose hello 지 속성 기술 toouse 입력 하는 경우 **1** hello 파일 규칙 라이브러리 toopersist 작업 출력을 사용 하 여 toorun hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="36162-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36162-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="36162-213">.NET 용 hello 일괄 처리 파일 규칙 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="36162-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="36162-214">.NET 용 hello 일괄 처리 파일 규칙 라이브러리에서 사용할 수는 [NuGet][nuget_package]합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="36162-215">hello 라이브러리 확장 hello [CloudJob] [ net_cloudjob] 및 [CloudTask] [ net_cloudtask] 새 메서드가 포함 된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="36162-216">또한 hello 참조 [참조 설명서](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello 파일 규칙 라이브러리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="36162-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="36162-217">hello [소스 코드] [ github_file_conventions] hello 파일 규칙에 대 한 라이브러리는 Microsoft Azure SDK.NET 저장소에 대 한 hello에서 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36162-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="36162-218">출력 데이터 유지를 위한 다른 방법 탐색</span><span class="sxs-lookup"><span data-stu-id="36162-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="36162-219">참조 [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md) 작업 및 작업 데이터 유지에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="36162-220">참조 [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md) toolearn toouse hello 일괄 처리 서비스 API toopersist 데이터를 출력 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="36162-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "포털의 저장된 출력 파일 및 저장된 로그 선택기"
[2]: ./media/batch-task-output/task-output-02.png "태스크 출력 블레이드 hello Azure 포털에서"
