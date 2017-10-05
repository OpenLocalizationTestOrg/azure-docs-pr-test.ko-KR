---
title: "Azure Batch 서비스 API를 사용하여 Azure Storage에 작업 및 태스크 출력 유지 | Microsoft Docs"
description: "Batch 서비스 API를 사용하여 Azure Storage에 Batch 작업 및 태스크 출력을 유지하는 방법을 알아봅니다."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 2530b7c20347b9fb58aee4dfe693847cf3911741
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-task-data-to-azure-storage-with-the-batch-service-api"></a><span data-ttu-id="db2c9-103">Batch 서비스 API를 사용하여 Azure Storage에 태스크 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="db2c9-103">Persist task data to Azure Storage with the Batch service API</span></span>

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="db2c9-104">2017-05-01 버전 이상에서는 Batch 서비스 API에서 가상 컴퓨터 구성으로 풀에서 실행되는 태스크 및 작업 관리자 태스크의 출력 데이터를 Azure Storage에 유지하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-104">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools with the virtual machine configuration.</span></span> <span data-ttu-id="db2c9-105">태스크를 추가할 때 Azure Storage의 컨테이너를 태스크 출력의 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-105">When you add a task, you can specify a container in Azure Storage as the destination for the task's output.</span></span> <span data-ttu-id="db2c9-106">그런 다음 태스크가 완료되면 Batch 서비스에서 해당 컨테이너에 출력 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-106">The Batch service then writes any output data to that container when the task is complete.</span></span>

<span data-ttu-id="db2c9-107">Batch 서비스 API를 사용하여 태스크 출력을 유지하는 이점은 태스크가 실행되는 응용 프로그램을 수정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-107">An advantage to using the Batch service API to persist task output is that you do not need to modify the application that the task is running.</span></span> <span data-ttu-id="db2c9-108">대신 클라이언트 응용 프로그램을 간단하게 약간만 수정하면 태스크를 만드는 코드 내에서 태스크 출력을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-108">Instead, with a few simple modifications to your client application, you can persist the task's output from within the code that creates the task.</span></span>   

## <a name="when-do-i-use-the-batch-service-api-to-persist-task-output"></a><span data-ttu-id="db2c9-109">Batch 서비스 API를 사용하여 태스크 출력을 유지하는 경우는?</span><span class="sxs-lookup"><span data-stu-id="db2c9-109">When do I use the Batch service API to persist task output?</span></span>

<span data-ttu-id="db2c9-110">Azure Batch는 태스크 출력을 유지하는 한 가지 이상의 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-110">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="db2c9-111">Batch 서비스 API를 사용하는 것은 다음 시나리오에 가장 적합한 편리한 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-111">Using the Batch service API is a convenient approach that's best suited to these scenarios:</span></span>

- <span data-ttu-id="db2c9-112">태스크가 실행되는 응용 프로그램을 수정하지 않고 클라이언트 응용 프로그램 내에서 태스크 출력을 유지하는 코드를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-112">You want to write code to persist task output from within your client application, without modifying the application that your task is running.</span></span>
- <span data-ttu-id="db2c9-113">가상 컴퓨터 구성으로 만든 풀에서 Batch 태스크 및 작업 관리자 태스크의 출력을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-113">You want to persist output from Batch tasks and job manager tasks in pools created with the virtual machine configuration.</span></span>
- <span data-ttu-id="db2c9-114">Azure Storage 컨테이너에 임의의 이름으로 출력을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-114">You want to persist output to an Azure Storage container with an arbitrary name.</span></span>
- <span data-ttu-id="db2c9-115">[Batch 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)(영문)에 따라 명명된 Azure Storage 컨테이너에 출력을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-115">You want to persist output to an Azure Storage container named according to the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> 

