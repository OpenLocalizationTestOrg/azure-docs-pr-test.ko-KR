---
title: "aaaPersist 작업 및 태스크 출력 hello Azure 배치 서비스 API가 있는 저장소 tooAzure | Microsoft Docs"
description: "일괄 처리 서비스 API toouse toopersist 일괄 처리 작업 및 작업 출력 tooAzure 저장소 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Hello 일괄 처리 서비스 API로 작업 tooAzure 데이터 저장소를 유지 합니다.

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

2017-05-01 버전 부터는 hello 일괄 처리 서비스 API 작업 및 hello 가상 컴퓨터 구성으로 풀에서 실행 되는 작업 관리자 작업에 대 한 유지 출력 데이터 tooAzure 저장소를 지원 합니다. 작업을 추가 하는 경우에 hello 작업의 출력에 대 한 hello 대상으로 Azure 저장소의 컨테이너를 지정할 수 있습니다. 그런 다음 hello 일괄 처리 서비스 hello 작업이 완료 될 때 모든 출력 데이터 toothat 컨테이너를 씁니다.

장점은 toousing hello 서비스 API toopersist 작업 출력은 작업 hello toomodify hello 응용 프로그램 필요 하지 않으면 일괄 처리 실행 중입니다. 대신, 몇 가지 간단한 수정 tooyour 클라이언트 응용 프로그램과 hello 작업을 만드는 hello 코드 내에서 hello 작업의 출력을 유지할 수 있습니다.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>일괄 처리 서비스 API hello toopersist 작업 출력을 사용 하는 경우

Azure 일괄 처리는 한 가지 방법은 더 toopersist 작업 출력을 제공합니다. Hello 일괄 처리 서비스 API를 사용 하 여 가장 적합 한 toothese 시나리오 되는 편리한 방법이입니다.

- 원하는 toowrite 코드 toopersist 작업 출력에서 클라이언트 응용 프로그램 내에서 작업을 실행 하는 hello 응용 프로그램을 수정 하지 않고 있습니다.
- Toopersist 출력을 일괄 처리 작업 및 가상 컴퓨터 구성 hello 사용 하 여 만든 풀에서 작업 관리자 작업을 사용 하는 것이 좋습니다.
- 원하는 임의의 이름을 사용 하 여 toopersist tooan Azure 저장소 컨테이너를 출력 합니다.
- 원하는 toopersist 출력 tooan Azure 저장소 컨테이너에 따라 toohello 라는 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다. 

시나리오와 다른 경우 위에 나열 된 다른 접근 방법이 tooconsider를 할 수 있습니다. 예를 들어 hello 일괄 처리 서비스 API는 현재 지원 하지 스트리밍 출력 tooAzure 저장소 hello 작업이 실행 되는 동안. toostream 출력 hello 일괄 처리 파일 규칙 라이브러리를.NET에 사용할 수 있는 사용 하는 것이 좋습니다. 다른 언어에 대 한 tooimplement를 고유한 솔루션이 필요 합니다. 지속 작업 출력에 대 한 다른 옵션에 대 한 자세한 내용은 참조 하십시오. [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md)합니다. 

## <a name="create-a-container-in-azure-storage"></a>Azure Storage에 컨테이너 만들기

