---
title: ".NET 용 hello Azure 배치 클라이언트 라이브러리 사용-aaaTutorial | Microsoft Docs"
description: "Hello Azure 일괄 처리의 기본 개념을 알아봅니다 하 고 간단한.NET을 사용 하 여 솔루션을 빌드하십시오."
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>.NET 용 hello 배치 클라이언트 라이브러리를 사용 하 여 솔루션을 구축

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

hello 기본 사항 알아보기 [Azure 배치] [ azure_batch] 및 hello [일괄 처리.NET] [ net_api] 이 문서에는 라이브러리는 C# 샘플 응용 프로그램의 단계별을 다룬 것 처럼 단계입니다. 의견에 귀 hello 샘플 응용 프로그램 hello 일괄 처리 서비스 tooprocess를 활용 하는 방법에 병렬 작업 hello 클라우드 및 어떻게 상호 작용 [Azure 저장소](../storage/common/storage-introduction.md) 파일 준비 및 검색 합니다. 일반적인 일괄 처리 응용 프로그램 워크플로 자세한 및 hello의 주요 구성 요소 일괄 처리 풀, 작업, 작업 등의 기본으로 이해 하 고 계산 노드 합니다.

![Batch 솔루션 워크플로(기본)][11]<br/>

## <a name="prerequisites"></a>필수 조건
이 문서에는 사용자에게 C# 및 Visual Studio에 대한 실용적인 지식이 있다고 가정합니다. 또한 Azure hello 일괄 처리 및 저장소 서비스에 대해 아래 지정 된 수 toosatisfy hello 계정 만들기 요구 하 가정 합니다.

### <a name="accounts"></a>계정
* **Azure 계정**: Azure 구독이 아직 없는 경우 [무료 Azure 계정][azure_free_account]을 만듭니다.
* **Batch 계정**: Azure 구독이 있으면 [Azure Batch 계정을 만듭니다](batch-account-create-portal.md).
* **Storage 계정**: [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)의 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 섹션을 참조하세요.