<span data-ttu-id="db2c9-116">위에서 나열한 시나리오와 다른 시나리오이면 다른 방법을 고려해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-116">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="db2c9-117">예를 들어 Batch 서비스 API는 현재 태스크가 실행되는 동안 Azure Storage에 대한 스트리밍 출력을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-117">For example, the Batch service API does not currently support streaming output to Azure Storage while the task is running.</span></span> <span data-ttu-id="db2c9-118">출력을 스트리밍하려면 .NET에서 사용할 수 있는 Batch 파일 규칙 라이브러리를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-118">To stream output, consider using the Batch File Conventions library, available for .NET.</span></span> <span data-ttu-id="db2c9-119">다른 언어의 경우 사용자 고유의 자체 솔루션을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-119">For other languages, you'll need to implement your own solution.</span></span> <span data-ttu-id="db2c9-120">태스크 출력을 유지하기 위한 다른 옵션에 대한 자세한 내용은 [Azure Storage에 작업 및 태스크 출력 유지](batch-task-output.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-120">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="create-a-container-in-azure-storage"></a><span data-ttu-id="db2c9-121">Azure Storage에 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="db2c9-121">Create a container in Azure Storage</span></span>

<span data-ttu-id="db2c9-122">Azure Storage에 태스크 출력을 유지하려면 출력 파일의 대상으로 사용할 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-122">To persist task output to Azure Storage, you'll need to create a container that serves as the destination for your output files.</span></span> <span data-ttu-id="db2c9-123">태스크를 실행하기 전에, 오히려 작업을 제출하기 전에 컨테이너를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-123">Create the container before you run your task, preferably before you submit your job.</span></span> <span data-ttu-id="db2c9-124">컨테이너를 만들려면 적절한 Azure Storage 클라이언트 라이브러리 또는 SDK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-124">To create the container, use the appropriate Azure Storage client library or SDK.</span></span> <span data-ttu-id="db2c9-125">Azure Storage API에 대한 자세한 내용은 [Azure Storage 설명서](https://docs.microsoft.com/azure/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-125">For more information about Azure Storage APIs, see the [Azure Storage documentation](https://docs.microsoft.com/azure/storage/).</span></span>

<span data-ttu-id="db2c9-126">예를 들어 C#으로 응용 프로그램을 작성하는 경우 [.NET용 Azure Storage 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-126">For example, if you are writing your application in C#, use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="db2c9-127">다음 예제에서는 컨테이너를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-127">The following example shows how to create a container:</span></span>

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-the-container"></a><span data-ttu-id="db2c9-128">컨테이너에 대한 공유 액세스 서명 가져오기</span><span class="sxs-lookup"><span data-stu-id="db2c9-128">Get a shared access signature for the container</span></span>

<span data-ttu-id="db2c9-129">컨테이너를 만든 후에는 컨테이너에 대한 쓰기 액세스 권한이 있는 SAS(공유 액세스 서명)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-129">After you create the container, get a shared access signature (SAS) with write access to the container.</span></span> <span data-ttu-id="db2c9-130">SAS는 컨테이너에 대해 위임된 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-130">A SAS provides delegated access to the container.</span></span> <span data-ttu-id="db2c9-131">SAS는 지정된 권한 집합 및 지정된 시간 간격으로 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-131">The SAS grants access with a specified set of permissions and over a specified time interval.</span></span> <span data-ttu-id="db2c9-132">Batch 서비스에는 컨테이너에 태스크 출력을 기록하는 쓰기 권한이 있는 SAS가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-132">The Batch service needs a SAS with write permissions to write task output to the container.</span></span> <span data-ttu-id="db2c9-133">SAS에 대한 자세한 내용은 [Azure Storage에서 \(SAS\)(공유 액세스 서명) 사용](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-133">For more information about SAS, see [Using shared access signatures \(SAS\) in Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

<span data-ttu-id="db2c9-134">Azure Storage API를 사용하여 SAS를 가져오면 API에서 SAS 토큰 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-134">When you get a SAS using the Azure Storage APIs, the API returns a SAS token string.</span></span> <span data-ttu-id="db2c9-135">이 토큰 문자열에는 SAS가 유효한 권한과 간격을 포함하여 SAS의 모든 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-135">This token string includes all parameters of the SAS, including the permissions and the interval over which the SAS is valid.</span></span> <span data-ttu-id="db2c9-136">SAS를 사용하여 Azure Storage의 컨테이너에 액세스하려면 SAS 토큰 문자열을 리소스 URI에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-136">To use the SAS to access a container in Azure Storage, you need to append the SAS token string to the resource URI.</span></span> <span data-ttu-id="db2c9-137">리소스 URI는 추가된 SAS 토큰과 함께 Azure Storage에 대해 인증된 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-137">The resource URI, together with the appended SAS token, provides authenticated access to Azure Storage.</span></span>

<span data-ttu-id="db2c9-138">다음 예제에서는 컨테이너에 대한 쓰기 전용 SAS 토큰 문자열을 가져온 다음 컨테이너 URI에 SAS를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-138">The following example shows how to get a write-only SAS token string for the container, then appends the SAS to the container URI:</span></span>

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a><span data-ttu-id="db2c9-139">태스크 출력에 대한 출력 파일 지정</span><span class="sxs-lookup"><span data-stu-id="db2c9-139">Specify output files for task output</span></span>

<span data-ttu-id="db2c9-140">태스크에 대한 출력 파일을 지정하려면 [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) 개체의 컬렉션을 만들고 태스크를 만들 때 [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) 속성에 이 컬렉션을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-140">To specify output files for a task, create a collection of [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objects and assign it to the [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) property when you create the task.</span></span> 

<span data-ttu-id="db2c9-141">다음 .NET 코드 예제에서는 `output.txt`라는 파일에 임의의 숫자를 쓰는 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-141">The following .NET code example creates a task that writes random numbers to a file named `output.txt`.</span></span> <span data-ttu-id="db2c9-142">이 예제에서는 `output.txt`라는 출력 파일을 만들어 컨테이너에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-142">The example creates an output file for `output.txt` to be written to the container.</span></span> <span data-ttu-id="db2c9-143">또한 `std*.txt` 파일 패턴(_, 예:_ , `stdout.txt` 및 `stderr.txt`)과 일치하는 모든 로그 파일에 대한 출력 파일도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-143">The example also creates output files for any log files that match the file pattern `std*.txt` (_e.g._, `stdout.txt` and `stderr.txt`).</span></span> <span data-ttu-id="db2c9-144">컨테이너 URL에는 이전에 컨테이너에 대해 만든 SAS가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-144">The container URL requires the SAS that was created previously for the container.</span></span> <span data-ttu-id="db2c9-145">Batch 서비스에서는 이 SAS를 사용하여 컨테이너에 대한 액세스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-145">The Batch service uses the SAS to authenticate access to the container:</span></span> 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a><span data-ttu-id="db2c9-146">일치시킬 파일 패턴 지정</span><span class="sxs-lookup"><span data-stu-id="db2c9-146">Specify a file pattern for matching</span></span>

<span data-ttu-id="db2c9-147">출력 파일을 지정할 때 [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) 속성을 사용하여 일치시킬 파일 패턴을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-147">When you specify an output file, you can use the [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) property to specify a file pattern for matching.</span></span> <span data-ttu-id="db2c9-148">파일 패턴은 0개 파일, 단일 파일 또는 태스크에서 만든 파일 집합과 일치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-148">The file pattern may match zero files, a single file, or a set of files that are created by the task.</span></span>

<span data-ttu-id="db2c9-149">**FilePattern** 속성은 `*`(비재귀 일치의 경우) 및 `**`(재귀 일치의 경우)와 같은 표준 파일 시스템 와일드카드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-149">The **FilePattern** property supports standard filesystem wildcards such as `*` (for non-recursive matches) and `**` (for recursive matches).</span></span> <span data-ttu-id="db2c9-150">예를 들어 위의 코드 샘플에서는 `std*.txt`와 비일치하는 파일 패턴을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-150">For example, the code sample above specifies the file pattern to match `std*.txt` non-recursively:</span></span> 

`filePattern: @"..\std*.txt"`

<span data-ttu-id="db2c9-151">단일 파일을 업로드하려면 와일드카드 없이 파일 패턴을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-151">To upload a single file, specify a file pattern with no wildcards.</span></span> <span data-ttu-id="db2c9-152">예를 들어 위의 코드 샘플에서는 `output.txt`와 비재귀적으로 일치하는 파일 패턴을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-152">For example, the code sample above specifies the file pattern to match `output.txt`:</span></span>

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a><span data-ttu-id="db2c9-153">업로드 조건 지정</span><span class="sxs-lookup"><span data-stu-id="db2c9-153">Specify an upload condition</span></span>

<span data-ttu-id="db2c9-154">[OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) 속성은 출력 파일의 조건부 업로드를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-154">The [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) property permits conditional uploading of output files.</span></span> <span data-ttu-id="db2c9-155">일반적인 시나리오는 태스크가 성공하면 한 파일 집합을 업로드하고, 실패하면 다른 파일 집합을 업로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-155">A common scenario is to upload one set of files if the task succeeds, and a different set of files if it fails.</span></span> <span data-ttu-id="db2c9-156">예를 들어 태스크가 실패하고 0이 아닌 종료 코드로 종료되는 경우에만 자세한 로그 파일을 업로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-156">For example, you may want to upload verbose log files only when the task fails and exits with a nonzero exit code.</span></span> <span data-ttu-id="db2c9-157">마찬가지로 태스크가 실패하는 경우 파일이 없거나 불완전할 수 있으므로, 태스크가 성공한 경우에만 결과 파일을 업로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-157">Similarly, you may want to upload result files only if the task succeeds, as those files may be missing or incomplete if the task fails.</span></span>

<span data-ttu-id="db2c9-158">위의 코드 샘플에서는 **UploadCondition** 속성을 **TaskCompletion**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-158">The code sample above sets the **UploadCondition** property to **TaskCompletion**.</span></span> <span data-ttu-id="db2c9-159">이 설정은 종료 코드의 값에 관계 없이 태스크가 완료된 후에 파일을 업로드하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-159">This setting specifies that the file is to be uploaded after the tasks completes, regardless of the value of the exit code.</span></span> 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

<span data-ttu-id="db2c9-160">다른 설정은 [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) 열거형을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-160">For other settings, see the [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.</span></span>

### <a name="disambiguate-files-with-the-same-name"></a><span data-ttu-id="db2c9-161">이름이 같은 파일의 구분</span><span class="sxs-lookup"><span data-stu-id="db2c9-161">Disambiguate files with the same name</span></span>

<span data-ttu-id="db2c9-162">작업의 태스크에서 이름이 같은 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-162">The tasks in a job may produce files that have the same name.</span></span> <span data-ttu-id="db2c9-163">예를 들어 `stdout.txt` 및 `stderr.txt`는 작업에서 실행되는 모든 태스크에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-163">For example, `stdout.txt` and `stderr.txt` are created for every task that runs in a job.</span></span> <span data-ttu-id="db2c9-164">태스크마다 자체의 컨텍스트에서 실행되므로 이러한 파일은 노드의 파일 시스템에서 충돌하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-164">Because each task runs in its own context, these files don't conflict on the node's file system.</span></span> <span data-ttu-id="db2c9-165">그러나 여러 태스크의 파일을 공유 컨테이너에 업로드할 때는 이름이 같은 파일을 명확하게 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-165">However, when you upload files from multiple tasks to a shared container, you'll need to disambiguate files with the same name.</span></span>

<span data-ttu-id="db2c9-166">[OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) 속성은 출력 파일에 대한 대상 Blob 또는 가상 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-166">The [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) property specifies the destination blob or virtual directory for output files.</span></span> <span data-ttu-id="db2c9-167">**Path** 속성을 사용하여 이름이 같은 출력 파일이 Azure Storage에서 고유한 이름으로 지정되는 방식으로 Blob 또는 가상 디렉터리의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-167">You can use the **Path** property to name the blob or virtual directory in such a way that output files with the same name are uniquely named in Azure Storage.</span></span> <span data-ttu-id="db2c9-168">고유한 이름을 지정하고 파일을 쉽게 식별할 수 있도록 경로에 태스크 ID를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-168">Using the task ID in the path is a good way to ensure unique names and easily identify files.</span></span>

<span data-ttu-id="db2c9-169">**FilePattern** 속성이 와일드카드 식으로 설정되면 해당 패턴과 일치하는 모든 파일이 **Path** 속성으로 지정된 가상 디렉터리에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-169">If the **FilePattern** property is set to a wildcard expression, then all files that match the pattern are uploaded to the virtual directory specified by the **Path** property.</span></span> <span data-ttu-id="db2c9-170">예를 들어 컨테이너가 `mycontainer`이고 태스크 ID가 `mytask`이고 파일 패턴이 `..\std*.txt`인 경우, Azure Storage의 출력 파일에 대한 절대 URI는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-170">For example, if the container is `mycontainer`, the task ID is `mytask`, and the file pattern is `..\std*.txt`, then the absolute URIs to the output files in Azure Storage will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

<span data-ttu-id="db2c9-171">**FilePattern** 속성이 단일 파일 이름과 일치하도록 설정되면(와일드카드 문자가 포함되지 않음) **Path** 속성의 값은 정규화된 Blob 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-171">If the **FilePattern** property is set to match a single file name, meaning it does not contain any wildcard characters, then the value of the **Path** property specifies the fully qualified blob name.</span></span> <span data-ttu-id="db2c9-172">여러 태스크에서 단일 파일과 이름이 충돌할 것으로 예상되는 경우 가상 디렉터리의 이름을 파일 이름의 일부로 포함하여 해당 파일을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-172">If you anticipate naming conflicts with a single file from multiple tasks, then include the name of the virtual directory as part of the file name to disambiguate those files.</span></span> <span data-ttu-id="db2c9-173">예를 들어 태스크 ID, 구분 기호 문자(일반적으로 슬래시) 및 파일 이름을 포함하도록 **Path** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-173">For example, set the **Path** property to include the task ID, the delimiter character (typically a forward slash), and the file name:</span></span>

`path: taskId + @"/output.txt"`

<span data-ttu-id="db2c9-174">태스크 집합의 출력 파일에 대한 절대 URI는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-174">The absolute URIs to the output files for a set of tasks will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

<span data-ttu-id="db2c9-175">Azure Storage의 가상 디렉터리에 대한 자세한 내용은 [컨테이너의 Blob 나열](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container)에 있는 Blob 나열을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-175">For more information about virtual directories in Azure Storage, see [List the blobs in a container](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).</span></span>


## <a name="diagnose-file-upload-errors"></a><span data-ttu-id="db2c9-176">파일 업로드 오류 진단</span><span class="sxs-lookup"><span data-stu-id="db2c9-176">Diagnose file upload errors</span></span>

<span data-ttu-id="db2c9-177">Azure Storage에 대한 출력 파일 업로드가 실패하면 태스크가 **완료됨** 상태로 전환되고 [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) 속성이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-177">If uploading output files to Azure Storage fails, then the task moves to the **Completed** state and the [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) property is set.</span></span> <span data-ttu-id="db2c9-178">**FailureInformation** 속성을 검사하여 발생한 오류를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-178">Examine the **FailureInformation** property to determine what error occurred.</span></span> <span data-ttu-id="db2c9-179">예를 들어 컨테이너가 없는 경우 파일 업로드에서 발생하는 오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-179">For example, here is an error that occurs on file upload if the container cannot be found:</span></span> 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of the specified Azure container(s) was not found while attempting to upload an output file
```

<span data-ttu-id="db2c9-180">모든 파일 업로드에서 Batch는 두 개의 로그 파일을 `fileuploadout.txt` 및 `fileuploaderr.txt` 계산 노드에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-180">On every file upload, Batch writes two log files to the compute node, `fileuploadout.txt` and `fileuploaderr.txt`.</span></span> <span data-ttu-id="db2c9-181">이러한 로그 파일을 검사하여 특정 오류에 대해 자세히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-181">You can examine these log files to learn more about a specific failure.</span></span> <span data-ttu-id="db2c9-182">예를 들어 태스크 자체가 실행되지 않아 파일 업로드를 시도할 수 없는 경우에는 이러한 로그 파일이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-182">In cases where the file upload was never attempted, for example because the task itself couldn’t run, then these log files will not exist.</span></span>

## <a name="diagnose-file-upload-performance"></a><span data-ttu-id="db2c9-183">파일 업로드 성능 진단</span><span class="sxs-lookup"><span data-stu-id="db2c9-183">Diagnose file upload performance</span></span>

<span data-ttu-id="db2c9-184">`fileuploadout.txt` 파일은 업로드 진행률을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-184">The `fileuploadout.txt` file logs upload progress.</span></span> <span data-ttu-id="db2c9-185">이 파일을 검사하면 파일 업로드에 소요된 시간에 대해 자세히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-185">You can examine this file to learn more about how long your file uploads are taking.</span></span> <span data-ttu-id="db2c9-186">노드 크기, 업로드 시 노드의 다른 활동, 대상 컨테이너가 Batch 풀과 동일한 지역에 있는지 여부, 저장소 계정에 동시에 업로드되는 노드 수 등 업로드 성능에 영향을 주는 많은 요인들이 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-186">Keep in mind that there are many contributing factors to upload performance, including the size of the node, other activity on the node at the time of the upload, whether the target container is in the same region as the Batch pool, how many nodes are uploading to the storage account at the same time, and so on.</span></span>

## <a name="use-the-batch-service-api-with-the-batch-file-conventions-standard"></a><span data-ttu-id="db2c9-187">Batch 파일 규칙 표준과 함께 Batch 서비스 API 사용</span><span class="sxs-lookup"><span data-stu-id="db2c9-187">Use the Batch service API with the Batch File Conventions standard</span></span>

<span data-ttu-id="db2c9-188">Batch 서비스 API를 사용하여 태스크 출력을 유지할 때 원하는 대로 대상 컨테이너 및 Blob의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-188">When you persist task output with the Batch service API, you can name your destination container and blobs however you like.</span></span> <span data-ttu-id="db2c9-189">또한 [Batch 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)(영문)에 따라 이름을 지정하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-189">You can also choose to name them according to the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="db2c9-190">파일 규칙 표준에서는 지정된 출력 파일에 대한 Azure Storage 대상 컨테이너 및 Blob의 이름을 작업 및 태스크의 이름을 기반으로 하여 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-190">The File Conventions standard determines the names of the destination container and blob in Azure Storage for a given output file based on the names of the job and task.</span></span> <span data-ttu-id="db2c9-191">파일 규칙 표준을 사용하여 출력 파일 이름을 지정하면 [Azure Portal](https://portal.azure.com)에서 출력 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-191">If you do use the File Conventions standard for naming output files, then your output files are available for viewing in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="db2c9-192">C#에서 개발하는 경우 [.NET용 Batch 파일 규칙 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files)(영문)에 기본 제공된 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-192">If you are developing in C#, you can use the methods built into the [Batch File Conventions library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files).</span></span> <span data-ttu-id="db2c9-193">이 라이브러리는 적절하게 명명된 컨테이너와 Blob 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-193">This library creates the properly named containers and blob paths for you.</span></span> <span data-ttu-id="db2c9-194">예를 들어 API를 호출하여 작업 이름에 기반한 올바른 컨테이너 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-194">For example, you can call the API to get the correct name for the container, based on the job name:</span></span>

```csharp
string containerName = job.OutputStorageContainerName();
```

<span data-ttu-id="db2c9-195">[CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) 메서드를 사용하여 컨테이너에 쓰는 데 사용되는 SAS(공유 액세스 서명) URL을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-195">You can use the [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) method to return a shared access signature (SAS) URL that is used to write to the container.</span></span> <span data-ttu-id="db2c9-196">그런 다음 이 SAS를 [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) 생성자에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-196">You can then pass this SAS to the [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructor.</span></span>

<span data-ttu-id="db2c9-197">C# 이외의 언어로 개발하는 경우 파일 규칙 표준을 직접 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-197">If you are developing in a language other than C#, you will need to implement the File Conventions standard yourself.</span></span>

## <a name="code-sample"></a><span data-ttu-id="db2c9-198">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="db2c9-198">Code sample</span></span>

<span data-ttu-id="db2c9-199">[PersistOutputs][github_persistoutputs] 샘플 프로젝트는 GitHub의 [Azure 배치 코드 샘플][github_samples] 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-199">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="db2c9-200">이 Visual Studio 솔루션에서는 .NET용 Batch 클라이언트 라이브러리를 사용하여 영구 저장소에 태스크 출력을 유지하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-200">This Visual Studio solution demonstrates how to use the Batch client library for .NET to persist task output to durable storage.</span></span> <span data-ttu-id="db2c9-201">샘플을 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-201">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="db2c9-202">**Visual Studio 2015 이상**에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-202">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="db2c9-203">Microsoft.Azure.Batch.Samples.Common 프로젝트에서 배치 및 저장소 **계정 자격 증명**을 **AccountSettings.settings**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-203">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="db2c9-204">**빌드** 합니다(하지만 실행하지 않음).</span><span class="sxs-lookup"><span data-stu-id="db2c9-204">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="db2c9-205">메시지가 표시되면 모든 NuGet 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-205">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="db2c9-206">Azure 포털을 사용하여 [PersistOutputsTask](batch-application-packages.md) 에 대한 **응용 프로그램 패키지**를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-206">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="db2c9-207">`PersistOutputsTask.exe` 및 종속 어셈블리를 .zip 패키지에 포함하고, 응용 프로그램 ID를 "PersistOutputsTask"로, 응용 프로그램 패키지 버전을 "1.0"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-207">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="db2c9-208">**PersistOutputs** 프로젝트를 **시작**(실행)합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-208">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="db2c9-209">샘플을 실행하는 데 사용할 지속성 기술을 선택하라는 메시지가 표시될 때 Batch 서비스 API를 통해 샘플을 실행하여 태스크 출력을 유지하려면 **2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-209">When prompted to choose the persistence technology to use for running the sample, enter **2** to run the sample using the Batch service API to persist task output.</span></span>
7. <span data-ttu-id="db2c9-210">원하는 경우 샘플을 다시 실행하고 **3**을 입력하여 Batch 서비스 API를 통해 출력을 유지하고 파일 규칙 표준에 따라 대상 컨테이너와 Blob 경로의 이름도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2c9-210">If desired, run the sample again, entering **3** to persist output with the Batch service API, and also to name the destination container and blob path according to the File Conventions standard.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db2c9-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db2c9-211">Next steps</span></span>

- <span data-ttu-id="db2c9-212">.NET용 파일 규칙 라이브러리를 사용하여 태스크 출력을 유지하는 방법에 대한 자세한 내용은 [.NET용 Batch 파일 규칙 라이브러리를 사용하여 Azure Storage에 작업 및 태스크 데이터 유지](batch-task-output-file-conventions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-212">For more information on persisting task output with the File Conventions library for .NET, see [Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist ](batch-task-output-file-conventions.md).</span></span>
- <span data-ttu-id="db2c9-213">Azure Batch에서 출력 데이터를 유지하는 다른 방법에 대한 자세한 내용은 [Azure Storage에 작업 및 태스크 출력 유지](batch-task-output.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db2c9-213">For information on other approaches for persisting output data in Azure Batch, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span>

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