toopersist 작업 출력 tooAzure 저장소, 출력 파일에 대 한 hello 대상으로 사용 되는 컨테이너 toocreate 필요 합니다. 실행 하기 전에 작업을 권장 작업을 제출 하기 전에 hello 컨테이너를 만듭니다. toocreate hello 컨테이너, 사용 하 여 hello 적합 한 Azure 저장소 클라이언트 라이브러리 또는 SDK를 선택 합니다. Azure 저장소 Api에 대 한 자세한 내용은 참조 hello [Azure 저장소 설명서](https://docs.microsoft.com/azure/storage/)합니다.

예를 들어 C#에서 응용 프로그램을 작성 하는 경우 사용 hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다. hello 방법을 예제와 다음 toocreate 컨테이너:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Hello 컨테이너에 대 한 공유 액세스 서명을 가져오기

Hello 컨테이너를 만든 후에 쓰기 권한을 toohello 컨테이너와 공유 액세스 서명을 (SAS)를 가져옵니다. SAS를 위임 된 액세스 toohello 컨테이너를 제공 합니다. hello SAS 사용 권한 및 지정한 시간 간격에 대해 지정된 된 집합을 사용 하 여 액세스 권한을 부여합니다. hello 일괄 처리 서비스 쓰기 권한 toowrite 작업 출력 toohello 컨테이너와 SAS 필요합니다. SAS에 대한 자세한 내용은 [Azure Storage에서 \(SAS\)(공유 액세스 서명) 사용](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

Hello Azure 저장소 Api를 사용 하 여 SAS를 얻으면 hello API SAS 토큰 문자열을 반환 합니다. 이 토큰 문자열 hello hello 사용 권한 및 hello는 hello SAS 유효한 간격을 포함 하 여 SAS의 모든 매개 변수를 포함 합니다. toouse hello SAS tooaccess Azure 저장소의 컨테이너 tooappend hello SAS 토큰 문자열 toohello 리소스 URI 필요합니다. hello와 함께 hello 리소스 URI, SAS 토큰을 추가, 인증 된 액세스 tooAzure 저장소를 제공 합니다.

hello 다음 예제에서는 tooget 쓰기 전용 SAS 토큰 hello 컨테이너에 대 한 문자열 하는 방법을 보여 줍니다. 다음 hello SAS toohello 컨테이너 URI를 추가 합니다.

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>태스크 출력에 대한 출력 파일 지정

태스크에 대 한 toospecify 출력 파일의 컬렉션을 만들 [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) 개체 및 toohello 할당 [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) hello 작업을 만들 때 속성입니다. 

hello 다음.NET 코드 예제에서는 작업을 만듭니다 라는 난수 tooa 파일 `output.txt`합니다. hello 예제에 대 한 출력 파일을 만듭니다 `output.txt` toobe toohello 컨테이너를 기록 합니다. hello 예제는 또한 hello 파일 패턴과 일치 하는 모든 로그 파일에 대 한 출력 파일을 만들며 `std*.txt` (_예:_, `stdout.txt` 및 `stderr.txt`). hello 컨테이너 URL 생성 된 SAS hello hello 컨테이너에 대 한 이전에 필요 합니다. hello 일괄 처리 서비스는 hello SAS tooauthenticate 액세스 toohello 컨테이너를 사용합니다. 

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

### <a name="specify-a-file-pattern-for-matching"></a>일치시킬 파일 패턴 지정

출력 파일을 지정 하면 hello를 사용할 수 있습니다 [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) 속성 toospecify 파일 패턴 일치에 대 한 합니다. 0 개 파일, 단일 파일 또는 hello 작업에 의해 만들어진 파일 집합이 hello 파일 패턴 일치 될 수 있습니다.

hello **FilePattern** 속성은 표준 파일 시스템 와일드 카드와 같은 지원 `*` (에 대 한 비재귀적와 같음) 및 `**` (에 대 한 재귀와 같음). 예를 들어 위의 코드 샘플 hello 지정 hello 파일 패턴 toomatch `std*.txt` 비재귀적: 

`filePattern: @"..\std*.txt"`

단일 파일을 tooupload 와일드 카드와 파일 패턴을 지정 합니다. 예를 들어 위의 코드 샘플 hello 지정 hello 파일 패턴 toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>업로드 조건 지정

hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) 속성에서 출력 파일의 조건부 업로드를 허용 합니다. 실패할 경우 일반적인 시나리오는 tooupload 하나의 집합만 hello 작업에 성공 하면 파일 및 다른 파일 집합입니다. 예를 들어 hello 작업 실패 하 고 0이 아닌 종료 코드로 종료 될 경우에 tooupload 자세한 로그 파일을 사용할 수 있습니다. 마찬가지로, 할 수 있습니다 tooupload 결과 파일 hello 작업이 성공 하는 경우에 이러한 파일이 누락 되었거나 불완전 hello 작업이 실패할 경우 수 있습니다.

hello 위의 코드 샘플 설정 hello **UploadCondition** 속성 너무**TaskCompletion**합니다. 이 설정은 hello이 파일은 toobe hello 종료 코드의 hello 값에 관계 없이 hello 작업에서 완료 된 후 업로드를 지정 합니다. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

기타 설정에 대 한 참조 hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) 열거형입니다.

### <a name="disambiguate-files-with-hello-same-name"></a>Hello 사용 하 여 파일 명확 하 게 같은 이름