> [!IMPORTANT]
> 에서는 현재 일괄 처리 *만* hello **범용** 5 단계에 설명 된 대로 저장소 계정 유형을 [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md#create-a-storage-account) 에 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.
>
>

### <a name="visual-studio"></a>Visual Studio
있어야 **Visual Studio 2015 이상** toobuild hello 샘플 프로젝트입니다. Hello에서 무료 또는 평가판 버전의 Visual Studio를 찾을 수 있습니다 [Visual Studio 제품 개요][visual_studio]합니다.

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial* 코드 샘플
hello [DotNetTutorial] [ github_dotnettutorial] 샘플을 사용 하면 많은 일괄 처리 코드 예제는 hello에서 발견 하는 hello 중 하나인 [azure 일괄 처리-샘플] [ github_samples] 의 리포지토리 GitHub 합니다. 클릭 하 여 모든 hello 샘플을 다운로드할 수 있습니다 **클론 또는 다운로드 > zip 파일 다운로드** hello 리포지토리 홈 페이지에서 또는 hello를 클릭 하 여 [azure 일괄 처리-샘플 master.zip] [ github_samples_zip]직접 다운로드 링크입니다. Hello 내용의 hello ZIP 파일을 추출 하면 hello 솔루션 hello 다음 폴더에서에서 찾을 수 있습니다.

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch 탐색기(선택 사항)
hello [Azure 일괄 처리 탐색기] [ github_batchexplorer] 는 hello에 포함 된 무료 유틸리티 [azure 일괄 처리-샘플] [ github_samples] GitHub의 리포지토리 합니다. 필요 없음 toocomplete 하는 동안이 자습서에서는 유용할 수 있습니다 개발 및 일괄 처리 솔루션을 디버깅 합니다.

## <a name="dotnettutorial-sample-project-overview"></a>DotNetTutorial 샘플 프로젝트 개요
hello *DotNetTutorial* 코드 샘플은 두 프로젝트로 구성 되어 있는 Visual Studio 솔루션은: **DotNetTutorial** 및 **TaskApplication**합니다.

* **DotNetTutorial** 은 계산 노드 (가상 컴퓨터)에 병렬 작업 일괄 처리 및 저장소 서비스 tooexecute hello와 상호 작용 하는 hello 클라이언트 응용 프로그램입니다. DotNetTutorial은 로컬 워크스테이션에서 실행합니다.
* **TaskApplication** Azure tooperform hello 실제 작업의 계산 노드에서 실행 되는 hello 프로그램. Hello 샘플에서 `TaskApplication.exe` 구문 분석 하 여 hello Azure 저장소 (hello 입력된 파일)에서 다운로드 한 파일의 텍스트입니다. 텍스트 파일을 생성 한 다음 (hello 출력 파일) hello 상위 3 개의에 있는 단어 hello 입력된 파일의 목록이 들어 있습니다. Hello 출력 파일을 만든 후 TaskApplication hello 파일 tooAzure 저장소에 업로드 합니다. 따라서이 다운로드에 대 한 클라이언트 응용 프로그램을 사용할 수 있는 toohello 있습니다. TaskApplication은 hello 일괄 처리 서비스의에서 여러 계산 노드에서 동시에 실행 됩니다.

hello 다음 다이어그램에서는 hello 클라이언트 응용 프로그램에 의해 수행 된 기본 작업이 hello *DotNetTutorial*, hello 작업에서 실행 되는 hello 응용 프로그램 및 *TaskApplication*. 이러한 기본 워크플로는 Batch를 사용하여 만드는 많은 계산 솔루션의 일반적인 형태입니다. Hello 일괄 처리 서비스에서에서 사용할 수 있는 모든 기능을 보여 주지 동안 거의 모든 일괄 처리 시나리오가 워크플로의 일부를 포함 합니다.

![Batch 예제 워크플로][8]<br/>

[**1단계.**](#step-1-create-storage-containers) Azure Blob Storage에 **컨테이너**를 만듭니다.<br/>
[**2단계.**](#step-2-upload-task-application-and-data-files) 업로드 작업 응용 프로그램 파일 및 입력된 파일 toocontainers 합니다.<br/>
[**3단계.**](#step-3-create-batch-pool) Batch **풀**을 만듭니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** 풀 hello **StartTask** 다운로드 hello 풀을 참가 작업 이진 파일 (TaskApplication) toonodes hello 합니다.<br/>
[**4단계.**](#step-4-create-batch-job) Batch **작업**을 만듭니다.<br/>
[**5단계.**](#step-5-add-tasks-to-job) 추가 **작업** toohello 작업 합니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** hello 작업은 예약 된 tooexecute 노드에 있습니다.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** 각 태스크는 Azure Storage에서 입력 데이터를 다운로드한 다음 실행을 시작합니다.<br/>
[**6단계.**](#step-6-monitor-tasks) 태스크를 모니터링합니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** 작업을 완료 하는 대로 해당 출력 데이터 tooAzure 저장소 업로드 합니다.<br/>
[**7단계.**](#step-7-download-task-output) Storage에서 태스크 출력을 다운로드합니다.

언급 했 듯이 모든 일괄 처리 솔루션 두 정확한 단계를 수행 하 고 될 수 있습니다 더 많은 포함 하지만 hello *DotNetTutorial* 샘플 응용 프로그램 일괄 처리 솔루션에는 일반적인 프로세스를 보여 줍니다.

## <a name="build-hello-dotnettutorial-sample-project"></a>Hello 빌드 *DotNetTutorial* 샘플 프로젝트
Hello에 모두 일괄 처리 및 저장소 계정 자격 증명을 지정 해야 성공적으로 hello 샘플을 실행할 수 있습니다, 전에 *DotNetTutorial* 프로젝트의 `Program.cs` 파일입니다. 아직 그렇게를 수행 하지 않은 경우 hello에서에서 솔루션을 열고 Visual Studio hello를 두 번 클릭 하 여 `DotNetTutorial.sln` 솔루션 파일입니다. Hello를 사용 하 여 Visual Studio 내에서 열에서 또는 **파일 > 열기 > 프로젝트/솔루션** 메뉴.

열기 `Program.cs` hello 내 *DotNetTutorial* 프로젝트. Hello 파일의 hello 맨 위 근처에 지정 된 자격 증명을 추가 합니다.

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Hello 자격 증명을 지정 하 고 현재 해야 위에서 설명 했 듯이 **범용** Azure 저장소의 저장소 계정입니다. Hello 내에서 blob 저장소를 사용 하는 일괄 처리 응용 프로그램 **범용** 저장소 계정입니다. Hello를 선택 하 여 생성 된 저장소 계정에 대 한 hello 자격 증명을 지정 하지 않으면 *Blob 저장소* 계정 유형입니다.
>
>

Hello에 일괄 처리 및 저장소 계정 자격 증명의 각 서비스 계정 블레이드 hello 내에서 찾을 수 있습니다 [Azure 포털][azure_portal]:

![Hello 포털에서 자격 증명을 일괄 처리][9]
![hello 포털에서 저장소 자격 증명][10]<br/>

솔루션 탐색기에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭을 자격 증명을 사용 하 여 hello 프로젝트를 업데이트 하 한 했으므로 **솔루션 빌드**합니다. 로그인할지 묻는 hello 복원 된 NuGet 패키지를 확인 합니다.

> [!TIP]
> Hello NuGet 패키지를 자동으로 복원 되지 않습니다, 또는 실패 toorestore hello 패키지에 대 한 오류가 표시 되 면 hello 가졌는지 확인 [NuGet 패키지 관리자] [ nuget_packagemgr] 설치 합니다. 누락 된 패키지의 hello 다운로드를 사용 합니다. 참조 [사용 하면 패키지를 복원 하는 동안 빌드] [ nuget_restore] tooenable 패키지 다운로드 합니다.
>
>

다음 섹션 hello,에서는 hello 샘플 응용 프로그램으로 구분 tooprocess를 수행 하는 hello 단계 hello 일괄 처리 서비스에서에서 작업 하 고 해당 단계를 자세히 설명 합니다. 좋습니다 toorefer toohello Visual Studio에서 열린 솔루션을 hello 샘플의 코드의 모든 줄에 설명 되어 있으므로이 문서의 hello 나머지 부분에서 작업 하는 동안.

Hello toohello 위쪽 탐색 `MainAsync` hello에 대 한 메서드 *DotNetTutorial* 프로젝트의 `Program.cs` 단계 1 toostart 파일입니다. 아래 단계 각각 다음과 같이 hello 진행 메서드의 호출 하는 약 `MainAsync`합니다.

## <a name="step-1-create-storage-containers"></a>1단계: Storage 컨테이너 만들기
![Azure Storage에 컨테이너 만들기][1]
<br/>

Batch에는 Azure Storage와의 상호 작용을 위해 기본 제공되는 지원이 포함됩니다. 저장소 계정의 컨테이너에는 일괄 처리 계정에서 실행 되는 hello 작업에서 필요한 hello 파일 제공 합니다. 또한 hello 컨테이너 hello 작업을 생성 하는 곳 toostore hello 출력 데이터를 제공 합니다. hello 먼저 hello *DotNetTutorial* 클라이언트 응용 프로그램에는에 세 개의 컨테이너를 만드는 방법 [Azure Blob 저장소](../storage/common/storage-introduction.md):

* **응용 프로그램**:이 컨테이너는 hello 작업으로 Dll과 같은 종속성 중 하나에서 실행 하는 hello 응용 프로그램을 저장 합니다.
* **입력**: 작업은 hello에서 데이터 파일 tooprocess hello를 다운로드 *입력* 컨테이너입니다.
* **출력**: hello 결과 toohello 업로드는 입력된 파일 처리를 완료 하는 작업 *출력* 컨테이너입니다.

저장소와 순서 toointeract에서 계정 및 컨테이너를 만들 hello 사용 하 여 [.NET 용 Azure 저장소 클라이언트 라이브러리][net_api_storage]합니다. 와 참조 toohello 계정 만듭니다 [CloudStorageAccount][net_cloudstorageaccount], 만들고 있는에서 [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

사용 하 여 hello `blobClient` hello 응용 프로그램 전체에서 참조 하 고 tooseveral 메서드 매개 변수로 전달 합니다. 이 예는 hello 코드 블록 바로 뒤에 오는 hello 위의 호출에서는 `CreateContainerIfNotExistAsync` tooactually hello 컨테이너를 만듭니다.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

Hello 컨테이너를 만든 후에 이제 hello 응용 프로그램 hello 작업에 의해 사용 될 hello 파일을 업로드 수 있습니다.

> [!TIP]
> [어떻게 toouse.NET에서 Blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md) Azure 저장소 컨테이너 및 blob 작업의 개요를 제공 합니다. 일괄 처리 작업을 시작할 때 hello 위쪽 읽기 목록에 있는 이어야 합니다.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>2단계: 작업 응용 프로그램 및 데이터 파일 업로드
![업로드 작업 응용 프로그램에 대 한 입력 (데이터) toocontainers 파일][2]
<br/>

Hello 파일에서 작업을 업로드 *DotNetTutorial* 먼저의 컬렉션을 정의 **응용 프로그램** 및 **입력** hello 로컬 컴퓨터에 있는 대로 파일 경로입니다. 그런 다음 이러한 파일 toohello 컨테이너 hello 이전 단계에서 만든를 업로드 합니다.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

두 가지가 `Program.cs` hello 업로드 프로세스에 관련 된입니다.

* `UploadFilesToContainerAsync`:이 메서드는 컬렉션을 반환 [ResourceFile] [ net_resourcefile] (아래 설명 참조) 개체를 내부적으로 호출 `UploadFileToContainerAsync` hello에 전달 된 각 파일을 즉 tooupload *filePaths* 매개 변수입니다.
* `UploadFileToContainerAsync`:이 실제로 hello 파일 업로드를 수행 하 고 hello 만듭니다는 hello 방법과 [ResourceFile] [ net_resourcefile] 개체입니다. Hello 파일을 업로드 한 후 hello 파일에 대 한 공유 액세스 서명 (SAS)를 얻어서를 점을 나타내는 ResourceFile 개체를 반환 합니다. 공유 액세스 서명도 아래에 설명되어 있습니다.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ net_resourcefile] 해당 태스크를 실행 하기 전에 hello URL tooa 파일 다운로드 한 tooa은 Azure 저장소에 있는 일괄 처리의 작업 계산 노드를 제공 합니다. hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] Azure 저장소에 있는 속성 hello hello 파일의 전체 URL을 지정 합니다. hello URL toohello 파일 보안 액세스를 제공 하는 공유 액세스 서명 (SAS)을 포함할 수도 있습니다. Batch .NET 내에서 대부분의 작업 형식은 다음을 포함하는 *ResourceFiles* 속성을 포함합니다.

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

hello DotNetTutorial 샘플 응용 프로그램에서는 hello JobPreparationTask 또는 JobReleaseTask 작업 종류를 사용 하지 않지만 자세히 알아볼 수 있습니다에 대 한 [Azure 일괄 처리에서 실행 작업 준비 및 완료 작업 하는 계산 노드](batch-job-prep-release.md)합니다.

### <a name="shared-access-signature-sas"></a>공유 액세스 서명(SAS)
공유 액세스 서명이 있는 문자열-URL의 일부분으로 포함 하는 경우-보안 액세스 toocontainers 및 Azure 저장소에서 blob를 제공 합니다. 두 blob을 사용 하 여 hello DotNetTutorial 응용 프로그램 및 컨테이너 공유 액세스 서명 Url 및 이러한 공유 tooobtain 서명 문자열 hello 저장소 서비스에서에서 액세스 하는 방법을 보여 줍니다.

* **공유 액세스 서명은 blob**: DotNetTutorial에 hello 풀 StartTask hello 응용 프로그램 이진 파일 및 입력된 데이터 파일 저장소에서 다운로드할 때 blob 공유 액세스 서명을 사용 하 여 (아래 #3 단계 참조). hello `UploadFileToContainerAsync` DotNetTutorial의 메서드에서 `Program.cs` hello 코드가 포함 된 각 blob의 공유 액세스 서명을 가져옵니다. [CloudBlob.GetSharedAccessSignature][net_sas_blob]를 호출하여 작업을 수행합니다.
* **컨테이너 공유 액세스 서명을**: 각 작업 hello 계산 노드에서 작업을 마치면 대로 해당 출력 파일 toohello 업로드 *출력* Azure 저장소의 컨테이너입니다. toodo TaskApplication hello 파일을 업로드 하는 경우 hello 경로의 일부로 toohello 컨테이너 쓰기 액세스를 제공 하는 컨테이너 공유 액세스 서명을 사용 하 여, 합니다. 가져오는 hello 컨테이너 공유 액세스 서명은 때 가져오는 hello blob 공유 액세스 서명으로 유사한 방식으로 수행 됩니다. DotNetTutorial, 해당 hello 확인할 `GetContainerSasUrl` 도우미 메서드를 호출 [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo 하도록 합니다. 읽게 TaskApplication hello 컨테이너를 사용 하는 방법에 대 한 자세한 공유 액세스 서명에서 "6 단계: 작업 모니터링 합니다."

> [!TIP]
> 공유 액세스 서명에 대 hello 두 부분으로 구성 시리즈 체크아웃 [1 부: 이해 hello 공유 액세스 서명 (SAS) 모델](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 및 [2 부: 만들기 및 공유 액세스 서명 (SAS)를 사용 하 여 Blob 저장소](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), 저장소 계정에 대 한 보안 액세스 toodata 제공 하는 방법에 대 한 자세한 toolearn 합니다.
>
>

## <a name="step-3-create-batch-pool"></a>3단계: Batch 풀 만들기
![Batch 풀 만들기][3]
<br/>

Batch **풀**은 Batch가 작업의 태스크를 실행하는 계산 노드(가상 컴퓨터)의 컬렉션입니다.

Hello 응용 프로그램 및 데이터 파일 toohello Azure 저장소 Api와 저장소 계정에 업로드 한 후 *DotNetTutorial* hello 일괄 처리.NET 라이브러리에서 제공 하는 api 호출 toohello 일괄 처리 서비스를 만들기 시작 합니다. hello 코드 먼저 만듭니다는 [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

다음으로 hello 샘플에서에서 풀을 만듭니다 계산 노드 호출 하 여 hello 일괄 처리 계정을 너무`CreatePoolIfNotExistsAsync`합니다. `CreatePoolIfNotExistsAsync`사용 하 여 hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] 메서드 toocreate hello 일괄 처리 서비스에서에서 새 풀:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

풀을 만들 때 [CreatePool][net_pool_create], 여러 매개 변수 지정 hello 계산 노드 수와 같이 hello [hello 노드의 크기가](../cloud-services/cloud-services-sizes-specs.md)를 작동 하는 노드 hello 및 시스템입니다. *DotNetTutorial*를 사용 하 여 [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 r 2에서 [클라우드 서비스](../cloud-services/cloud-services-guestos-update-matrix.md)합니다. 

Hello를 지정 하 여 계산 노드를 Azure 가상 컴퓨터 (Vm)의 풀을 만들 수도 있습니다 [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] 풀에 있습니다. Windows 또는 [Linux 이미지](batch-linux-nodes.md)에서 VM 계산 노드의 풀을 만들 수 있습니다. VM 이미지에 대 한 hello 소스는 다음 중 하나일 수 있습니다.

- hello [Azure 가상 컴퓨터 마켓플레이스][vm_marketplace], 즉시 사용 되는 Windows 및 Linux 이미지를 제공 하는 합니다. 
- 사용자가 준비하고 제공하는 사용자 지정 이미지입니다. 사용자 지정 이미지에 대한 자세한 내용은 [Batch를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#pool)을 참조하세요.

> [!IMPORTANT]
> Batch의 계산 리소스에 대한 요금이 부과됩니다. toominimize 비용을 낮출 수는 있습니다 `targetDedicatedComputeNodes` too1 hello 샘플을 실행 하기 전에.
>
>

이러한 물리적 노드 속성과 함께 지정할 수도 있습니다는 [StartTask] [ net_pool_starttask] hello 풀에 대 한 합니다. StartTask hello 해당 노드의 hello 풀에 참가 하 고 노드를 다시 시작 될 때마다 각 노드에서 실행 됩니다. StartTask hello 작업의 계산 노드 이전 toohello 실행 응용 프로그램을 설치 하는 데 특히 유용 합니다. 예를 들어 Python 스크립트를 사용 하 여 데이터를 처리 하는 작업을 하는 경우 StartTask tooinstall Python hello 계산 노드에서 사용할 수 있습니다.

이 샘플 응용 프로그램에서는 hello StartTask 저장소에서 다운로드 하는 hello 파일에 복사 (hello를 사용 하 여 지정 되는 [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] 속성) hello StartTask 작업 디렉터리 toohello 공유 디렉터리에서는 *모든* hello 노드에서 실행 되는 작업에 액세스할 수 있습니다. 기본적으로,이 복사 `TaskApplication.exe` 및 해당 종속성 toohello 공유 디렉터리에 각 노드에 hello 노드 hello 풀에 참가 하는 대로 hello 노드에서 실행 되는 모든 작업에 액세스할 수 있도록 합니다.

> [!TIP]
> hello **응용 프로그램 패키지** Azure 일괄 처리의 기능은 다른 방식으로 tooget hello 계산 노드는 풀의 응용 프로그램을 제공 합니다. 참조 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md) 대 한 자세한 내용은 합니다.
>
>

또한 위의 코드 조각 hello에에서 주목할 만한은 hello를 사용 하 여 hello에 두 환경 변수의 *CommandLine* hello StartTask의 속성: `%AZ_BATCH_TASK_WORKING_DIR%` 및 `%AZ_BATCH_NODE_SHARED_DIR%`합니다. 일괄 처리 풀 내에서 각 계산 노드가 특정 tooBatch 있는 여러 환경 변수가 자동으로 구성 됩니다. 작업에 의해 실행 되는 모든 프로세스는 액세스 toothese 환경 변수가 있습니다.

> [!TIP]
> 일괄 처리 풀 및 작업 작업 디렉터리에 대 한 정보에 대 한 계산 노드에서 사용할 수 있는 hello 환경 변수에 대 한 자세한 내용을 toofind 참조 hello [작업에 대 한 환경 설정을](batch-api-basics.md#environment-settings-for-tasks) 및 [파일 및 디렉터리 ](batch-api-basics.md#files-and-directories) hello의 섹션에서는 [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md)합니다.
>
>

## <a name="step-4-create-batch-job"></a>4단계: Batch 작업 만들기
![Batch 작업 만들기][4]<br/>

Batch **작업**은 태스크의 컬렉션이며 계산 노드의 풀과 관련됩니다. 작업의 hello 작업 관련 hello 풀 계산 노드에서 실행 됩니다.

구성 하 고 관련된 작업에서 작업을 추적 뿐만 아니라 hello 일괄 처리에 있는 관계 tooother 작업에서 작업 우선 순위 뿐만 아니라-hello 최대 runtime hello 작업에 대 한 (및 확장 하면 해당 작업)와 같은 특정 제약 조건을 부과 하는 것에 대 한 작업을 사용할 수 있습니다. 계정입니다. 그러나이 예제에서는 hello 작업 3 단계에서 생성 된 hello 풀 연관 되어 있습니다. 추가적으로 구성되는 다른 속성은 없습니다.

모든 Batch 작업은 특정 풀에 연결됩니다. 이 연결은 hello 작업의 작업에서 실행 될 노드를 표시 합니다. Hello를 사용 하 여이 지정할 [CloudJob.PoolInformation] [ net_job_poolinfo] hello 아래 코드 조각에 나와 있는 것 처럼 속성입니다.

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

작업을 만든 후, tooperform hello 작업 작업에 추가 됩니다.

## <a name="step-5-add-tasks-toojob"></a>5 단계: 추가 작업 toojob
![작업 toojob 추가][5]<br/>
*(1) 작업 toohello 작업 추가 되 고 (2) hello 작업은 노드에서 예약 된 toorun (3) hello 작업 hello 데이터 파일 tooprocess 다운로드*

일괄 처리 **작업** hello 개별 작업 단위 hello를 실행 하는 계산 노드는 합니다. 작업 명령줄 개이고 hello 스크립트 또는 명령줄에서 지정 하는 실행 파일을 실행 합니다.

작업을 수행 하는 tooactually, 작업 tooa 작업을 추가 해야 합니다. 각 [CloudTask] [ net_task] 명령줄 속성을 사용 하 여 구성 및 [ResourceFiles] [ net_task_resourcefiles] (hello 풀 StartTask와 마찬가지로)를 해당 명령줄이 자동으로 실행 하기 전에 hello 작업 toohello 노드를 다운로드 합니다. Hello에 *DotNetTutorial* 샘플 프로젝트를 각 작업에서는 하나의 파일을 처리 합니다. 따라서 ResourceFiles 컬렉션은 단일 요소를 포함합니다.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> 와 같은 환경 변수에 액세스 하면 `%AZ_BATCH_NODE_SHARED_DIR%` hello 노드에 없는 응용 프로그램을 실행 또는 `PATH`, 작업 명령줄 ज ा य `cmd /c`합니다. 명시적으로 hello 명령 인터프리터 실행 되 고 tooterminate 명령을 수행한 후 지시 합니다. 이 요구 사항을 작업 hello 노드의 응용 프로그램을 실행 하는 경우에 필요 하지 않습니다. `PATH` (같은 *robocopy.exe* 또는 *powershell.exe*) 및 환경 변수 사용 됩니다.
>
>

Hello 내 `foreach` hello 위의 코드 조각에서 루프를 3 개의 명령줄 인수는 너무 전달 되도록 hello 작업에 대 한 hello 명령줄 생성을 확인할 수 있습니다*TaskApplication.exe*:

1. hello **첫 번째 인수** hello 파일 tooprocess hello 경로입니다. Hello 노드에 있는 것 처럼 hello 로컬 경로 toohello 파일입니다. 때 ResourceFile 개체에 hello `UploadFileToContainerAsync` 처음 만들어진 위, hello 파일 이름이 (매개 변수 toohello ResourceFile 생성자)으로이 속성에 사용 되었습니다. 해당 hello 파일이 hello에 동일한 나타냅니다으로 디렉터리 *TaskApplication.exe*합니다.
2. hello **의 두 번째 인수** 해당 hello 위쪽 *N* 단어 toohello 출력 파일이 작성 해야 합니다. Hello 예제에서이 하드 코드 된 상위 세 단어 hello toohello 출력 파일 기록 되도록 합니다.
3. hello **세 번째 인수** toohello 쓰기 액세스를 제공 하는 hello 공유 액세스 서명 (SAS)은 **출력** Azure 저장소의 컨테이너입니다. *TaskApplication.exe* hello 출력 파일 tooAzure 저장소에 업로드 하는 경우 사용 하 여가 공유 액세스 서명 URL입니다. Hello에서이 대 한 hello 코드를 찾을 수 있습니다 `UploadFileToContainer` hello TaskApplication 프로젝트에서 메서드 `Program.cs` 파일:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>6단계: 작업 모니터링
![작업 모니터링][6]<br/>
*hello 클라이언트 응용 프로그램 (1) 모니터 hello 완성 및 성공 상태에 대 한 작업 및 (2) 작업 업로드 결과 데이터 tooAzure 저장소 hello*

작업 tooa 작업 추가 되 면 자동으로 큐에 대기 되며 hello 작업과 연결 된 hello 풀 내에서 계산 노드에서 실행 되도록 예약 됩니다. 지정 된 hello 설정에 따라, 일괄 처리 모든 작업 큐, 예약, 다시 시도 및 기타 작업 관리 업무에 대 한 처리 있습니다.

가지 많은 작업 실행이 toomonitoring입니다. DotNetTutorial은 완료 및 태스크 실패 또는 성공 상태에 대해서만 보고하는 간단한 예제를 보여 줍니다. Hello 내 `MonitorTasks` DotNetTutorial의 메서드에서 `Program.cs`는 토론을 보증 하는 세 가지 일괄 처리.NET 개념이 있습니다. 표시된 순서에 따라 아래 나열되어 있습니다.

1. **ODATADetailLevel**: 목록 작업에서 [ODATADetailLevel][net_odatadetaillevel] 지정(작업의 태스크 목록을 가져오는 것과 같은)은 Batch 응용 프로그램 성능을 보장하는 데 반드시 필요합니다. 추가 [hello Azure 배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md) 모든 종류의 일괄 처리 응용 프로그램 내에서 상태 모니터링을 수행 하려는 경우 목록을 읽는 tooyour 합니다.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor]는 태스크 상태를 모니터링하기 위한 도우미 유틸리티를 사용하여 Batch .NET 응용 프로그램을 제공합니다. `MonitorTasks`, *DotNetTutorial* 모든 작업 tooreach 될 때까지 대기 [TaskState.Completed] [ net_taskstate] 제한 시간 내에서. 그런 다음 hello 작업을 종료 합니다.
3. **TerminateJobAsync**: 작업이 종료 [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (또는 hello JobOperations.TerminateJob 차단) 해당 작업을 완료로 표시 합니다. 필수 toodo는 일괄 처리 솔루션에서 사용 하는 경우는 [JobReleaseTask][net_jobreltask]합니다. 이것은 특수한 유형의 태스크이며, [작업 준비 및 완료 태스크](batch-job-prep-release.md)에 설명이 있습니다.

hello `MonitorTasks` 메서드에서 *DotNetTutorial*의 `Program.cs` 아래에 표시 됩니다.

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>7단계: 작업 출력 다운로드
![Storage에서 작업 출력 다운로드][7]<br/>

Hello 작업이 완료 되 면 했으므로 hello 작업의에서 출력을 hello Azure 저장소에서 다운로드할 수 있습니다. 이렇게 호출 하 여 너무`DownloadBlobsFromContainerAsync` 에 *DotNetTutorial*의 `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> 호출을 너무 hello`DownloadBlobsFromContainerAsync` hello에 *DotNetTutorial* 응용 프로그램 파일을 지정 하 hello 다운로드 한 tooyour `%TEMP%` 폴더입니다. 무료 toomodify 느껴집니다이 위치를 출력 합니다.
>
>

## <a name="step-8-delete-containers"></a>8단계: 컨테이너 삭제
Azure 저장소에 있는 데이터에 대 한 요금이 청구 되므로 항상 이므로 일괄 처리 작업에 대해 더 이상 필요 없는 것이 좋습니다 tooremove blob입니다. DotNetTutorial의에서 `Program.cs`, 이렇게 3 개의 호출이 toohello 도우미 메서드로 `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

hello 메서드 자체 단순히 참조 toohello 컨테이너를 가져오고 다음 호출 [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a>9 단계: hello 작업과 hello 풀 삭제
이제 마지막 단계인 hello 메시지 표시 toodelete hello 작업과 hello 풀 hello DotNetTutorial 응용 프로그램에서 생성 된 것입니다. 작업 및 태스크 자체에 대한 요금이 부과되지 않지만 계산 노드에 대한 요금이 청구 *됩니다*. 따라서 노드를 필요할 때만 할당하는 것이 좋습니다. 사용하지 않는 풀을 삭제하는 것이 유지 관리 프로세스의 일부가 될 수 있습니다.

hello BatchClient의 [JobOperations] [ net_joboperations] 및 [PoolOperations] [ net_pooloperations] 경우 이라고 하는 해당 삭제 방법을 둘 다 hello 사용자 삭제를 확인합니다.

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> 계산 리소스에 대해 요금이 부과되고 사용하지 않는 풀 삭제는 비용을 최소화한다는 점을 유의하세요. 또한,을 해당 풀에서 모든 계산 노드를 삭제할 풀을 삭제 하 고는 hello 노드에서 모든 데이터를 복구할 수 없습니까 hello 풀이 삭제 된 후 주의 합니다.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Hello 실행 *DotNetTutorial* 샘플
Hello 샘플 응용 프로그램을 실행 하면 비슷한 toohello 다음 hello 콘솔 출력이 됩니다. 실행 중에 일시 중지 길어집니다 `Awaiting task completion, timeout in 00:30:00...` hello 풀 계산 노드에서 시작 됩니다. 사용 하 여 hello [Azure 포털] [ azure_portal] toomonitor 풀, 계산 노드, 작업 및 작업 동안과 그 후 실행 합니다. 사용 하 여 hello [Azure 포털] [ azure_portal] 또는 hello [Azure 저장소 탐색기] [ storage_explorers] tooview hello 저장소 리소스 (컨테이너 및 blob)를 hello 응용 프로그램에 의해 만들어집니다.

일반적인 실행 시간은 **약 5 분** hello 응용 프로그램 기본 구성에서 실행할 때.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>다음 단계
무료 toomake 변경 너무 느껴집니다*DotNetTutorial* 및 *TaskApplication* tooexperiment 서로 다른 시나리오를 계산 합니다. 예를 들어 너무 실행 지연을 추가 해 보십시오*TaskApplication*등와 마찬가지로 [Thread.Sleep][net_thread_sleep], toosimulate 장기 실행 작업 및 hello 포털에서이 모니터링 합니다. 시도 더 많은 작업을 추가 하거나 hello 계산 노드 수를 조정 합니다. 에 대 한 논리 toocheck를 추가 하 고 기존 풀 toospeed 실행 시간이 hello 사용 허용 (*힌트*: 체크 아웃 `ArticleHelpers.cs` hello에 [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] 프로젝트에서 [azure 일괄 처리-샘플][github_samples]).

이제 일괄 처리 솔루션의 기본 워크플로 hello에 익숙하다면 toohello hello 일괄 처리 서비스의 추가 기능에서 toodig 시간입니다.

* 검토 hello [Azure 배치 개요 기능](batch-api-basics.md) 아티클의 새 toohello 서비스 하는 경우는 것이 좋습니다.
* 시작 hello에서 다른 일괄 처리 개발 문서 **개발 심층 분석** hello에 [일괄 학습 경로][batch_learning_path]합니다.
* 체크 아웃의 hello에서 일괄 처리를 사용 하 여 "상위 n 개 단어" hello 작업 부하를 처리 한 다른 구현을 [TopNWords] [ github_topnwords] 샘플.
* 검토 hello 일괄 처리.NET [릴리스 정보](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) hello 라이브러리에 최신 변경 내용을 hello에 대 한 합니다.

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "업로드 작업 응용 프로그램에 대 한 입력 (데이터) toocontainers 파일"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch 풀 만들기"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch 작업 만들기"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "작업 toojob 추가"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "작업 모니터링"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Storage에서 작업 출력 다운로드"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch 솔루션 워크플로(전체 다이어그램)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "포털의 Batch 자격 증명"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "포털의 Storage 자격 증명"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch 솔루션 워크플로(최소 다이어그램)"
