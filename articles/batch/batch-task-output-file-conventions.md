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
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>작업을 유지 하 고.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 함께 데이터 tooAzure 저장소 작업 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

한 가지 방법은 toopersist 작업 데이터는 toouse hello [.NET 용 Azure 배치 파일 규칙 라이브러리][nuget_package]합니다. hello 파일 규칙 라이브러리 프로세스가 간소화 되어 hello 작업 출력을 저장할 경우의 데이터 tooAzure 저장소 및 검색 하기. Hello 파일 규칙 라이브러리 태스크와 클라이언트 모두 코드에서 사용할 수 있습니다 &mdash; 유지 파일에 대 한 작업 코드 및 클라이언트 toolist 코드을 검색 합니다. 작업 코드에서 사용할 수도 업스트림 작업 라이브러리 tooretrieve hello 출력 hello와 같은 한 [종속성 작업](batch-task-dependencies.md) 시나리오입니다. 

tooretrieve 출력 hello 파일 규칙 라이브러리를 사용 하 여 파일, 작업 또는 작업에 대 한 hello 파일 ID와 목적으로 나열 하 여 찾을 수 있습니다. Tooknow hello 이름 또는 hello 파일의 위치가 필요는 없습니다. 예를 들어 지정된 된 태스크에 대 한 hello 파일 규칙 라이브러리 toolist 모든 중간 파일을 사용 하거나 지정된 된 작업에 대 한 미리 보기 파일을 가져올 수 있습니다.

> [!TIP]
> 2017-05-01 버전 부터는 hello 일괄 처리 서비스 API 작업 및 가상 컴퓨터 구성 hello 사용 하 여 만든 풀에서 실행 되는 작업 관리자 작업에 대 한 유지 출력 데이터 tooAzure 저장소를 지원 합니다. hello 일괄 처리 서비스 API 작업을 만들고 역할을 대체 toohello 파일 규칙 라이브러리는 hello 코드 내에서 출력 하는 간단한 방법을 toopersist를 제공 합니다. 작업을 실행 하는 tooupdate hello 응용 프로그램 필요 없이 일괄 처리 클라이언트 응용 프로그램 toopersist 출력을 수정할 수 있습니다. 자세한 내용은 참조 [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md)합니다.
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Hello 파일 규칙 라이브러리 toopersist 작업 출력을 사용 하는 경우

Azure 일괄 처리는 한 가지 방법은 더 toopersist 작업 출력을 제공합니다. hello 파일 규칙은 가장 적합 한 toothese 시나리오입니다.

- 작업 hello 파일 규칙 라이브러리를 사용 하 여 toopersist 파일 실행 되 고 있는지 hello 응용 프로그램에 대 한 hello 코드를 쉽게 수정할 수 있습니다.
- 원하는 toostream 데이터 tooAzure 저장소 hello 작업 실행 중입니다.
- Toopersist 데이터 hello 클라우드 서비스 구성 또는 hello 가상 컴퓨터 구성 중 하나를 사용 하 여 만든 풀에서 사용 하는 것이 좋습니다.
- 클라이언트 응용 프로그램 또는 hello의 다른 작업이 요구 toolocate 작업 하 고 ID 또는 용도 따라 작업 출력 파일을 다운로드 합니다. 
- Tooview 작업 출력을 hello Azure 포털에서에서 사용 하는 것이 좋습니다.

시나리오와 다른 경우 위에 나열 된 다른 접근 방법이 tooconsider를 할 수 있습니다. 지속 작업 출력에 대 한 다른 옵션에 대 한 자세한 내용은 참조 하십시오. [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md)합니다. 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Hello 표준 일괄 처리 파일 규칙 이란?

hello [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) hello 대상 컨테이너와 blob 경로 toowhich 출력 파일이 작성 되는 이름 지정 체계를 제공 합니다. 파일 지속형된 tooAzure toohello 표준 파일 규칙을 준수 하는 저장소 자동으로 hello Azure 포털에서에서 볼 수 있습니다. hello 포털 hello 명명 규칙을 인식 하며 따라서 tooit 준수 하는 파일을 표시할 수 있습니다.

.NET 용 hello 파일 규칙 라이브러리 이름을 저장소 컨테이너 및 태스크 출력 파일 toohello 표준 파일 규칙에 따라 자동으로 지정 합니다. 또한 hello 파일 규칙 라이브러리 toojob ID, 작업 ID 또는 용도 따라 메서드 tooquery 출력 파일이 Azure 저장소에 제공 합니다.   