작업의 hello 작업 hello 있는 파일을 생성할 수 있습니다 동일한 이름입니다. 예를 들어 `stdout.txt` 및 `stderr.txt`는 작업에서 실행되는 모든 태스크에 대해 만들어집니다. 자체 컨텍스트에서 각 태스크를 실행 하기 때문에 이러한 파일 hello 노드의 파일 시스템에 충돌 하지 않습니다. 그러나 여러 작업 tooa 공유 컨테이너에서 파일을 업로드 하는 경우 해야 hello 사용 하 여 toodisambiguate 파일 이름이 같은 합니다.

hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) hello 대상 blob 또는 출력 파일에 대 한 가상 디렉터리 속성을 지정 합니다. Hello를 사용할 수 있습니다 **경로** 속성 tooname hello blob 또는 출력 파일 이름이 같은 Azure 저장소의 이름이 고유한 지 hello로 하는 방식으로 가상 디렉터리입니다. Hello 작업 ID를 사용 하 여 hello 경로에 좋은 방법 tooensure 고유 이름 이며 쉽게 파일을 식별 합니다.

경우 hello **FilePattern** tooa 와일드 카드 식 속성은 다음 hello 패턴과 일치 하는 모든 파일은 hello로 지정 된 업로드 toohello 가상 디렉터리 **경로** 속성입니다. 예를 들어 hello 컨테이너 인지 `mycontainer`, hello 작업 ID가 `mytask`, hello 파일 패턴은 및 `..\std*.txt`, 다음 Uri toohello 출력 파일이 Azure 저장소는 것과 비슷하지만 절대 hello:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

경우 hello **FilePattern** 속성은 집합 toomatch 단일 파일 이름, 값의 hello hello 다음 모든 와일드 카드 문자가 포함 되지 않은 데이터를 의미가 **경로** 속성 hello 정규화 된 blob 이름 지정 . 이름 여러 작업을 단일 파일 충돌을 예상 하는 경우 다음 hello 가상 디렉터리의 hello 이름 hello 파일 이름 toodisambiguate의 일환으로 이러한 파일을 포함할 합니다. 예를 들어 집합 hello **경로** 속성 tooinclude hello 작업 ID, hello 구분 기호 문자 (일반적으로 슬래시), 및 hello 파일 이름:

`path: taskId + @"/output.txt"`

hello 절대 Uri toohello 출력 파일에서 작업 집합을 유사한 됩니다.

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Azure 저장소에 가상 디렉터리에 대 한 자세한 내용은 참조 [컨테이너에서 hello blob 나열](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container)합니다.


## <a name="diagnose-file-upload-errors"></a>파일 업로드 오류 진단

TooAzure 저장소 실패 파일 출력 업로드 경우 hello toohello 이동 **Completed** 상태 및 hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) 속성을 설정 합니다. Hello 검사 **FailureInformation** 속성 toodetermine 어떤 오류가 발생 했습니다. 예를 들어 다음은 hello 컨테이너를 찾을 수 없는 경우 파일 업로드 시 발생 하는 오류가입니다. 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

일괄 처리에서 모든 파일 업로드 파일 toohello 계산 노드를 두 개의 로그를 쓰기 `fileuploadout.txt` 및 `fileuploaderr.txt`합니다. 특정 오류에 대 한 자세한 로그 파일 toolearn 이러한를 검사할 수 있습니다. 된 hello 파일 업로드 되지 하려고, 예를 들어 hello 작업 자체 수 없습니다. 실행의 경우 다음 이러한 로그 파일이 존재 하지 않습니다.

## <a name="diagnose-file-upload-performance"></a>파일 업로드 성능 진단

hello `fileuploadout.txt` 파일 업로드 진행률을 기록 합니다. 파일 업로드 하는 기간에 대 한 자세한 내용이이 파일 toolearn을 검사할 수 있습니다. 개가 많은 영향을 주는 요인 hello 대상 컨테이너에서 hello 인지 hello 업로드의 hello 시 hello 노드에서 다른 작업이 hello 노드의 hello 크기를 포함 하 여 tooupload 성능을 염두에 둬야 배치 풀을 hello와 동일한 지역 노드 수는 hello 시간, 및 등 동일한 저장소 계정을 진단 toohello를 업로드 합니다.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Hello 일괄 처리 서비스 API를 사용 하 여 일괄 처리 파일 규칙 표준 hello로