.NET 이외의 다른 언어로 개발 하는 경우 직접 구현할 수 있습니다 hello 파일 규칙 표준 응용 프로그램에 있습니다. 자세한 내용은 참조 [hello 일괄 처리 파일 규칙 표준에 대 한](batch-task-output.md#about-the-batch-file-conventions-standard)합니다.

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Azure 저장소 계정 tooyour 일괄 처리 계정 연결

출력 데이터 tooAzure toopersist hello 파일 규칙 라이브러리를 사용 하 여 저장소를 먼저 연결 해야 Azure 저장소 계정 tooyour 일괄 처리 계정. 아직 수행 하지 않은 경우 일괄 처리 계정에는 저장소 계정 tooyour hello를 사용 하 여 연결 [Azure 포털](https://portal.azure.com):

1. Hello Azure 포털에서에서 tooyour 일괄 처리 계정을 이동 합니다. 
2. **설정**에서 **저장소 계정**을 선택합니다.
3. 배치 계정과 연결된 저장소 계정이 아직 없으면 **저장소 계정(없음)**을 클릭합니다.
4. 구독에 대 한 hello 목록에서 저장소 계정을 선택 합니다. 최상의 성능을 위해 hello에 해당 하는 Azure 저장소 계정을 사용 하 여 작업이 실행 되 고 있는 일괄 처리 계정 hello와 동일한 영역입니다.

## <a name="persist-output-data"></a>출력 데이터 유지

toopersist job 및 task hello 파일 규칙 라이브러리를 사용 하 여 데이터를 출력를 Azure 저장소의 컨테이너를 만든 다음 hello 출력 toohello 컨테이너를 저장 합니다. 사용 하 여 hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) 작업 코드 tooupload hello 작업 출력 toohello 컨테이너의 합니다. 

Azure Storage의 컨테이너와 Blob 사용에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.

> [!WARNING]
> 작업 및 작업에 대 한 모든 출력 라이브러리에 저장 된 hello 파일 규칙을 통해 지속 hello 동일한 컨테이너입니다. 많은 수의 작업을 시도 하는 경우 toopersist 파일에 hello 동일한 시간 [조절 제한 저장소](../storage/common/storage-performance-checklist.md#blobs) 적용 될 수 있습니다.
> 
> 

### <a name="create-storage-container"></a>저장소 컨테이너 만들기

toopersist 작업 출력 tooAzure 저장소를 먼저 호출 하 여 컨테이너를 만들 [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]합니다. 이 확장 메서드는 [CloudStorageAccount][net_cloudstorageaccount] 개체를 매개 변수로 사용합니다. 명명 된 따라 toohello 파일 규칙 콘텐츠를 검색할 수 있도록 표준 hello hello 문서의 뒷부분에 설명 된 Azure 포털 및 hello 검색 메서드는 컨테이너를 만듭니다.

일반적으로 클라이언트 응용 프로그램의 hello 코드 toocreate 컨테이너에 넣으면 &mdash; hello 풀, 작업 및 작업을 만드는 응용 프로그램입니다.

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

### <a name="store-task-outputs"></a>태스크 출력 저장

작업 출력 toohello 컨테이너 hello를 사용 하 여 저장할 수는 Azure 저장소의 컨테이너를 준비 했으므로, 이제 [TaskOutputStorage] [ net_taskoutputstorage] hello 파일 규칙 라이브러리에 클래스를 찾을 수 있습니다.

작업 코드에서 먼저 만듭니다는 [TaskOutputStorage] [ net_taskoutputstorage] 개체를 다음 hello 작업의 작업 완료 되 면 호출 hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] 메서드 toosave 해당 출력 tooAzure 저장소입니다.

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

hello `kind` hello의 매개 변수 [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) 메서드 분류 hello 파일을 유지 합니다. 미리 정의된 4개의 [TaskOutputKind][net_taskoutputkind] 형식, 즉 `TaskOutput`, `TaskPreview`, `TaskLog` 및 `TaskIntermediate.`가 있습니다. 사용자 정의 범주의 출력도 정의할 수 있습니다.

이러한 출력 형식을 사용 하면 toospecify 어떤 유형의 출력 toolist 나중 hello에 대 한 일괄 처리를 쿼리할 때 지정된 된 태스크의 출력을 유지 합니다. 즉, 작업에 대 한 hello 출력 나열 하는 경우 hello 출력 형식 중 하나에 hello 목록을 필터링 할 수 있습니다. 예를 들어 "hello를 되돌리지 *미리 보기* 작업에 대 한 출력 *109*." 에 표시를 나열 하 고 출력을 검색에 대 한 자세한 [출력을 검색](#retrieve-output) hello 문서의 뒷부분에 나오는 합니다.

> [!TIP]
> hello 출력 종류 결정 hello Azure 포털 특정 파일 나타나는 한 위치: *TaskOutput*-분류 된 파일이 아래에 나타납니다 **작업 출력 파일**, 및 *TaskLog*파일이 아래에 나타납니다 **로그 작업**합니다.
> 
> 

### <a name="store-job-outputs"></a>작업 출력 저장

또한 toostoring 태스크 출력에 연결 된 전체 작업 hello 출력 저장할 수 있습니다. 예를 들어 영화 렌더링 작업의 hello 병합 작업에서는 작업 출력으로 완벽 하 게 렌더링 하는 hello 영화를 유지할 수 있습니다. 작업이 완료 된 클라이언트 응용 프로그램 나열 하 고 hello 출력 hello 작업에 대 한 검색할 수 및 않습니다 하지 필요 tooquery hello 개별 작업입니다.

Hello를 호출 하 여 작업 출력을 저장할 [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] 메서드를 hello 지정 [JobOutputKind] [ net_joboutputkind] 및 파일 이름:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Hello와 마찬가지로 **TaskOutputKind** 형식 hello를 사용 하면 작업 출력에 대 한 [JobOutputKind] [ net_joboutputkind] 형식 toocategorize 작업의 파일을 유지 합니다. 이 매개 변수는 특정 유형의 출력 (목록)에 대 한 쿼리를 toolater 있습니다. hello **JobOutputKind** 유형의 출력과 미리 보기 범주를 포함 하 고 사용자 지정 범주 만들기를 지원 합니다.

### <a name="store-task-logs"></a>태스크 로그 저장

또한 toopersisting 파일 toodurable 저장소 작업 또는 작업 하는 경우 완료 되 면 toopersist 파일 작업의 hello 실행 중에 업데이트를 할 수 있습니다 &mdash; 로그 파일 또는 `stdout.txt` 및 `stderr.txt`, 예를 들어 있습니다. 이 작업을 위해 hello Azure 일괄 처리 파일 규칙 라이브러리는 hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] 메서드. 와 [SaveTrackedAsync][net_savetrackedasync], (사용자가 지정한 간격) 마다 hello 노드에서 업데이트 tooa 파일을 추적 하 고 해당 업데이트 tooAzure 저장소를 유지 합니다.

다음 코드 조각 hello를 사용 하 여 [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` hello hello 작업을 실행 하는 동안은 15 초 마다 Azure 저장소에서:

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

섹션을 주석 처리 된 hello `Code tooprocess data and produce output file(s)` 작업은 일반적으로 수행 하는 hello 코드에 대 한 자리 표시자입니다. 예를 들어 Azure Storage에서 데이터를 다운로드하고 변환 또는 계산을 수행하는 코드가 있을 수 있습니다. 어떻게 이러한 코드에 래핑할 수 있습니다이 조각의 hello 중요 한 부분을 입증 하 고는 `using` 와 파일을 업데이트 하는 블록 tooperiodically [SaveTrackedAsync][net_savetrackedasync]합니다.

hello 노드 에이전트는 hello 풀의 각 노드에서 실행 되 고 hello 노드와 hello 일괄 처리 서비스 간의 hello 명령 컨트롤 인터페이스를 제공 하는 프로그램입니다. hello `Task.Delay` 콜이이 hello 끝에 필요한 `using` 노드 에이전트 hello 블록 tooensure 내용이 시간 tooflush hello 표준의 hello 노드에서 toohello stdout.txt 파일입니다. 이러한 지연 시간 없이 것은 가능한 toomiss hello 출력의 마지막 몇 초입니다. 이 지연 시간은 일부 파일에만 필요할 수 있습니다.

> [!NOTE]
> 사용 하는 추적 파일을 사용 하면 **SaveTrackedAsync**만 *추가* toohello 추적 된 파일 지속형된 tooAzure 저장 됩니다. 이 메서드를 사용 하 여 추적 회전 아닌 로그 파일에 대해서만 또는 toowith 작성 된 기타 파일 추가 작업 toohello hello 파일 끝입니다.
> 
> 

## <a name="retrieve-output-data"></a>출력 데이터 검색

Hello Azure 일괄 처리 파일 규칙 라이브러리를 사용 하 여 지속형된 출력을 검색 하는 경우 이렇게 하면 작업 및 작업 중심 방식에서입니다. Hello에 대 한 출력 작업 또는 작업 지정한 tooknow 필요 없이 해당 파일 이름 또는 Azure 저장소에 해당 경로 요청할 수 있습니다. 대신 태스크별 또는 작업 ID별로 출력 파일을 요청할 수 있습니다.

hello 다음 코드 조각 반복 작업의 작업, hello 작업에 대 한 hello 출력 파일에 대 한 일부 정보 출력을 다음 저장소에서 해당 파일을 다운로드 합니다.

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

## <a name="view-output-files-in-hello-azure-portal"></a>Hello Azure 포털에서에서 출력 파일 보기

hello Azure 포털 작업 출력 파일 표시 하 고 로그는 지속형된 tooa hello를 사용 하 여 Azure 저장소 계정을 연결 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다. Hello, 선택한 언어에에서 직접이 규칙을 구현할 수 있습니다 또는.NET 응용 프로그램에서 hello 파일 규칙 라이브러리를 사용할 수 있습니다.

hello 포털에 출력 파일의 tooenable hello 디스플레이 hello 요구 사항을 준수를 충족 해야 합니다.

1. [Azure 저장소 계정 연결](#requirement-linked-storage-account) tooyour 일괄 처리 계정.
2. 출력을 유지할 때 toohello 미리 정의 된 저장 컨테이너 및 파일에 대 한 명명 규칙을 준수 합니다. Hello 파일 규칙 라이브러리에서 이러한 규칙의 hello 정의 찾을 수 있습니다 [README][github_file_conventions_readme]합니다. Hello를 사용 하는 경우 [Azure 일괄 처리 파일 규칙] [ nuget_package] 라이브러리 toopersist 프로그램 출력을 파일 toohello 표준 파일 규칙에 따라 유지 됩니다.

toohello 작업에 관심이 있는 출력을 가진 클릭 한 다음 탐색, tooview 작업 출력 파일 및 hello Azure 포털 로그인 **Saved 출력 파일** 또는 **저장 된 로그**합니다. 이 이미지는 hello **Saved 출력 파일** ID "007" hello, 작업에 대 한:

![태스크 출력 블레이드 hello Azure 포털에서][2]

## <a name="code-sample"></a>코드 샘플

hello [PersistOutputs] [ github_persistoutputs] 샘플 프로젝트를 사용 하면 hello 중 하나인 [Azure 배치 코드 샘플] [ github_samples] GitHub에서 합니다. 이 Visual Studio 솔루션 toouse hello Azure 일괄 처리 파일 규칙 라이브러리 toopersist 작업 toodurable 저장소를 출력 하는 방법을 보여 줍니다. toorun hello 예제를 다음이 단계를 수행 합니다.

1. 프로젝트 열기 hello **Visual Studio 2015 이상**합니다.
2. 일괄 처리 및 저장소 추가 **계정 자격 증명** 너무**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 프로젝트에 있습니다.
3. **빌드** (하지만 실행 하지 않는) hello 솔루션입니다. 메시지가 표시되면 모든 NuGet 패키지를 복원합니다.
4. 사용 하 여 hello Azure 포털 tooupload는 [응용 프로그램 패키지](batch-application-packages.md) 에 대 한 **PersistOutputsTask**합니다. Hello 포함 `PersistOutputsTask.exe` 및 해당 종속 어셈블리도 hello.zip 패키지 집합 hello 응용 프로그램 ID에에서 너무 "PersistOutputsTask" 및 hello 응용 프로그램 패키지 버전 "1.0" 너무 합니다.
5. **시작** (실행된) hello **PersistOutputs** 프로젝트.
6. 실행 중인 hello 샘플에 대 한 증명된 toochoose hello 지 속성 기술 toouse 입력 하는 경우 **1** hello 파일 규칙 라이브러리 toopersist 작업 출력을 사용 하 여 toorun hello 예제입니다. 

## <a name="next-steps"></a>다음 단계

### <a name="get-hello-batch-file-conventions-library-for-net"></a>.NET 용 hello 일괄 처리 파일 규칙 라이브러리 가져오기

.NET 용 hello 일괄 처리 파일 규칙 라이브러리에서 사용할 수는 [NuGet][nuget_package]합니다. hello 라이브러리 확장 hello [CloudJob] [ net_cloudjob] 및 [CloudTask] [ net_cloudtask] 새 메서드가 포함 된 클래스입니다. 또한 hello 참조 [참조 설명서](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello 파일 규칙 라이브러리에 대 한 합니다.

hello [소스 코드] [ github_file_conventions] hello 파일 규칙에 대 한 라이브러리는 Microsoft Azure SDK.NET 저장소에 대 한 hello에서 GitHub에서 사용할 수 있습니다. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>출력 데이터 유지를 위한 다른 방법 탐색

- 참조 [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md) 작업 및 작업 데이터 유지에 대 한 개요입니다.
- 참조 [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md) toolearn toouse hello 일괄 처리 서비스 API toopersist 데이터를 출력 하는 방법입니다.

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