하지만 Hello 일괄 처리 서비스 API 사용 하 여 작업 출력을 유지 하는 경우 대상 컨테이너 이름을 지정할 수 및 원하는 blob입니다. Tooname 선택할 수도 있습니다 toohello에 따라 이러한 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다. hello 파일 규칙 표준 hello 대상 컨테이너 및 hello hello 작업 및 작업 이름을 사용 하 여 지정 된 출력 파일에 대 한 Azure 저장소에 blob의 hello 이름을 결정 합니다. Hello 표준 파일 규칙을 사용 하 여 출력 파일 이름 지정에 대 한 않는 경우 출력 파일이 있는 hello에 표시할 수 있는 [Azure 포털](https://portal.azure.com)합니다.

C#에서 개발 하는 경우에 hello에 기본 제공 하는 hello 방법을 사용할 수 있습니다 [.NET에 대 한 일괄 처리 파일 규칙 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files)합니다. 이 라이브러리는 제대로 컨테이너 및 blob 경로 수에 대 한 명명 된 hello를 만듭니다. 예를 들어 hello API tooget hello hello 작업 이름을 기반으로 하는 hello 컨테이너에 대 한 올바른 이름을 호출할 수 있습니다.

```csharp
string containerName = job.OutputStorageContainerName();
```

Hello를 사용할 수 있습니다 [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) 메서드 tooreturn 사용 되는 toowrite toohello 컨테이너 공유 액세스 서명 (SAS) URL입니다. 이 SAS toohello에 전달할 수 있습니다 [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) 생성자입니다.

C# 이외의 언어에서 개발 하는 경우에 사용자가 직접 tooimplement hello 파일 규칙 표준을 해야 합니다.

## <a name="code-sample"></a>코드 샘플

hello [PersistOutputs] [ github_persistoutputs] 샘플 프로젝트를 사용 하면 hello 중 하나인 [Azure 배치 코드 샘플] [ github_samples] GitHub에서 합니다. 이 Visual Studio 솔루션 toouse.NET toopersist 작업에 대 한 일괄 처리 클라이언트 라이브러리 hello toodurable 저장소를 출력 하는 방법을 보여 줍니다. toorun hello 예제를 다음이 단계를 수행 합니다.

1. 프로젝트 열기 hello **Visual Studio 2015 이상**합니다.
2. 일괄 처리 및 저장소 추가 **계정 자격 증명** 너무**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 프로젝트에 있습니다.
3. **빌드** (하지만 실행 하지 않는) hello 솔루션입니다. 메시지가 표시되면 모든 NuGet 패키지를 복원합니다.
4. 사용 하 여 hello Azure 포털 tooupload는 [응용 프로그램 패키지](batch-application-packages.md) 에 대 한 **PersistOutputsTask**합니다. Hello 포함 `PersistOutputsTask.exe` 및 해당 종속 어셈블리도 hello.zip 패키지 집합 hello 응용 프로그램 ID에에서 너무 "PersistOutputsTask" 및 hello 응용 프로그램 패키지 버전 "1.0" 너무 합니다.
5. **시작** (실행된) hello **PersistOutputs** 프로젝트.
6. 실행 중인 hello 샘플에 대 한 증명된 toochoose hello 지 속성 기술 toouse 입력 하는 경우 **2** hello 일괄 처리 서비스 API toopersist 작업 출력을 사용 하 여 toorun hello 예제입니다.
7. 원하는 경우 hello 샘플을 다시 실행 입력 **3** hello 일괄 처리 서비스 API 및 tooname hello 컨테이너 및 blob 경로 toohello 표준 파일 규칙에 따라 toopersist 출력 합니다.

## <a name="next-steps"></a>다음 단계

- .NET 용 hello 파일 규칙 라이브러리와 함께 지속 작업 출력에 자세한 내용은 참조 [작업 및 작업 데이터 tooAzure 저장소.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 유지 ](batch-task-output-file-conventions.md)합니다.
- Azure 일괄 처리의 출력 데이터 유지를 위한 다른 방법에 대 한 자세한 내용은 참조 하십시오. [지속 작업을 작업 출력 tooAzure 저장소](batch-task-output.md)합니다.

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
